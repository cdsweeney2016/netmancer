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

## Repo and notes (2026-10-15)

- Netmancer lives in its own repo at `E:\Projects\Netmancer`, never inside HomeNet Dash.
- Project knowledge is kept in `docs/` as an Obsidian vault, so a session reads these pages instead of the game file. The design doc stays the long-form reference; decisions made in sessions are recorded here first.
