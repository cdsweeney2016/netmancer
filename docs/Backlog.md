---
title: Backlog
tags: [planning]
updated: 2026-10-15
---

# Backlog

Pick from the top. Each item says what it touches so a session can scope it without reading the game file.

## Done 2026-10-29: Course Module 3, IP Connectivity (3.01-3.09, 3.10 FHRP stub)

R2 over 10.0.12.0/30 on R1 Gi0/1, branch SW3 + PC4 on 192.168.40.0/24, statics, default, OSPF area 0 with router-ids 1.1.1.1 / 2.2.2.2, passive LAN interfaces, backup link 10.0.21.0/30 on Gi0/2 with floating statics (AD 200), hello-timer fault lesson. HSRP (3.10) waits for the engine.

## Next milestone: Course Module 4, IP Services

NAT/PAT needs an internet device in the course lab (an ISP router the lab cannot add yet), DHCP relay (`ip helper-address` is not in the engine), NTP, syslog and SNMP need engine models. Also the HSRP engine for 3.10 and the STP engine for 2.14.

## Was: Module 3 plan

Static routes, a default route, single-area OSPF between R1 and a second router R2, a floating static, first-hop redundancy (HSRP needs the engine). The lab leaves Module 2 as SW1 (VLANs 10/20/30/99, trunks, Po1 to SW2, SSH, port security) and R1 as router-on-a-stick; Module 3 adds R2 and a second site.

## Module 2 follow-ups

- [ ] **IP phone PC port.** Phones have one port; a real phone bridges a PC through its second port (untagged data VLAN, tagged voice). Needs a two-port bridging host in the engine, then lesson 2.07 can put PC1 behind PH1 (Colby hit this on 2026-10-28).
- [ ] **2.14 Rapid PVST+ and 2.15 wireless** are stubs until the spanning tree engine and a wireless model exist.
- [ ] **Command cards for Module 2** (VLANs, trunks, EtherChannel, port security, SSH, CDP) in `cmdDrill.cards`.

## Academy guide follow-ups

- [ ] **Hand-written walkthroughs for Era 2 and 3 tickets** (17 tickets). Same schema as `content.guides`; `testGuides` proves each one. Until then they use the automatic guide.
- [ ] **Guide for bad tickets** (triage): facts that show it is a user-error or duplicate ticket, then the triage action.

## Command drill follow-ups

- [ ] **Badges and recommendation for Module 2** when its cards land (`dev:` badges per device cover it; add a `module` badge).
- [ ] **Module 2 cards** as the lessons land: VLANs, trunks, EtherChannel, port security, SSH, CDP. Append to `cmdDrill.cards`; the deck test proves each answer.
- [ ] **Reverse cards.** Show a command or a slice of its output and ask what it does or what is wrong (multiple choice). Needs a small question bank per card.
- [ ] **Due cards on the title tile and in Night Watch.** The Lab tile could show "n commands due"; Night Watch could add two command cards to its five review cards.

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

## Large: engine gaps, grouped by the course module waiting on them

Colby's fidelity priorities: spanning tree, ACLs and NAT, services (DHCP relay, HSRP, NTP, syslog). IPv6 last.

- [ ] **Module 2 (2.14):** Rapid PVST+ state: root election, port roles and states, `show spanning-tree`. PortFast and BPDU guard already exist as errdisable triggers.
- [x] **Module 3:** shipped 2026-10-29 (10 lessons).
- [ ] **Lesson links:** Colby adds hand-picked YouTube videos per lesson (`links:[{t,u}]` on the lesson).
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
- [x] Command drill: 46 Module 1 cards answered in the real console, spaced repetition, Commands tab (2026-10-17)
- [x] Drill statistics: mastery tiers, weak spots, Start here recommendation, 14 badges, session summaries (2026-10-17)
- [x] Course Module 2, Network Access: 13 lessons (VLANs → port security) plus two stubs (2026-10-17)
