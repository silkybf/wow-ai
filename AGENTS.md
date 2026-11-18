# AGENTS.md — instructions for coding agents

This file tells any coding agent (Hermes, Claude Code, Codex, Cursor) how to work
in this repository. It is **not** [docs/AGENTS.md](docs/AGENTS.md), which documents
the five agent CLIs the bridge can drive.

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
