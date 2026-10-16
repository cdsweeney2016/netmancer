---
title: Backlog
tags: [planning]
updated: 2026-10-15
---

# Backlog

Pick from the top. Each item says what it touches so a session can scope it without reading the game file.

## Next milestone: Course Module 2, Network Access

Fifteen lessons, listed in [Course](Course.md). They need no engine work until 2.14 and 2.15 (`kind:'stub'` until then). Order: VLANs → access ports → router-on-a-stick → trunk to SW2 → allowed list and native VLAN → CDP → voice VLAN → management SVI → SSH → console line, banner, encryption → EtherChannel → PortFast and BPDU guard → port security → Rapid PVST+ (stub) → wireless (stub). Touches content (`course.lessons`), maybe a `port_vlan`/`voice_vlan`/`native` check or two in `CHECKS`.

## Lab mode follow-ups

- [ ] **Collapsible side panel on phones.** The lesson panel sits above the map and terminal, so a phone scrolls a long way to reach the console. A collapse toggle on the panel, or a tab that swaps panel/map/terminal.
- [ ] **Spread new devices.** `labFreeXY` stacks the first devices in one column; a nicer default layout (hosts under their switch) would save dragging.
- [ ] **Fiber and SFP ports.** `labLink` refuses fiber today. Add SFP uplink ports on the switch model and a fiber cable type.
- [ ] **Lab sharing.** Export is JSON in a download or a textarea. A share code (deflate + base64) would fit a chat message.

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

## Large: engine gaps, grouped by the course module waiting on them

Colby's fidelity priorities: spanning tree, ACLs and NAT, services (DHCP relay, HSRP, NTP, syslog). IPv6 last.

- [ ] **Module 2 (2.14):** Rapid PVST+ state: root election, port roles and states, `show spanning-tree`. PortFast and BPDU guard already exist as errdisable triggers.
- [ ] **Module 3:** static routes and OSPF already exist; add `show ip ospf` detail, passive interfaces, default routes.
- [ ] **Module 4 (IP Services):** NAT translation table (`show ip nat translations`), DHCP relay (`ip helper-address`), HSRP (`standby`, `show standby`), NTP (`ntp server`, `show ntp status`), syslog to a server (`logging host`).
- [ ] **Module 5 (Security):** ACLs that filter traffic (today `access-list` only feeds NAT), `show access-lists` hit counts, AAA basics.
- [ ] **Wireless (2.15, 1.x):** basic WLC/AP state.
- [ ] **IPv6:** addressing, SLAAC, static routes. Last by choice.
- [ ] Career Era 4 content: a three-site topology and 8–10 tickets for objectives 4.x and 5.x, plus the Wizard rank gate.

## Done

- [x] 2b: title screen, Academy, shared profile, fading rule, generator (2026-10-06)
- [x] Academy study theme (2026-10-06)
- [x] `?` help and Tab completion on PC shells; Save config button removed (2026-10-06)
- [x] Windows Terminal-style console (2026-10-06)
- [x] Own repo + docs vault (2026-10-15)
- [x] Lab mode + CCNA course Module 1 (15 lessons), plain terms by default (2026-10-15)
