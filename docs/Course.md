---
title: Course
tags: [reference, content]
updated: 2026-10-15
---

# Course

The CCNA course in Lab mode: lessons that build one network step by step. The tables are generated from `course` in the content pack; regenerate with `node .bak/docsH.js course-only` after changing lessons.

## Lab addressing plan

Domain `lab.local`. LAN A `192.168.10.0/24` (R1 .1, SRV1 .5, DHCP from .10). LAN B `192.168.20.0/24` (R1 .1, DHCP from .10). MGMT `192.168.99.0/24` (Module 2). Module 1 builds SW1 – R1 – SW2 with PC1, PC2, SRV1 on LAN A and PC3 on LAN B.

## Modules

| Id | Title | Lessons |
| --- | --- | --- |
| m1 | 1.0 Network Fundamentals | 15 |
| m2 | 2.0 Network Access (coming) | 0 |
| m3 | 3.0 IP Connectivity (coming) | 0 |
| m4 | 4.0 IP Services (coming) | 0 |
| m5 | 5.0 Security Fundamentals (coming) | 0 |
| m6 | 6.0 Automation and Programmability (coming) | 0 |

## Lessons

| Id | Objectives | Title | Goals | Setup |
| --- | --- | --- | --- | --- |
| 1.01 | 1.1, 1.2 | Your first switch | has_device, ran |  |
| 1.02 | 1.3, 1.4 | Plug in a PC with an RJ45 patch cable | has_device, has_link, iface_up |  |
| 1.03 | 1.1, 2.8, 5.3 | Console cable, hostname, save | has_link, hostname, saved |  |
| 1.04 | 1.4 | Force a duplex mismatch | speed_duplex, ran |  |
| 1.05 | 1.4 | Fix the mismatch | speed_duplex, link_full |  |
| 1.06 | 1.6, 1.7, 1.10 | A static IPv4 address | host_ip, host_net, ran |  |
| 1.07 | 1.13, 1.10 | Second PC: ping, ARP and the MAC address table | has_device, has_link, reach, ran ×2 |  |
| 1.08 | 1.6 | Same wire, different subnet | host_net, iface_up, not_reach |  |
| 1.09 | 1.1, 1.6 | A router becomes the gateway | has_device, has_link, iface_ip, iface_up, hostname, host_ip, reach ×2 |  |
| 1.10 | 1.6, 3.1 | A second LAN behind the router | has_device ×2, has_link ×2, iface_ip, reach, ran ×2 |  |
| 1.11 | 4.3, 1.10 | DHCP from the router | lease ×2, host_net, ran |  |
| 1.12 | 1.4 | Admin down: the switch side of "no link" | ran, iface_up, lease |  |
| 1.13 | 4.3, 1.10 | A server and DNS | has_device, host_ip, resolve, ran ×2 |  |
| 1.14 | 1.5 | TCP and UDP: what is listening | reach, ran ×2 |  |
| 1.15 | 1.10, 4.3 | Broken client: your first fault | resolve, reach, lease | yes |

## Lesson schema

```
{id, module, obj[], title, brief, requires[], setup?[steps], goals[checks], constraints?[checks], hints[], solution[steps], kind?:"stub", note?}
```

- `brief` is plain text: a blank line starts a paragraph, a line starting with `- ` is a list item, backticks mark code. Rendered by `briefHtml`.
- Steps are lab actions `{lab:"add"|"link"|"unlink"|"remove"|"move"|"rename"|"dns"|"svc"|"host", ...}` or CLI `{dev, lines[]}`. `C.lab.apply(net, steps)` replays them; the self-test replays every lesson's `solution` in order, so a solution must pass its own goals.
- `setup` is applied once when the lesson first opens (tracked in `S.course.setupDone`). Use it to inject a fault into the lab.
- Goals are `CHECKS` entries. `ran {dev, re, label}` matches a command the player typed on that device (`net.cmdlog`). Give a `label` to any goal whose automatic label would be unclear.
- `requires` lists earlier lesson ids; the Course tab shows lessons in pack order.

## Adding a lesson

1. Append it to `course.lessons` in `NetmancerContent` (keep the module order). Objectives must exist in `objectives`.
2. Write the `solution` so that replaying every earlier solution and then this one passes the goals. A CLI step on a switch starts in user mode, so begin with `enable`.
3. Run `#selftest`: the engine suite replays the course and names the first lesson that breaks.
4. Regenerate this page.

## Objectives referenced

- 1.1 Network components
- 1.10 Verify client IP parameters
- 1.13 Switching concepts
- 1.2 Network topology architectures
- 1.3 Physical interfaces and cabling
- 1.4 Interface and cable issues
- 1.5 TCP and UDP
- 1.6 IPv4 addressing and subnetting
- 1.7 Private IPv4 addressing
- 2.8 Device management access
- 3.1 Routing table components
- 4.3 DHCP and DNS
- 5.3 Local passwords and device access

## Command deck

The Commands tab drills these cards in the real console (see [Decisions](Decisions.md)). Generated from `cmdDrill.cards`; regenerate with `node .bak/docsJ.js course-only`.

Card schema: `{id, obj[], dev, start, pre?[], where?, task, accept[], answer, note?, check?}`. `start` is user, priv, config (IOS), cmd, ps (PC) or sh (server); `pre` lines run after that; `accept` patterns use `abc[def]` for abbreviations, `*` for any token and `{re}` for a raw regex token.

| Id | Device | Objectives | Task | Answer |
| --- | --- | --- | --- | --- |
| c01 | SW1 | 2.8 | Enter privileged EXEC mode. | `enable` |
| c02 | SW1 | 2.8 | Enter global configuration mode. | `configure terminal` |
| c03 | SW1 | 2.8 | Rename the switch to ACCESS1. | `hostname ACCESS1` |
| c04 | SW1 | 2.8 | Go straight back to privileged EXEC from here. | `end` |
| c05 | SW1 | 2.8 | Save the running configuration so it survives a reload. | `write memory` |
| c06 | SW1 | 1.4 | List every port with its status, VLAN, duplex and speed. | `show interfaces status` |
| c07 | SW1 | 1.4 | Show the detail for Gi0/1: line status, duplex, speed and error counters. | `show interfaces GigabitEthernet0/1` |
| c08 | SW1 | 1.13 | Show which MAC address was learned on which port. | `show mac address-table` |
| c09 | SW1 | 2.8 | Show the running configuration. | `show running-config` |
| c10 | SW1 | 2.8 | Show the configuration the switch will boot with. | `show startup-config` |
| c11 | SW1 | 1.10 | Show every interface with its address and status in one table. | `show ip interface brief` |
| c12 | SW1 | 1.1 | Show the software version, uptime and model. | `show version` |
| c13 | SW1 | 2.8 | Enter interface configuration for Gi0/2. | `interface GigabitEthernet0/2` |
| c14 | SW1 | 1.4 | Force this port to 100 Mb/s. | `speed 100` |
| c15 | SW1 | 1.4 | Force full duplex on this port. | `duplex full` |
| c16 | SW1 | 1.4 | Put speed and duplex back to autonegotiation (two commands). | `speed auto / duplex auto` |
| c17 | SW1 | 1.4 | Administratively shut this port down. | `shutdown` |
| c18 | SW1 | 1.4 | Bring the port back up. | `no shutdown` |
| c19 | SW1 | 2.8 | Label this port "SRV1 uplink". | `description SRV1 uplink` |
| c20 | SW1 | 2.8 | Give the switch a management address 192.168.10.2/24 on VLAN 1 and enable the interface (three commands). | `interface vlan 1 / ip address 192.168.10.2 255.255.255.0 / no shutdown` |
| c21 | SW1 | 2.8 | Set the default gateway so the switch can be reached from other subnets. | `ip default-gateway 192.168.10.1` |
| c22 | SW1 | 1.10 | Ping the router at 192.168.10.1 from the switch. | `ping 192.168.10.1` |
| c23 | R1 | 1.6 | Give Gi0/1 the address 192.168.20.1/24 and enable it (three commands). | `interface GigabitEthernet0/1 / ip address 192.168.20.1 255.255.255.0 / no shutdown` |
| c24 | R1 | 3.1 | Show the routing table. | `show ip route` |
| c25 | R1 | 4.3 | Show the DHCP leases the router has handed out. | `show ip dhcp binding` |
| c26 | R1 | 4.3 | Keep 192.168.20.1 through 192.168.20.9 out of the DHCP range. | `ip dhcp excluded-address 192.168.20.1 192.168.20.9` |
| c27 | R1 | 4.3 | Create a DHCP pool named LAN20 for 192.168.20.0/24 whose clients use 192.168.20.1 as their gateway (three commands). | `ip dhcp pool LAN20 / network 192.168.20.0 255.255.255.0 / default-router 192.168.20.1` |
| c28 | R1 | 4.3 | Hand clients 192.168.10.5 as their DNS server. | `dns-server 192.168.10.5` |
| c29 | R1 | 1.10 | Show the ARP cache on the router. | `show ip arp` |
| c30 | R1 | 1.10 | Show the router's interfaces with address and status in one table. | `show ip interface brief` |
| c31 | R1 | 2.8 | Save the configuration. | `copy running-config startup-config ⏎` |
| c32 | PC1 | 1.10 | Show the PC's IPv4 address, mask and default gateway. | `ipconfig` |
| c33 | PC1 | 1.10 | Show the full picture: MAC address, DHCP server, lease times and DNS servers. | `ipconfig /all` |
| c34 | PC1 | 4.3 | Ask the DHCP server for a fresh lease. | `ipconfig /renew` |
| c35 | PC1 | 4.3 | Give the lease back to the server. | `ipconfig /release` |
| c36 | PC1 | 1.10 | Test reachability to the gateway 192.168.10.1. | `ping 192.168.10.1` |
| c37 | PC1 | 1.10 | Show the hop-by-hop path to 192.168.10.5. | `tracert 192.168.10.5` |
| c38 | PC1 | 1.13 | Show the ARP cache: the MAC address learned for each neighbour. | `arp -a` |
| c39 | PC1 | 1.6 | Set a static address 192.168.10.50/24 with gateway 192.168.10.1 on the Ethernet adapter. | `netsh interface ip set address "Ethernet" static 192.168.10.50 255.255.255.0 192.168.10.1` |
| c40 | PC2 | 4.3 | Put the adapter back on DHCP. | `netsh interface ip set address "Ethernet" dhcp` |
| c41 | PC2 | 4.3 | Resolve srv1.lab.local and see which server answered. | `nslookup srv1.lab.local` |
| c42 | PC2 | 4.3 | Point this PC's DNS at 192.168.10.5 statically. | `netsh interface ip set dns "Ethernet" static 192.168.10.5` |
| c43 | PC1 | 1.5 | Test whether TCP port 80 on 192.168.10.5 accepts a connection. | `Test-NetConnection 192.168.10.5 -Port 80` |
| c44 | SRV1 | 1.5 | List the listening TCP and UDP sockets with the program behind each. | `ss -tulpn` |
| c45 | SRV1 | 1.10 | Show the server's interfaces and addresses. | `ip address show` |
| c46 | SRV1 | 4.3 | Query the DNS server 192.168.10.5 for srv1.lab.local. | `dig @192.168.10.5 srv1.lab.local` |

## Badges

Earned once in the command drill; tests live in `DRILL_BADGES` (core), names here are from `cmdDrill.badges`.

| Id | Name | How |
| --- | --- | --- |
| first | First blood | Your first correct answer. |
| clean | Clean sweep | A session of eight or more with every card right first time. |
| run10 | Ten in a row | Ten first-try answers in a row. |
| fluent5 | Fast hands | Five cards fluent: three first-try answers each, all quick. |
| dev:SW1 | Switch hand | Every switch card known. |
| dev:R1 | Router hand | Every router card known. |
| dev:PC | Desktop support | Every PC card known. |
| dev:SRV1 | Server room | Every server card known. |
| deck | Module 1 known | Every card in the deck known. |
| deckfluent | Module 1 fluent | Every card in the deck fluent. |
| hundred | Hundred club | One hundred correct answers. |
| comeback | Comeback | A session after a week or more away. |
| scholar | Scholar | Five times: revealed a card, then got it first time on its next showing. |
| explorer | Explorer | Used ? or Tab twenty-five times during cards. |
