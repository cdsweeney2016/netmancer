# Netmancer

A CCNA study game. You start on a help desk and rise to network engineer, fixing tickets on a simulated network by typing real commands. Everything is in one self-contained file, `netmancer.html`: open it in a browser, with no build step.

## Modes

- **Zero to Hero (Career):** tickets arrive in Mail on an in-game workstation. Ranks, reputation and the nightly Night Watch challenge live here. Each career is a separate save.
- **The Academy (Training):** pick exam objectives, or let it target your weak areas, then solve tickets back to back. It earns no career XP or rank.

Both modes share one skill profile: mastery and a review date for each exam objective, plus review cards, drills and the mistakes journal.

## Naming rule

Every command, keyword and protocol is real. Only trademarked brands get fictional names: the network gear is by Arcanet Systems running RuneOS, Windows-style PCs run "Casement", Linux-style ones "Oakhollow", and the VPN client is "Wardgate".

## Code layout (inside `netmancer.html`)

| Part | What it is |
| --- | --- |
| `NetmancerCore` | The engine: network simulation, the RuneOS CLI, the PC shells, grading, the ticket picker, review scheduling. No DOM or storage. |
| `NetmancerContent` | Data only: topologies, tickets, bad tickets, wiki pages, exam objectives, ranks. |
| `WebPlatform` | The storage and clipboard adapter, so the game can be ported to Electron/Steam later. |
| `NetmancerOS` | The UI: title screen, workstation (Mail, Terminal, Files, Map, Browser, Skills, Settings), and the Academy. |

## Testing

Open `netmancer.html#selftest` to run the built-in tests: the engine, the workstation and the game modes. It uses a throwaway save, so your progress isn't touched. Settings → Diagnostics runs the same tests in normal play.

Some browsers block a file opened straight from disk. If the self-test doesn't run, serve the folder over a local web server instead.

Screenshot demos: `#demo-mail`, `#demo-phone`, `#demo-academy`.

## Links

- Design doc: https://claude.ai/code/artifact/2936cf04-c15c-4a4e-a0d8-9dca49045f26
- Playable copy: https://claude.ai/artifact/WGEWFFJycGFEWpFZ8CEwDK. This is the same file, without its html/head/body wrapper and with the title "Netmancer".

Netmancer is an unofficial study game. CCNA is a trademark of Cisco Systems, Inc.; this game is not affiliated with or endorsed by Cisco.
