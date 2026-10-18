---
title: Tickets
tags: [reference, content]
updated: 2026-10-15
---

# Tickets

Generated from the content pack on 2026-10-15. Objectives are CCNA 200-301 v1.1 numbers (see the map at the end).

## Ticket schema

A quest in `NetmancerContent.quests`:

| Field | Meaning |
| --- | --- |
| `id` `era` `topology` `tier` `sla` | Identity, content tier, which topology to build, difficulty 1–4, minutes for the time bonus |
| `flavor` `title` `reporter` `symptom` `brief` | Wizard name, plain title, who reported it, their words, the technician's notes |
| `xp` `obj` | XP per school (`fund` `access` `conn` `svc` `sec` `auto`), objective tags |
| `start` | Device the terminal opens on |
| `faults` `hosts` `errdisable` `removeLinks` `addLinks` `cond` `down` `dnsAdd` | How the fault is injected on top of the topology |
| `success` `constraints` `style` | Checks that must pass, must not break, and earn the style bonus. Types come from the `CHECKS` table |
| `hints` (3) `solution` `alt` `wrong` | Owl hints; the reference fix (also hint 4); alternative fixes; known-wrong fixes with `why` |
| `debrief` | `curse` (root cause), `concept`, `real` (why it happens in real life) |

Bad tickets (`badTickets`) add `kind` (vague, user, dup, team, mislead), `known` (what the ticket already says), `need` / `answer` / `partial` (vague), `verify` / `check` / `see` (proof commands), `guide` / `team` / `dupOf`, `cause`, `thanks`, and `real` (the fault a vague ticket unlocks).

## Topologies

| Id | Name | Devices | Used by |
| --- | --- | --- | --- |
| `ground` | The Ground Floor | ISP, R1, SW1, SRV-1, PC-RECEP, LAPTOP-7, PC-DANA, PC-NEW, PC-ACCT, PRN-1, THERMO-1 | Era 1, Night Watch |
| `closet` | The Rune Closet | ISP, R1 (router-on-a-stick), SW1, SW2 (Po1 LACP uplink), PC-ADMIN, SRV-1, PRN-2, PC-10-1, PC-20-1, PC-30-1, PHONE-5 + PC-5, NEWHIRE, PC-HR, PC-FRONT | Era 2 |
| `tower` | The Second Tower | ISP, R1 (HQ), SW1, PC-HQ, SRV-HQ, R2 (branch), SW3, PC-B10, SRV-B, PC-B20; fiber WAN 172.16.1.0/30, slow 4G backup 172.16.9.0/30 | Era 3 |

## Quests

| Id | Era | Tier | Objectives | Title | Start | The fault |
| --- | --- | --- | --- | --- | --- | --- |
| T-001 | 1 | 1 | 1.4, 1.10 | New laptop, no internet | LAPTOP-7 | SW1 g0/5 shutdown |
| T-002 | 1 | 1 | 1.10, 4.3 | Websites dead, chat app works | PC-DANA | PC has a retired static DNS server |
| T-003 | 1 | 1 | 1.6, 1.10 | New PC reaches the printer but not the internet | PC-NEW | Static gateway typo 10.10.1.1 |
| T-006 | 1 | 2 | 1.4 | Slow network at one desk | PC-ACCT | SW1 g0/8 hard-set 100/full (duplex mismatch) |
| T-007 | 1 | 2 | 1.10, 1.13 | Printer works on and off | PC-DANA | THERMO-1 uses the printer's IP (duplicate) |
| T-013 | 2 | 2 | 2.1 | New hire on the wrong network | NEWHIRE | SW2 g0/6 has no access VLAN (VLAN 1) |
| T-014 | 2 | 3 | 2.2 | VLAN 30 can't reach the printer | PC-30-1 | SW2 Po1 allowed list lacks 30 |
| T-015 | 2 | 3 | 2.1 | Phones work, PCs behind them don't | PC-5 | SW2 g0/5 data and voice VLANs swapped |
| T-016 | 2 | 3 | 2.2, 2.3 | CDP complains about native VLAN | PC-ADMIN | SW2 Po1 native VLAN 1 vs 99 |
| T-017 | 2 | 3 | 2.2 | New switch won't trunk | SW2 | Both ends dynamic auto, only g0/24 cabled |
| T-018 | 2 | 3 | 2.4 | Uplink bandwidth halved | SW1 | SW2 g0/24 moved to channel-group 2 mode on |
| T-019 | 2 | 2 | 2.5 | Port dead after desk switch plugged in | PC-HR | SW2 g0/7 err-disabled by BPDU guard |
| T-040 | 2 | 2 | 5.7 | Port shut down after hub plugged in | PC-FRONT | SW2 g0/9 err-disabled by port security |
| T-021 | 2 | 3 | 2.1, 3.1 | Inter-VLAN routing broken for one VLAN | PC-30-1 | R1 g0/0.30 tagged VLAN 31; must save config |
| T-022 | 2 | 2 | 2.8, 4.8 | Can't SSH to the new switch | PC-ADMIN | SW2 has no domain, keys, user or SSH transport |
| T-024 | 3 | 3 | 3.3 | Branch can't reach HQ | PC-B10 | R1 lost its routes to the branch |
| T-025 | 3 | 2 | 3.3 | Branch has no internet | PC-B10 | R2 has no default route |
| T-026 | 3 | 4 | 3.1, 3.2 | Traffic to one server takes the slow path | PC-HQ | Leftover /32 host route via 4G on R1 |
| T-027 | 3 | 4 | 3.3 | Branch traffic stuck on the backup link | PC-HQ | Floating static has AD 100, below OSPF's 110 |
| T-028 | 3 | 4 | 3.4 | OSPF neighbor never comes up | R1 | R2 g0/1 hello-interval 5 |
| T-030 | 3 | 3 | 3.4 | New LAN not in the routing tables | PC-HQ | R2 network statement with wildcard 0.0.0.0 |
| T-046 | 3 | 3 | 2.1, 3.1 | New VLAN has no gateway | PC-B20 | R2 has no g0/0.20 subinterface |

Era 3 OSPF tickets (T-027, T-028, T-030) first convert R1 and R2 from statics to OSPF with the shared `OSPF1` / `OSPF2` line lists, then break something.

## Night Watch templates (`watch`)

| Id | Objective | Title | Variants |
| --- | --- | --- | --- |
| H1 | 1.4 | {{host}} lost its network | 4 hosts: port shutdown on SW1 |
| H2 | 1.10 | {{host}} can't resolve names | 4 hosts: a bad static DNS server |
| H3 | 1.4 | {{host}} is slow | 3 hosts: duplex mismatch |
| H4 | 2.5 | {{host}} port err-disabled | 3 hosts: BPDU guard |
| H5 | 1.6 | {{host}} can't leave the subnet | 3 hosts: wrong static gateway |

`watchFor` picks template `day % 5` and variant `floor(day / 5)`. On about 4 nights in 10, `nightHex` serves a bad ticket instead.

## Bad tickets (`badTickets`)

| Id | Era | Kind | Objectives | Title | Right move |
| --- | --- | --- | --- | --- | --- |
| B-101 | 1 | vague | 1.10, 4.3 | internet broken | Ask for device + error; unlocks a public-DNS fault on PC-RECEP |
| B-102 | 1 | user | 1.10 | Internet down at home | Verify, then guide: VPN (Wardgate) not connected |
| B-103 | 1 | user | 1.4, 1.10 | Whole office internet down!! | Verify, then guide: loose cable |
| B-104 | 1 | user | 1.10 | Printer broken, network down? | Verify, then guide: printer out of paper |
| B-105 | 1 | dup | 1.4 | Hot desk 5 laptop has no internet | Merge into T-001 |
| B-201 | 2 | user | 1.10, 1.11 | Wi-Fi works, internal sites don't | Guide: on SPIRE-GUEST, join SPIRE-CORP |
| B-202 | 2 | user | 1.10, 5.3 | Network won't let me sign in | Guide: Caps Lock |
| B-203 | 2 | user | 1.10, 1.11 | Laptop says No internet | Guide: airplane mode |
| B-204 | 2 | dup | 2.2 | Studio can't print (again) | Merge into T-014 |
| B-205 | 2 | team | 1.10 | Network is eating my timesheet | Reassign to Business apps (HTTP 500) |
| B-206 | 2 | mislead | 2.1 | I think my PC has a virus | Real fault: VLAN 30 deleted from SW2 |
| B-301 | 3 | user | 1.10 | HQ file server is DOWN | Guide: VPN session expired |
| B-302 | 3 | user | 1.10, 3.1 | Router broken: supplier portal won't load | Guide: external site down |
| B-303 | 3 | vague | 4.6, 3.1 | lab pc not working | Ask; unlocks R2 g0/0.20 re-addressed (no DHCP) |
| B-304 | 3 | mislead | 1.10, 3.1 | DNS is broken at the branch | Real fault: PC-B10 wrong static gateway |

Rate: about one bad ticket per four real tickets resolved (`badVisible`).

## Objectives and schools

| Objective | Name | Objective | Name |
| --- | --- | --- | --- |
| 1.4 | Interface and cable issues | 2.8 | Device management access |
| 1.6 | IPv4 addressing and subnetting | 3.1 | Routing table components |
| 1.10 | Verify client IP parameters | 3.2 | Router forwarding decisions |
| 1.11 | Wireless principles | 3.3 | IPv4 static routing |
| 1.13 | Switching concepts | 3.4 | Single-area OSPFv2 |
| 2.1 | VLANs across switches | 4.3 | DHCP and DNS |
| 2.2 | Interswitch connectivity (trunks) | 4.6 | DHCP client and relay |
| 2.3 | CDP and LLDP | 4.8 | Remote access with SSH |
| 2.4 | EtherChannel (LACP) | 5.3 | Local passwords and device access |
| 2.5 | Rapid PVST+ | 5.7 | Layer 2 security |

Schools (XP buckets): `fund` Divination 1.0, `access` Binding 2.0, `conn` Wayfinding 3.0, `svc` Enchantment 4.0, `sec` Abjuration 5.0, `auto` Artifice 6.0.

Ranks: Apprentice (Helpdesk Tech I) → Acolyte (500 fund XP + T-003) → Adept (800 access + 500 fund + T-014, T-017) → Magus (1,000 conn + T-028, T-030) → Wizard (Era 4, locked).

## Adding a ticket

1. Add it to `quests` with every field above. Keep `obj` to objectives that exist in `objectives`, or add the objective there too.
2. Give it at least one `wrong` case; the self-test proves wrong fixes fail.
3. Add a `questCards` entry (two cards) and an `artifacts` entry.
4. Run `#selftest`: it builds the ticket, checks it fails before the fix, passes after `solution` and each `alt`, fails each `wrong`, and survives a save/load round trip.

## Guided walkthroughs

Academy tickets with a hand-written guide (`content.guides`, schema: `facts[{q, why}]`, `steps[{dev, cmd, show, look, why} | {dev, lines, check, why}]`, `done`). Every other ticket gets an automatic guide from its hints and solution.

| Ticket | Facts | Steps |
| --- | --- | --- |
| T-001 New laptop, no internet | 3 | 5 |
| T-002 Websites dead, chat app works | 4 | 4 |
| T-003 New PC reaches the printer but not the internet | 4 | 4 |
| T-006 Slow network at one desk | 4 | 4 |
| T-007 Printer works on and off | 5 | 6 |
