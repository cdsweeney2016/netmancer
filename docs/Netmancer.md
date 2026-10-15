---
title: Netmancer
tags: [index]
updated: 2026-10-15
---

# Netmancer

A single-file browser game for CCNA study. Players fix tickets on a simulated network by typing real commands. The whole game is `netmancer.html` (about 640 KB, 3,955 lines) in the repo root.

**Start here.** These notes exist so a work session can learn the project from a few short pages instead of reading the game file. Read the page you need, then grep the game file by function name.

| Page | Read it when |
| --- | --- |
| [Architecture](Architecture.md) | You need to change the engine, the UI, or how a ticket is built and graded |
| [Tickets](Tickets.md) | You are adding, fixing or looking up a ticket, template or topology |
| [Decisions](Decisions.md) | You wonder why something is the way it is (naming rule, modes, console look) |
| [Backlog](Backlog.md) | You are picking the next piece of work |
| [Workflow](Workflow.md) | You need to test, publish or commit |
| [Sessions](Sessions/) | You want to know what happened last time |

## Links

- Design doc (Claude Doc, the long version): https://claude.ai/code/artifact/2936cf04-c15c-4a4e-a0d8-9dca49045f26
- Playable copy: https://claude.ai/artifact/WGEWFFJycGFEWpFZ8CEwDK
- Repo: `E:\Projects\Netmancer` (git, branch `main`, no remote yet)

## Vocabulary

| In the game | Real thing |
| --- | --- |
| Arcanet Systems, RuneOS | The network vendor and its CLI (IOS-style syntax) |
| Casement prompt / Casement Shell | cmd / PowerShell on a Windows-style PC |
| Oakhollow | A Linux-style shell |
| Wardgate | The VPN client |
| Spire | The company whose help desk you work on |
| Quest, curse, ward check | Ticket, root cause, the state-based grading check |
| Runes | Mastery and review date per CCNA objective (shared skill profile) |
| Night Watch | The daily challenge: one quick fault plus five review cards |
| Era | A content tier: 1 Fundamentals, 2 Switching, 3 Routing |
