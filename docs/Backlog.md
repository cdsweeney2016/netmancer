---
title: Backlog
tags: [planning]
updated: 2026-10-15
---

# Backlog

Pick from the top. Each item says what it touches so a session can scope it without reading the game file.

## Small (finish 2b properly)

- [ ] **Plain hints in the Academy.** Ticket `hints` are written in wizard flavour ("Scry the switch"). In the Academy they should read plain. Options: a `plainHints` field per ticket, or a flavour→plain word map applied in `acBrief`. Touches content + `acBrief`.
- [ ] **Daily review ticket in Career.** The doc wants one review quest a day driven by faded runes. `nightHex` could ask `pickTicket` for the most-faded objective instead of the day-number template on some nights. Touches `nightHex`, `mailbox`.
- [ ] **Decide on *Check the fix*.** It now lives only in the console's right-click menu. Keep, or remove entirely.
- [ ] **Real iOS keyboard test.** Only emulated so far. Check the inline input and the quick-insert row with the real on-screen keyboard.

## Medium

- [ ] **Trial of the Conclave.** The timed mock exam: questions sampled by blueprint weight (`domainWeight`), multiple choice plus short lab tickets from the picker, flavour-free, with a readiness view from the runes. New Academy view; needs a question bank in the content pack.
- [ ] **"Story off" career option.** Placeholder until there is a story to switch off.
- [ ] **Bad tickets in the Academy.** They need Mail's triage panels, which the Academy doesn't have. Either a Triage drill view or leave them Career-only.
- [ ] **Push the repo to a remote** (Gitea or GitHub).

## Large (Era 4: Network Engineer)

- [ ] Engine: ACLs that filter (today `access-list` only feeds NAT), NAT translation table, DHCP relay (`ip helper-address`), FHRP (HSRP), basic wireless (WLC/AP) state.
- [ ] Content: a three-site topology and 8–10 tickets for objectives 4.x and 5.x, plus the Wizard rank gate.

## Done

- [x] 2b: title screen, Academy, shared profile, fading rule, generator (2026-10-06)
- [x] Academy study theme (2026-10-06)
- [x] `?` help and Tab completion on PC shells; Save config button removed (2026-10-06)
- [x] Windows Terminal-style console (2026-10-06)
- [x] Own repo + docs vault (2026-10-15)
