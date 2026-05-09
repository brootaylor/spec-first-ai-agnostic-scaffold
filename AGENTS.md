# AGENTS.md

This file explains how AI coding agents are set up in this project.
It is tool-agnostic — the pattern works with any capable coding agent.

---

## The core idea

All project context that an AI agent needs lives in one place:

```
docs/ai-context.md
```

This file is tool-agnostic. It describes the project, the stack, the coding
conventions, and the workflow the agent must follow. It is the single source
of truth — nothing is duplicated across agent-specific config files.

---

## Agent config structure

Each supported agent has its own directory inside `.agents/`:

```
.agents/
├── claude/          ← Claude Code (Anthropic)
├── cursor/          ← Cursor
└── copilot/         ← GitHub Copilot
```

Every file inside these directories does two things only:

1. Tells the agent to read `docs/ai-context.md` first
2. Adds anything that is genuinely specific to that tool
   (custom commands, model settings, etc.)

Nothing else belongs in these files.

---

## Adding a new agent

1. Create a directory under `.agents/<agent-name>/`
2. Create the agent's required config file inside it
3. Add a single line pointing to `docs/ai-context.md`
4. Add any tool-specific config below that line

That's it. All project conventions are already in `docs/ai-context.md`.

---

## Removing an agent

Delete its directory from `.agents/`. Nothing else needs to change.

---

## Important note on tool conventions

Most tools are designed to look for their config file in a specific location
(e.g. Claude Code expects `CLAUDE.md` at the project root). In this project,
config files live inside `.agents/` instead — you may need to point each tool
at the correct path when setting it up for the first time.

See each agent's directory for setup notes.

---

## Updating project conventions

Edit `docs/ai-context.md` only. Every agent picks up the change automatically
because their config files all point to it.
