# AGENTS.md — instructions for coding agents

This file tells any coding agent (Hermes, Claude Code, Codex, Cursor) how to work
in this repository. It is **not** [docs/AGENTS.md](docs/AGENTS.md), which documents
the agent CLIs the bridge can drive.

Read [CONTRIBUTING.md](CONTRIBUTING.md) first: it is the source of truth for layout,
conventions and the test map. This file only adds what an automated agent needs on
top of it.

## What this repo is

A World of Warcraft addon (`addon/WoWAI`, Lua 5.1) plus a zero-dependency Node
companion (`bridge/`). They talk over a pixel strip drawn on screen (out) and
load-on-demand slot addons (in). Read [docs/ARCHITECTURE.md](docs/ARCHITECTURE.md)
before touching either transport.

## Setup and test

```bash
npm install     # test tooling only: fengari (Lua VM) and luaparse
npm test        # the portable suite; must pass before you push
```

`npm test` is safe in a headless, client-less environment: it exercises
`capture_x11.py` and `capture_mac.py` in decode-only mode.

These need a real game or a live agent CLI, so do not run them on a build box:

- `node setup.js` — needs a WoW client directory
- `npm run test:live` — needs a logged-in agent CLI
- `npm start`, `npm run probe`, `npm run probe:mac` — need a running bridge or game window

## Non-negotiables

- `bridge/` stays dependency-free: no `dependencies`, only `devDependencies`.
- Lua uses tabs, `local` everywhere, and only APIs present in the Forever client —
  check against the `forever` branch of Gethe/wow-ui-source before adding a call.
- JavaScript uses two-space indent, single quotes, `'use strict'`, CommonJS.
- Pure logic belongs in `bridge/protocol.js`, where it is testable without spawning.
- Every behaviour change gets an added or extended test in the matching file.
- Never edit generated slot files, `tests/tmp/` (gitignored scratch), or a local
  `bridge/config.json`.

## Two agents work in this repo

More than one agent works here, from more than one machine. Keep it safe:

- Never commit directly to `main`. Branch, push, open a pull request.
- Prefix the branch with the machine: `vps/<task>` or `desktop/<task>`.
- `git fetch origin` and rebase on `origin/main` before starting work.
- One logical change per PR; small commits with `fix:`, `feat:`, `docs:` subjects.
- Review comes from the other agent, never from the author of the change.
- `upstream` is the original project. Do not push to it; PRs target `origin`.
