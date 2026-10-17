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
| Steam | One product; Career leads the store page, Academy is a feature bullet; achievements split by mode. Free web edition = Career Era 1 + Academy limited to Era 1 objectives |

## Bad tickets (2026-10-06)

Five kinds (vague, user error, duplicate, wrong team, misleading diagnosis), graded by `triage`. Checking before acting earns +20% XP; closing unverified halves XP and costs reputation; changing config on a no-change ticket costs 10 reputation; asking for a password costs 10. About 20% of incoming tickets, more in Night Watch.

## Academy look (2026-10-06)

The Academy has its own plain study theme, independent of the career skin: flat background, solid dark header, white cards, and it follows the OS light/dark setting. Reason: the career skins' patterned wallpapers made the Academy text hard to read, and the skins' chrome styles leaked into the Academy header.

## Console (2026-10-06)

- Styled after Windows Terminal running PowerShell, in the game's colours: a tab strip (device tab, `+`, `˅` device menu), the prompt and input inline on the last line, no toolbar buttons.
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

## Repo and notes (2026-10-15)

- Netmancer lives in its own repo at `E:\Projects\Netmancer`, never inside HomeNet Dash.
- Project knowledge is kept in `docs/` as an Obsidian vault, so a session reads these pages instead of the game file. The design doc stays the long-form reference; decisions made in sessions are recorded here first.
