---
title: Architecture
tags: [reference]
updated: 2026-10-15
---

# Architecture

`netmancer.html` holds four `<style>` blocks and five `<script>` blocks. Everything below is addressed by function name; grep for it rather than reading the file top to bottom.

## The five script blocks

| # | Block | Lines | What it is |
| --- | --- | --- | --- |
| 1 | error overlay | 1 | Shows JS errors on screen in `#selftest` and `#demo-*` modes only |
| 2 | `NetmancerCore` | ~1,450 | The engine. Pure logic: no DOM, no storage. Portable to a worker or Electron |
| 3 | `NetmancerContent` | ~730 | Data only: topologies, tickets, cards, objectives, ranks, wiki text |
| 4 | `WebPlatform` | 13 | Storage and clipboard adapter (`storage.get/set/del`, `copy`) |
| 5 | `NetmancerOS` | ~1,050 | The UI: title screen, workstation apps, the Academy, self-tests |

Style blocks: base styles, the three career skins (`#skins`: arcane, torch, tower; `classic` is no `data-theme`), the workstation chrome (`#os-css`), and the 2b additions (title screen, Academy study theme, Windows Terminal-style console, rune chips).

## NetmancerCore, in order

| Area | Key functions |
| --- | --- |
| Utilities | `ip2n` `n2ip` `maskLen` `inCidr` `fnv` (hash) `canon` (stable JSON) `parseIfName` `shortIf` |
| Device factories | `newSwitch` (24 Gi ports + Vlan1) `newRouter` (4 Gi ports) `newHost` (pc, laptop, server, printer, phone, iot) |
| Build | `buildNet(topo, quest)`: devices, links, topology `config` (seeded through the real CLI with `seed`), then the quest's `faults`, `hosts`, `cond`, `down`, `dnsAdd`, `errdisable`. Snapshots each device's startup-config |
| Recompute | `refresh(net)`: `computeL1` (link, speed/duplex via `nego`) → `computeEC` (EtherChannel bundling) → `computeOp` (access/trunk via DTP) → `detectErr` (BPDU guard, port security) → `computeSvi` → `computeDhcp` → `computeOspf` → `cdpChecks` → `linkEvents` (syslog lines) |
| Layer 2 | `bfs`/`domain`: flooding domain over switch×VLAN nodes; `receive` decides how a frame enters a device |
| Layer 3 | `routesOf` `lookup` (longest prefix, then AD) `routerForward` `hostSend` `reach` (also checks the return path) `reachPort` |
| DNS | `resolveName(net, host, name)`: walks the host's DNS servers, internal zone vs public resolvers |
| RuneOS CLI | `S(modes, dev, pattern, fn)` registers a command spec (204 of them). `specsFor` `walk` `filterLive` `resolve` do prefix matching. `Ios` is a session: `exec` `dispatch` `helpText` (`?`) `complete` (Tab) `errOut` (caret errors) |
| Show commands | `runningConfig` `showIpIntBrief` `showIntStatus` `showInterface` `showTrunk` `showVlan` `showMac` `showEtherSummary` `showPortSec` `showCdp` `showIpRoute` `showRouteEntry` `showOspfNbr` `showOspfIfBrief` `showProtocols` `showDhcpBinding` `showIpSsh` `showArp` `iosPing` `iosTrace` |
| PC shells | `Casement` (cmd; `powershell` switches `ps` on, cmdlets in `PSCMD`), `Oak` (bash-like). `ipconfig` `winPing` `winTrace` `nslookup` `netsh` `sshCmd` `linuxIp` `dig` |
| Bad-ticket overlays | `condRun` and the `ov*` functions fake a remote laptop, guest Wi-Fi, airplane mode, Caps Lock, a printer out of paper. `wardgate` is the VPN client. `adUser` `netCmd` fake the directory |
| Terminal | `Terminal`: a stack of shells on one device (`attach` `exec` `help` `complete` `wantsHelpKey(line)`). SSH pushes a new `Ios` onto the stack |
| Shell help | `CMDTREE` `PSTREE` `OAKTREE` + `treeWalk` `shellHelp` `shellComplete`: `?` and Tab for the PC shells. On PC shells a `?` right after `/`, `-`, `[` or `:` is literal |
| Grader | `CHECKS` table (`host_net` `reach` `trunk_up` `bundle` `saved` `failover` `ospf_nbr` … 26 kinds) and `grade(net, quest)` → `{pass, results, style}` |
| Templates | `instantiate(tpl, k)` fills `{{var}}` placeholders; `watchFor(content, t)` picks the day's Night Watch hex |
| Drills | `drillQ(level, rng, mode)` subnetting questions; `adapt` moves the level |
| Review | `srsNew` `srsReview` (SM-2 style) `srsDue` `srsPick` |
| Runes | `runeScore({pass, pen, late})` `runeUpdate` `runeState` (new / fresh / fading) `runeApply` `weakWeights`. Config in `RUNE` |
| Picker | `ticketPool(content)` = quests ∪ expanded watch templates ∪ bad tickets. `pickTicket(content, {seed, objectives, weights, tierRange, eras, kinds, exclude})` is deterministic per seed |
| Triage | `triage(content, q, act, ctx)`: grades ask / user / team / merge / fix on bad tickets. Constants in `TRI` |
| Self-test | `testQuest` `testBad` `testTriageData` `testDrills` `testSrs` `testModes` → `selfTest(content)` |

## NetmancerContent

Exported as one object: `topologies` (ground, closet, tower), `quests`, `watch`, `badTickets`, `triage` (asks, guides, teams), `questCards`, `drillCards`, `objectives`, `domainWeight`, `schools`, `ranks`, `eras`, `tiers`, `glossary`, `spellbook`, `cliCases`, `os` (wiki, runbooks, welcome), `artifacts`. See [Tickets](Tickets.md) for the schema and the catalogue.

## NetmancerOS

| Area | Key functions |
| --- | --- |
| Save model | `fresh` `splitSave` `mergeSave` `load` `saveNow`. In memory `S` is one merged object; on disk it is split by `PROF_KEYS` into the shared profile and the current career slot. See *Saves* below |
| Rules | `rankIdx` (sticky rank + fading rule) `gateMet` `blockedBy` `eraOpen` `visibleQuests` `badVisible` `nightHex` `addXp` |
| Ticket flow | `startQuest(q, {mode, silent})` → `doCheck` → `complete` (career) or `completeAcademy`. `doTriage(act)` for bad tickets. `revealHint` `resetQuest` `grim` (mistakes journal) |
| Cards | `addCard` `questCardsFor` `unlockSpells` `cardRune` |
| Academy | `enterAcademy` `leaveAcademy` (stashes the career ticket, pauses its SLA) `startRun` `acReq` (the director's request to `pickTicket`) `acNext` `acFinish` `acRender` `acHome` `acRun` `acBrief` `acSum` |
| Mail | `mailbox` builds the message list from quests, bad tickets and the nightly hex; `MailApp` renders tickets, triage panels and the debrief |
| Files | A virtual home folder: `vfsList` `vfsRead` `vfsWrite`. Runbooks, ticket attachments, saved configs, the Grimoire |
| Window manager | `openApp` `focusWin` `closeWin` `tileWin` `mountWin`; `WM.mode` is desktop or mobile |
| Apps | `TermApp` `MailApp` `FilesApp` `NotesApp` `MapApp` `BrowserApp` (wiki + training portal via `trainMount`) `SkillsApp` `SettingsApp` |
| Shell | `boot` → `titleScreen` → `setup` / `loginNow` → `session`; `toTitle` `signOut` `restart` |
| Tests | `uiSelfTest` (workstation) `modeSelfTest` (saves, modes, fading rule) `fullTestReport` |
| Dev modes | URL hash `#selftest` `#demo-mail` `#demo-phone` `#demo-academy` set `DEV` and use a throwaway save |

## How a ticket runs

1. Mail → Accept, or Academy → run: `startQuest(q)` builds `net = C.questNet(K, q)` and sets `S.active`.
2. The terminal mutates `net` through `Terminal.exec`. A changing command marks the session dirty, which calls `refresh(net)` and emits syslog lines.
3. Career: Reply & resolve runs `doTriage({type:'fix'})` → `doCheck` → `C.grade`. Academy: Check my fix calls `doCheck` directly.
4. `complete`: XP per school (hint penalty, SLA bonus, replay 25%, style bonus, triage multiplier), reputation, `S.done`, cards, runes, promotion check. `completeAcademy`: runes and cards only.

## Saves

- `localStorage` keys: `netmancer.profile.v1` (shared: cards, drill, grim, plain, font, theme, runes, academy), `netmancer.career.<n>.v2` (xp, rep, done, active, watch, os, rank…), `netmancer.careers` (slot index). Dev modes prefix them with `netmancer.dev.<mode>.`.
- A pre-2b `netmancer.save.v1` is migrated into slot 1 on first load and kept as a backup.
- Save codes: `NMC2-<checksum>-<base64>`; `NMC1` codes still import.

## Conventions

- ES5-style code, one statement-dense line per function. No build step, no dependencies, no template literals.
- Every command, keyword and output format is real. Only brands are fictional. Check the trademark table in the design doc before naming anything.
- Engine, content and UI stay separate: the engine never touches the DOM; content is data only.
