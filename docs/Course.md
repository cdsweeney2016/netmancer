---
title: Course
tags: [reference, content]
updated: 2026-10-17
---

# Course

The CCNA course in Lab mode: lessons that build one network step by step. The tables are generated from the content pack; regenerate with `node .bak/docsCourse.js` after changing lessons, cards or badges.

## Lab addressing plan

Domain `lab.local`. Module 1: LAN A `192.168.10.0/24` (R1 .1, SRV1 .5, DHCP from .10), LAN B `192.168.20.0/24` (R1 .1, PC3). Module 2 turns R1 into router-on-a-stick: VLAN 10 USERS 192.168.10.0/24, VLAN 20 OFFICE2 192.168.20.0/24 (pool LAN20), VLAN 30 VOICE 192.168.30.0/24 (pool VOICE), VLAN 99 MGMT 192.168.99.0/24 (R1 .1, SW1 .2, SW2 .3); SW1 Gi0/24 trunk to R1, Po1 (Gi0/22-23 to SW2 Gi0/23-24) between the switches; SSH user admin / enable secret Lab123! on SW1.

## Modules

| Id | Title | Lessons |
| --- | --- | --- |
| m1 | 1.0 Network Fundamentals | 15 |
| m2 | 2.0 Network Access | 15 |
| m3 | 3.0 IP Connectivity | 10 |
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
| 2.01 | 2.1 | VLANs: one switch, several broadcast domains | vlan_exists ×3, ran |  |
| 2.02 | 2.1 | Access ports: put the users in VLAN 10 | port_vlan ×3 |  |
| 2.03 | 2.2, 1.6 | Router-on-a-stick: one cable, every VLAN | trunk_up, iface_ip ×2, iface_down, lease, reach |  |
| 2.04 | 2.2, 2.1, 4.3 | A trunk to SW2 | has_link, trunk_up ×2, vlan_exists, port_vlan, lease, reach |  |
| 2.05 | 2.2 | Allowed list and native VLAN | native ×2, not_all ×2, vlan_exists · keeps: reach |  |
| 2.06 | 2.3 | CDP: who is on the other end | ran ×2, port_desc ×3 |  |
| 2.07 | 2.1, 4.3 | A voice VLAN for an IP phone | has_device, has_link, voice_vlan, port_vlan, lease |  |
| 2.08 | 2.8, 2.1 | A management address for each switch | iface_ip, svi_ip ×2, default_gw ×2, reach ×2 |  |
| 2.09 | 4.8, 5.3, 2.8 | SSH to the switch | ssh_ok, ssh_only, running_has, saved, ran |  |
| 2.10 | 5.3, 2.8 | Console password, banner, encrypted passwords | running_has ×3, saved |  |
| 2.11 | 2.4 | EtherChannel: two cables, one link | has_link, bundle ×2, trunk_up · keeps: reach |  |
| 2.12 | 2.5, 5.7 | PortFast and BPDU guard: a rogue switch | bpduguard ×2, has_device, ran | yes |
| 2.13 | 5.7 | Port security: one MAC per desk | psec, running_has, saved, ran |  |
| 2.14 | 2.5 | Rapid PVST+: who blocks and why (stub) |  |  |
| 2.15 | 2.6 | Wireless: an access point on the trunk (stub) |  |  |
| 3.01 | 3.1, 3.2 | Reading the routing table | ran ×2 |  |
| 3.02 | 3.1 | A second router: the WAN link | has_device, hostname, has_link, iface_ip ×2, iface_up ×2, ran |  |
| 3.03 | 3.1, 3.2 | The branch LAN: connected is not enough | has_device ×2, hostname, has_link ×2, host_ip, default_gw, iface_ip, reach, not_reach |  |
| 3.04 | 3.3 | Static routes: tell each router about the other side | route_type ×3, reach ×2, ran |  |
| 3.05 | 3.3, 3.2 | A default route for the branch | route_present, no_static ×4, reach |  |
| 3.06 | 3.4 | OSPF: let the routers tell each other | ospf_nbr ×2, route_type ×2, no_static, running_has ×2, reach, ran |  |
| 3.07 | 3.4 | Passive interfaces and OSPF verification | running_has ×5, ospf_nbr, ran ×2 |  |
| 3.08 | 3.3 | A floating static route as the backup path | has_link, iface_ip ×2, route_present ×2, route_type, failover |  |
| 3.09 | 3.4 | Troubleshoot OSPF: the adjacency that will not form | ospf_hello, ospf_nbr, route_type, ran · keeps: ospf_hello | yes |
| 3.10 | 3.5 | First-hop redundancy: two gateways, one address (stub) |  |  |

## Lesson schema

```
{id, module, obj[], title, brief, requires[], setup?[steps], goals[checks], constraints?[checks], hints[], solution[steps], kind?:"stub", note?, links?[{t,u}]}
```

- `brief` is plain text: a blank line starts a paragraph, a line starting with `- ` is a list item, backticks mark code. Rendered by `briefHtml`.
- Steps are lab actions `{lab:"add"|"link"|"unlink"|"remove"|"move"|"rename"|"dns"|"svc"|"host", ...}` or CLI `{dev, lines[]}`. `C.lab.apply(net, steps)` replays them; the self-test replays every lesson's `solution` in order, so a solution must pass its own goals. A CLI step starts a fresh shell in user mode: begin with `enable` (and the enable secret once one is set).
- `setup` is applied once when the lesson first opens (tracked in `S.course.setupDone`). Use it to inject a fault or a rogue device.
- Goals are `CHECKS` entries. `ran {dev, re, label}` matches a command the player typed on that device (`net.cmdlog`). A failing `reach` goal carries a `why` the lesson panel shows.
- `requires` lists earlier lesson ids; the lesson panel warns when they are not done.

## Adding a lesson

1. Append it to `course.lessons` in `NetmancerContent` (keep the module order). Objectives must exist in `objectives`.
2. Write the `solution` so that replaying every earlier solution and then this one passes the goals.
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
- 2.1 VLANs across switches
- 2.2 Interswitch connectivity (trunks)
- 2.3 CDP and LLDP
- 2.4 EtherChannel (LACP)
- 2.5 Rapid PVST+
- 2.6 Wireless architectures
- 2.8 Device management access
- 3.1 Routing table components
- 3.2 Router forwarding decisions
- 3.3 IPv4 static routing
- 3.4 Single-area OSPFv2
- 3.5 First hop redundancy
- 4.3 DHCP and DNS
- 4.8 Remote access with SSH
- 5.3 Local passwords and device access
- 5.7 Layer 2 security

## References

Each lesson shows a Learn more list: the links for its objectives from `course.links` (vendor-neutral: Wikipedia, RFCs, the exam blueprint under `*`), plus any `links[{t,u}]` of its own. Hand-picked videos are Colby's to add later.

| Objective | Links |
| --- | --- |
| * | [CCNA 200-301 exam topics (Cisco Learning Network)](https://learningnetwork.cisco.com/s/ccna-exam-topics) |
| 1.1 Network components | [Router (Wikipedia)](https://en.wikipedia.org/wiki/Router_(computing)), [Network switch (Wikipedia)](https://en.wikipedia.org/wiki/Network_switch), [Ethernet frame (Wikipedia)](https://en.wikipedia.org/wiki/Ethernet_frame) |
| 1.10 Verify client IP parameters | [ipconfig (Wikipedia)](https://en.wikipedia.org/wiki/Ipconfig), [Link-local address and APIPA (Wikipedia)](https://en.wikipedia.org/wiki/Link-local_address), [RFC 3927: Dynamic Configuration of IPv4 Link-Local Addresses](https://www.rfc-editor.org/rfc/rfc3927) |
| 1.11 Wireless principles | [Wireless LAN (Wikipedia)](https://en.wikipedia.org/wiki/Wireless_LAN), [IEEE 802.11 (Wikipedia)](https://en.wikipedia.org/wiki/IEEE_802.11) |
| 1.13 Switching concepts | [MAC address (Wikipedia)](https://en.wikipedia.org/wiki/MAC_address), [Forwarding information base, the MAC table (Wikipedia)](https://en.wikipedia.org/wiki/Forwarding_information_base), [Address Resolution Protocol (Wikipedia)](https://en.wikipedia.org/wiki/Address_Resolution_Protocol), [RFC 826: ARP](https://www.rfc-editor.org/rfc/rfc826) |
| 1.2 Network topology architectures | [Network topology (Wikipedia)](https://en.wikipedia.org/wiki/Network_topology), [Local area network (Wikipedia)](https://en.wikipedia.org/wiki/Local_area_network) |
| 1.3 Physical interfaces and cabling | [Ethernet over twisted pair (Wikipedia)](https://en.wikipedia.org/wiki/Ethernet_over_twisted_pair), [Medium-dependent interface, MDI-X and crossover (Wikipedia)](https://en.wikipedia.org/wiki/Medium-dependent_interface), [Small form-factor pluggable (Wikipedia)](https://en.wikipedia.org/wiki/Small_Form-factor_Pluggable) |
| 1.4 Interface and cable issues | [Autonegotiation (Wikipedia)](https://en.wikipedia.org/wiki/Autonegotiation), [Duplex mismatch (Wikipedia)](https://en.wikipedia.org/wiki/Duplex_mismatch) |
| 1.5 TCP and UDP | [Transmission Control Protocol (Wikipedia)](https://en.wikipedia.org/wiki/Transmission_Control_Protocol), [User Datagram Protocol (Wikipedia)](https://en.wikipedia.org/wiki/User_Datagram_Protocol), [RFC 9293: TCP](https://www.rfc-editor.org/rfc/rfc9293), [RFC 768: UDP](https://www.rfc-editor.org/rfc/rfc768) |
| 1.6 IPv4 addressing and subnetting | [Subnet (Wikipedia)](https://en.wikipedia.org/wiki/Subnet), [Classless Inter-Domain Routing (Wikipedia)](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing), [RFC 4632: CIDR](https://www.rfc-editor.org/rfc/rfc4632) |
| 1.7 Private IPv4 addressing | [Private network (Wikipedia)](https://en.wikipedia.org/wiki/Private_network), [RFC 1918: Address Allocation for Private Internets](https://www.rfc-editor.org/rfc/rfc1918) |
| 2.1 VLANs across switches | [VLAN (Wikipedia)](https://en.wikipedia.org/wiki/VLAN), [Broadcast domain (Wikipedia)](https://en.wikipedia.org/wiki/Broadcast_domain) |
| 2.2 Interswitch connectivity (trunks) | [IEEE 802.1Q (Wikipedia)](https://en.wikipedia.org/wiki/IEEE_802.1Q), [Router on a stick (Wikipedia)](https://en.wikipedia.org/wiki/Router_on_a_stick), [Dynamic Trunking Protocol (Wikipedia)](https://en.wikipedia.org/wiki/Dynamic_Trunking_Protocol) |
| 2.3 CDP and LLDP | [Cisco Discovery Protocol (Wikipedia)](https://en.wikipedia.org/wiki/Cisco_Discovery_Protocol), [Link Layer Discovery Protocol (Wikipedia)](https://en.wikipedia.org/wiki/Link_Layer_Discovery_Protocol) |
| 2.4 EtherChannel (LACP) | [Link aggregation and LACP (Wikipedia)](https://en.wikipedia.org/wiki/Link_aggregation), [EtherChannel (Wikipedia)](https://en.wikipedia.org/wiki/EtherChannel) |
| 2.5 Rapid PVST+ | [Spanning Tree Protocol, incl. RSTP and PVST (Wikipedia)](https://en.wikipedia.org/wiki/Spanning_Tree_Protocol), [IEEE 802.1D (Wikipedia)](https://en.wikipedia.org/wiki/IEEE_802.1D) |
| 2.6 Wireless architectures | [Wireless access point (Wikipedia)](https://en.wikipedia.org/wiki/Wireless_access_point), [Wireless LAN controller (Wikipedia)](https://en.wikipedia.org/wiki/Wireless_LAN_controller), [RFC 5415: CAPWAP](https://www.rfc-editor.org/rfc/rfc5415) |
| 2.8 Device management access | [Out-of-band and in-band management (Wikipedia)](https://en.wikipedia.org/wiki/Out-of-band_management), [Default gateway (Wikipedia)](https://en.wikipedia.org/wiki/Default_gateway) |
| 3.1 Routing table components | [Routing table (Wikipedia)](https://en.wikipedia.org/wiki/Routing_table), [Administrative distance (Wikipedia)](https://en.wikipedia.org/wiki/Administrative_distance), [Metric (Wikipedia)](https://en.wikipedia.org/wiki/Metrics_(networking)) |
| 3.2 Router forwarding decisions | [Longest prefix match (Wikipedia)](https://en.wikipedia.org/wiki/Longest_prefix_match), [IP routing (Wikipedia)](https://en.wikipedia.org/wiki/IP_routing), [RFC 1812: Requirements for IP Version 4 Routers](https://www.rfc-editor.org/rfc/rfc1812.html) |
| 3.3 IPv4 static routing | [Static routing (Wikipedia)](https://en.wikipedia.org/wiki/Static_routing), [Default route (Wikipedia)](https://en.wikipedia.org/wiki/Default_route) |
| 3.4 Single-area OSPFv2 | [Open Shortest Path First (Wikipedia)](https://en.wikipedia.org/wiki/Open_Shortest_Path_First), [RFC 2328: OSPF Version 2](https://www.rfc-editor.org/rfc/rfc2328), [Link-state routing protocol (Wikipedia)](https://en.wikipedia.org/wiki/Link-state_routing_protocol) |
| 3.5 First hop redundancy | [First-hop redundancy protocol (Wikipedia)](https://en.wikipedia.org/wiki/First-hop_redundancy_protocol), [Hot Standby Router Protocol (Wikipedia)](https://en.wikipedia.org/wiki/Hot_Standby_Router_Protocol), [RFC 2281: HSRP](https://www.rfc-editor.org/rfc/rfc2281.html), [RFC 5798: VRRP](https://www.rfc-editor.org/rfc/rfc5798) |
| 4.3 DHCP and DNS | [Dynamic Host Configuration Protocol (Wikipedia)](https://en.wikipedia.org/wiki/Dynamic_Host_Configuration_Protocol), [RFC 2131: DHCP](https://www.rfc-editor.org/rfc/rfc2131.html), [Domain Name System (Wikipedia)](https://en.wikipedia.org/wiki/Domain_Name_System), [RFC 1034: DNS concepts](https://www.rfc-editor.org/rfc/rfc1034) |
| 4.6 DHCP client and relay | [DHCP relay agent (Wikipedia, in the DHCP article)](https://en.wikipedia.org/wiki/Dynamic_Host_Configuration_Protocol#Relaying), [RFC 3046: DHCP Relay Agent Information Option](https://www.rfc-editor.org/rfc/rfc3046) |
| 4.8 Remote access with SSH | [Secure Shell (Wikipedia)](https://en.wikipedia.org/wiki/Secure_Shell), [RFC 4253: SSH Transport Layer Protocol](https://www.rfc-editor.org/rfc/rfc4253), [Telnet (Wikipedia)](https://en.wikipedia.org/wiki/Telnet) |
| 5.3 Local passwords and device access | [Password strength (Wikipedia)](https://en.wikipedia.org/wiki/Password_strength), [Authentication, authorization and accounting (Wikipedia)](https://en.wikipedia.org/wiki/AAA_(computer_security)) |
| 5.7 Layer 2 security | [Port security (Wikipedia)](https://en.wikipedia.org/wiki/Port_security), [Spanning Tree Protocol: BPDU guard and PortFast (Wikipedia)](https://en.wikipedia.org/wiki/Spanning_Tree_Protocol), [MAC flooding (Wikipedia)](https://en.wikipedia.org/wiki/MAC_flooding) |

## Command deck

The Commands tab drills these cards in the real console (see [Decisions](Decisions.md)). Card schema: `{id, obj[], dev, start, pre?[], where?, task, accept[], answer, note?, why?, check?}`. `start` is user, priv, config (IOS), cmd, ps (PC) or sh (server); `pre` lines run after that; `accept` patterns use `abc[def]` for abbreviations, `*` for any token and `{re}` for a raw regex token; `why` explains the answer in networking terms.

| Id | Device | Objectives | Task | Answer |
| --- | --- | --- | --- | --- |
| c01 | SW1 | 2.8 | We have a switch to look at and the prompt ends in >. Get to privileged EXEC from the CLI. | `enable` |
| c02 | SW1 | 2.8 | We have a change to make on this switch. Enter global configuration mode from the CLI. | `configure terminal` |
| c03 | SW1 | 2.8 | We have a switch still called Switch; the standard says it should be ACCESS1. Rename it from the CLI. | `hostname ACCESS1` |
| c04 | SW1 | 2.8 | We have finished editing Gi0/4 and need the privileged prompt back. Get straight back to privileged EXEC from the CLI. | `end` |
| c05 | SW1 | 2.8 | We have changes on this switch that would vanish on a reload. Save the running configuration from the CLI. | `write memory` |
| c06 | SW1 | 1.4 | We have a user saying their port is dead. Grab the status, VLAN, duplex and speed of every port from the CLI. | `show interfaces status` |
| c07 | SW1 | 1.4 | We have slow transfers on the PC behind Gi0/1 and suspect a duplex mismatch. Grab the detail and error counters for Gi0/1 from the CLI. | `show interfaces GigabitEthernet0/1` |
| c08 | SW1 | 1.13 | We have a PC that nobody can find on the switch. Grab the MAC address table from the CLI. | `show mac address-table` |
| c09 | SW1 | 2.8 | We have a switch configured by someone else. Grab the running configuration from the CLI. | `show running-config` |
| c10 | SW1 | 2.8 | We have a switch that may boot with an older configuration. Grab the startup configuration from the CLI. | `show startup-config` |
| c11 | SW1 | 1.10 | We have a switch and need its interface addresses and states at a glance. Grab the one-table interface summary from the CLI. | `show ip interface brief` |
| c12 | SW1 | 1.1 | We have an audit asking for the software version, uptime and model. Grab them from the CLI. | `show version` |
| c13 | SW1 | 2.8 | We have a change to make on Gi0/2. Enter its interface configuration from the CLI. | `interface GigabitEthernet0/2` |
| c14 | SW1 | 1.4 | We have a legacy device on Gi0/1 that only runs at 100 Mb/s. Force this port to 100 Mb/s from the CLI. | `speed 100` |
| c15 | SW1 | 1.4 | We have an old device on Gi0/1 that cannot negotiate duplex. Force full duplex on this port from the CLI. | `duplex full` |
| c16 | SW1 | 1.4 | We have Gi0/1 forced to 100/full and the device on it has been replaced. Put speed and duplex back to autonegotiation from the CLI (two commands). | `speed auto / duplex auto` |
| c17 | SW1 | 1.4 | We have a rogue device on Gi0/2. Shut the port down from the CLI. | `shutdown` |
| c18 | SW1 | 1.4 | We have Gi0/2 shut down and the rogue device is gone. Bring the port back up from the CLI. | `no shutdown` |
| c19 | SW1 | 2.8 | We have no idea what plugs into Gi0/3, and it is the server. Label this port SRV1 uplink from the CLI. | `description SRV1 uplink` |
| c20 | SW1 | 2.8 | We have a switch we cannot SSH to because it has no address. Give it 192.168.10.2/24 on VLAN 1 and enable the interface from the CLI (three commands). | `interface vlan 1 / ip address 192.168.10.2 255.255.255.0 / no shutdown` |
| c21 | SW1 | 2.8 | We have a switch that answers on its own subnet but not from the office next door. Set its default gateway to 192.168.10.1 from the CLI. | `ip default-gateway 192.168.10.1` |
| c22 | SW1 | 1.10 | We have given the switch an address and want to prove it reaches the router. Ping 192.168.10.1 from the CLI. | `ping 192.168.10.1` |
| c23 | R1 | 1.6 | We have a new LAN that needs Gi0/1 as its gateway, 192.168.20.1/24. Address and enable the interface from the CLI (three commands). | `interface GigabitEthernet0/1 / ip address 192.168.20.1 255.255.255.0 / no shutdown` |
| c24 | R1 | 3.1 | We have packets going nowhere and need to see what the router knows. Grab the routing table from the CLI. | `show ip route` |
| c25 | R1 | 4.3 | We have a PC that says it got no address. Grab the DHCP leases the router has handed out from the CLI. | `show ip dhcp binding` |
| c26 | R1 | 4.3 | We have gear with fixed addresses 192.168.20.1 to .9 on the new LAN. Keep them out of the DHCP range from the CLI. | `ip dhcp excluded-address 192.168.20.1 192.168.20.9` |
| c27 | R1 | 4.3 | We have a new LAN 192.168.20.0/24 with no DHCP. Create pool LAN20 with 192.168.20.1 as the gateway from the CLI (three commands). | `ip dhcp pool LAN20 / network 192.168.20.0 255.255.255.0 / default-router 192.168.20.1` |
| c28 | R1 | 4.3 | We have clients on LAN10 that get an address but cannot resolve names. Hand them 192.168.10.5 as their DNS server from the CLI. | `dns-server 192.168.10.5` |
| c29 | R1 | 1.10 | We have a host that pings from the router but is not where the paperwork says. Grab the router's ARP cache from the CLI. | `show ip arp` |
| c30 | R1 | 1.10 | We have a router with an interface that may be shut down. Grab the one-table interface summary from the CLI. | `show ip interface brief` |
| c31 | R1 | 2.8 | We have router changes that would vanish on a reload. Save the configuration from the CLI. | `copy running-config startup-config ⏎` |
| c32 | PC1 | 1.10 | We have a PC with "no internet" and need its address, mask and gateway. Grab them from the CLI. | `ipconfig` |
| c33 | PC1 | 1.10 | We have a PC that may be on the wrong DHCP server. Grab the MAC address, DHCP server, lease times and DNS servers from the CLI. | `ipconfig /all` |
| c34 | PC1 | 4.3 | We have fixed the DHCP pool and the PC still has an old address. Ask the server for a fresh lease from the CLI. | `ipconfig /renew` |
| c35 | PC1 | 4.3 | We have a PC moving to another subnet and its lease should go back. Release the lease from the CLI. | `ipconfig /release` |
| c36 | PC1 | 1.10 | We have a PC that cannot reach anything. Test reachability to the gateway 192.168.10.1 from the CLI. | `ping 192.168.10.1` |
| c37 | PC1 | 1.10 | We have slow access to the server at 192.168.10.5. Grab the hop-by-hop path from the CLI. | `tracert 192.168.10.5` |
| c38 | PC1 | 1.13 | We have a duplicate-address complaint on the LAN. Grab the PC's ARP cache from the CLI. | `arp -a` |
| c39 | PC1 | 1.6 | We have a PC that must keep 192.168.10.50/24 with gateway 192.168.10.1. Set that static address on the Ethernet adapter from the CLI. | `netsh interface ip set address "Ethernet" static 192.168.10.50 255.255.255.0 192.168.10.1` |
| c40 | PC2 | 4.3 | We have PC2 on a static address that should come from DHCP. Put the adapter back on DHCP from the CLI. | `netsh interface ip set address "Ethernet" dhcp` |
| c41 | PC2 | 4.3 | We have a user who cannot open srv1.lab.local by name. Resolve it and see which server answered, from the CLI. | `nslookup srv1.lab.local` |
| c42 | PC2 | 4.3 | We have PC2 pointed at a dead DNS server. Point its DNS at 192.168.10.5 statically from the CLI. | `netsh interface ip set dns "Ethernet" static 192.168.10.5` |
| c43 | PC1 | 1.5 | We have a web server at 192.168.10.5 that pings but will not load. Test TCP port 80 from PowerShell. | `Test-NetConnection 192.168.10.5 -Port 80` |
| c44 | SRV1 | 1.5 | We have a server that should be serving web and DNS. Grab the listening TCP and UDP sockets with their programs from the CLI. | `ss -tulpn` |
| c45 | SRV1 | 1.10 | We have a server that may have the wrong address. Grab its interfaces and addresses from the CLI. | `ip address show` |
| c46 | SRV1 | 4.3 | We have a name that resolves on one PC and not another. Query the DNS server 192.168.10.5 for srv1.lab.local from the CLI. | `dig @192.168.10.5 srv1.lab.local` |

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
