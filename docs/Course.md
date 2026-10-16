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
