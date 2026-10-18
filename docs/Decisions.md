---
title: Decisions
tags: [design]
updated: 2026-10-15
---

# Decisions

The short form. The reasoning lives in the design doc; this page records what was decided and when.

## Naming rule (from the start)

Every command, keyword, protocol name and output format is real, so what the player learns transfers to the exam and the job. Only trademarked brands get fictional names: Arcanet Systems / RuneOS for the gear, Casement for Windows, Oakhollow for Linux, Wardgate for the VPN client. CCNA and Cisco are named only in plain description with a not-affiliated disclaimer; no logos.

## Game modes (2b, decided 2026-10-06)

| Decision | What |
| --- | --- |
| Two modes, one engine | **Zero to Hero** (Career) and **The Academy** (Training) share the engine, content and one ticket picker |
| Shared skill profile | Runes (mastery 0–100 and a review date per objective), cards, drills, Grimoire and settings are one profile. Each career is its own save slot |
| The fading rule | A rune past its review date fades. A faded rune in a school holds the next promotion in that school. Practising it anywhere recharges it |
| No grinding | The Academy never grants career XP, reputation, rank or money. Career ranks never drop once earned |
| Directors | Career: era and rank gating, Mail delivery, Night Watch. Academy: weights objectives by low mastery and fading (or by blueprint weight for a mixed set), tier adapts per objective, plain wording forced on |
| Unlocks | Academy is fully open. Career keeps era and rank gates |
| Practice from Career | A failed ticket's debrief, or two failed checks, offers *Practise in the Academy* preset to its objectives. The career ticket and network are kept and its SLA clock pauses |
| No Endless mode | Career covers it (Night Watch now, contract work later). Academy has a timed mixed set, later the Trial |

## Bad tickets (2026-10-06)

Five kinds (vague, user error, duplicate, wrong team, misleading diagnosis), graded by `triage`. Checking before acting earns +20% XP; closing unverified halves XP and costs reputation; changing config on a no-change ticket costs 10 reputation; asking for a password costs 10. About 20% of incoming tickets, more in Night Watch.

## Study theme and title screen: the Layer Eight look (2026-10-17)

Colby likes the console but not the theme; he wants the game styled like the staged Layer Eight Systems redesign (`D:layereightsystems`, `app/globals.css`): near-black slate surfaces (`#0a0d12` page, `#10151c` cards, `#161c25` inputs), lines `#242c37`/`#33404f`, ink `#e6edf3` / dim `#a3afbc`, one signal-green accent `#3ddc97` with `#04140c` text on it, warn `#f5c451`, error `#ff8080`, radii 12 and 8, Inter for text and IBM Plex Mono for labels, headings 600 with −0.02em tracking, a faint 48 px blueprint grid. Applied to Lab & Course, the Academy and the title screen; the career skins and the Tabby console are untouched. Dark only (`color-scheme: dark`), like the site. Fonts come from Google Fonts and fall back to system fonts offline.

## Academy look (2026-10-06)

The Academy has its own plain study theme, independent of the career skin: flat background, solid dark header, white cards, and it follows the OS light/dark setting. Reason: the career skins' patterned wallpapers made the Academy text hard to read, and the skins' chrome styles leaked into the Academy header.

## Console (2026-10-06)

- Styled after Windows Terminal running PowerShell, in the game's colours: a tab strip (device tab, `+`, `˅` device menu), the prompt and input inline on the last line, no toolbar buttons.
- Colours and type (2026-10-17, Colby's Tabby theme): one palette in every mode and skin, dark violet-grey background `#1e1c2c`, lavender text, the echoed command word in blue and its arguments in orange (as Clink paints them), semibold Cascadia Code / JetBrains Mono / Consolas, the prompt and input inline with no box. Variables live on `.tv` (`--tbg --tfg --tp --tcmd --targ --tok --terr --tfont`).
- No *Save config* button. On a switch or router you save with `write memory` or `copy running-config startup-config`, as on real gear. *Check the fix* survives only in the right-click menu.
- Font size: Ctrl+= / Ctrl+- / Ctrl+0 or Ctrl+wheel. Touch screens get a small run button and the quick-insert key row; PCs don't.
- `?` and Tab work on every shell. On the PC shells a `?` right after `/`, `-`, `[` or `:` is literal so `ipconfig /?` still works.

## Lab mode and the course (2026-10-15)

Colby's direction: develop the game first as his own study tool, hands-on simulation with freedom, as close to real gear as the engine allows. The course follows CCNA from the beginning ("how RJ45 works → plug one in") and builds one network as it goes.

| Decision | What |
| --- | --- |
| Third mode | **Lab & Course** is the first tile on the title screen. Blank canvas or a clean preset (the three ticket topologies with no fault). Labs are saved in the shared profile; the course has its own lab |
| Cable model | Links carry a cable type: copper straight-through (default), crossover, console, fiber. Gigabit copper ports auto-MDIX, so straight and crossover both come up. Fiber is refused at plug time until there are SFP ports. Console cables fit only the virtual `con0` (switch, router) and `com1` (PC with an OS) ports, which L1–L3 never see |
| Console access | *Realistic console access* (Lab tab) requires a console cable from a PC to the device's `con0`, or SSH over the network. **Off by default** (Colby's call); lesson 1.03 teaches the cable either way |
| Graded by state, plus "you ran it" | Lesson goals use the same state checks as tickets. Lessons about looking (`show mac address-table`, `arp -a`) use the `ran` check over `net.cmdlog`, which exists only on lab nets |
| Crash-safe goals | A goal on a device that does not exist yet reads "(not ready yet)" rather than throwing |
| Lesson setup | A lesson's `setup` steps (same format as `solution`) are applied once when it first opens, so ticket faults can be injected into the growing lab (1.15 is T-002's dead DNS) |
| Plain terms by default | New profiles start plain; an old profile stays plain until the flavour is chosen in Settings. Lab mode always reads plain |
| Labs not in save codes | Save codes carry course progress but not labs (size). Labs export and import as JSON |
| Milestone cut | Lab mode + Module 1 (15 lessons). Module 2 is written up in the backlog and the Course tab shows it as "coming" |

## Command drill (2026-10-17)

Colby asked for a way to practise CLI commands like flash cards. Choices made with him: it lives in Lab & Course as a Commands tab; a card is answered by typing in the real console on a scratch device, not in a text box; the first deck covers Module 1 only and grows with the course.

| Decision | What |
| --- | --- |
| Scratch network per card | Every card loads a fresh network (SW1, R1 with DHCP, PC1 on DHCP, PC2 static, SRV1 as DNS) so config cards cannot wreck the lab and each card starts from a known state. The lab record is saved before the swap and never written while the drill is on |
| Graded by what you typed and what it did | A card passes when a typed line matches one of its accept patterns (IOS abbreviations allowed: `sh int status` counts) and, for config cards, the device state check passes. First try = Good, detours = Hard, Reveal = Again |
| Hands on the keyboard | Cards are scenarios printed in the terminal ("We have X. Grab Y from the CLI."). A correct answer advances by itself; skip, reveal, quit and again are typed at the prompt and intercepted before the shell sees them. The side panel mirrors the card but nothing needs a click once a set has started |
| `?` and Tab stay on | Colby: it encourages exploration and helps the practice. Context help shows the next keyword, not the whole answer; reveal is still there for a blank |
| Same spaced repetition as review cards | `C.srs` records per card in the profile; due cards come first. Each answer also feeds the card's objectives' runes with the card weight, so the drill shows in the skill profile but never grants career XP |
| Deck proven by the self-test | `testCmdDrill` answers every card with its reference answer and fails the build if an answer errors, does not match its own patterns, or leaves the state check false |

## Drill statistics and badges (2026-10-17)

Colby wanted the Commands tab more compelling and informative. His choices: mastery tiers and badges only (no points, nothing touches career XP), no daily streak (statistics only), speed tracked quietly for a fluency tier, all inside the Commands tab.

| Decision | What |
| --- | --- |
| Four tiers per card | new → learning → known (two SRS reps and two first-try answers in a row) → fluent (the last three first-try answers each under 6 s per answer line). A reveal drops the card to learning. No visible timer |
| Start here | One recommendation with its reason, in this order: a refresher after 7+ days away (trouble + due + known cards), due cards, the weakest objective (trouble score ≥ 1.5: reveals ×2 + retries, per card), new cards, a mixed ten |
| Weak spots | Per objective and per device: accuracy, reveals, retries, a trouble score; trouble cards (any reveal, or under 60 % right) get their own one-card sessions |
| Badges | Fourteen, plain names (First blood, Clean sweep, Ten in a row, Fast hands, Switch/Router/Desktop/Server hand, Module 1 known/fluent, Hundred club, Comeback, Scholar, Explorer). Tests in core, names in content, earned once, toast + a terminal line |
| No streak | By Colby's choice: the 14-day bars show activity, nothing nags |
| Why it works | Each card carries a `why`: the mechanism in TCP/IP terms and a few other situations the command answers. Printed after a correct answer (the drill waits a little longer before the next card) and after a reveal |

## Academy guide (2026-10-17)

Colby: the Academy should guide you to the answer and make you type the commands, but give you the command: point out the important details in the request, explain briefly why they matter, then walk through to resolution. Choices: Era 1 tickets hand-written first (the rest built from their hints and solution), a *Guide me* toggle per ticket (off by default, remembered in the profile), one step at a time.

| Decision | What |
| --- | --- |
| Facts first | The guide quotes the request (marked in the symptom and brief with a number) and says why each detail matters, before any command |
| One step at a time | Each step names the device, the command to type, what to read in the output and why. The next step appears when a typed line on that device matches (show steps) or the device state proves it (fix steps). Skip exists; read steps have Done |
| Costs the same as the full-commands hint | Turning the guide on reveals hint 4, so a guided ticket earns half mastery, like one solved with the exact commands shown |
| Hand-written where it matters | `content.guides` for T-001, T-002, T-003, T-006, T-007; the engine self-test replays each guide and fails the build if it does not solve its ticket. Other tickets get an automatic guide until written |

## Console wrapping (2026-10-17)

The console log wraps long lines (`pre-wrap`, `overflow-wrap: anywhere`) instead of scrolling sideways, so a narrower window keeps everything readable. Tables lose their alignment when they wrap, which is what a real terminal does too.

## Lab palette (2026-10-17)

Packet Tracer layout: a palette column of icon tiles (Network, End devices, Cables) beside the canvas, tools in a slim row above it. Colby found the earlier tab-and-row bar fiddly. Port labels are placed outside the node shape, drawn on top with a halo, so they never hide under a node or under each other.

## Lab goals explain themselves (2026-10-17)

A failing reach goal in a lesson says why ("PC1 reaches PC3 — PC1 has no default gateway"). The engine already computed the reason; hiding it only cost study time. Career and Academy tickets do not show it: there the diagnosis is the exercise.

## Repo and notes (2026-10-15)

- Netmancer lives in its own repo at `E:\Projects\Netmancer`, never inside HomeNet Dash.
- Project knowledge is kept in `docs/` as an Obsidian vault, so a session reads these pages instead of the game file. The design doc stays the long-form reference; decisions made in sessions are recorded here first.
