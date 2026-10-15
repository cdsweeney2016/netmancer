# Netmancer

A single-file browser game for CCNA study: `netmancer.html` (about 640 KB, 3,955 lines).

## Read the notes, not the file

The project's knowledge is an Obsidian vault in `docs/`. Start at `docs/Netmancer.md`, then open only the page you need:

- `docs/Architecture.md`: the five script blocks and the key functions by name, how a ticket runs, the save model.
- `docs/Tickets.md`: ticket schema, every ticket and topology, how to add one.
- `docs/Decisions.md`: why things are the way they are.
- `docs/Backlog.md`: what to do next.
- `docs/Workflow.md`: how to edit, test, publish and commit.
- `docs/Sessions/`: what happened last time.

Do not read `netmancer.html` end to end. Grep it by function name and read only the region you are changing. The content pack can be evaluated in node for data questions (see the generator snippet in `docs/Workflow.md`).

## Rules

- Every command, keyword and output format is real; only brands are fictional (Arcanet/RuneOS, Casement, Oakhollow, Wardgate). Never add a real vendor name to the game world.
- Keep the engine (`NetmancerCore`), content (`NetmancerContent`) and UI (`NetmancerOS`) separate. ES5 style, no build step, no template literals.
- Every change: syntax-check the script blocks, run `#selftest` (three suites must PASS), then update the vault page it affects and add a line to `docs/Sessions/<date>.md`.
- Commit here, in this repo, never in another project's checkout.
