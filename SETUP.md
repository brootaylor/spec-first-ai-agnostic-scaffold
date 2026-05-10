# SETUP.md

SETUP.md explains how "Ai" coding agents are set up in this project.

The pattern is agent-agnostic &mdash; it works with any capable coding agent.

---

## The core idea

All project context that an "Ai" agent needs lives in one place:

```bash
docs/ai-context.md
```

`ai-context.md` is agent-agnostic. It describes the project, the stack, the coding conventions, and the workflow the agent must follow. It is the single source of truth &mdash; nothing is duplicated across agent-specific config files.

---

## How an agent reads this scaffold

Agents don't run in the background &mdash; they only read the project context when you actively invoke them in their respective tool.

When you fire up an agent, the sequence is:

1. You open your tool of choice (eg. Claude Code, Cursor, Copilot, etc.)
2. The tool looks for its config file in `.agents/<agent-name>/`
3. That config file tells the agent to read `docs/ai-context.md`
4. The agent now has the full project context and is ready to work

From that point it understands your conventions, your workflow, and where everything lives &mdash; without you having to explain any of it each time.

---

## Agent config structure

Each supported agent has its own directory inside `.agents/`:

```bash
.agents/
├── claude/          # ← Claude Code (Anthropic)
├── cursor/          # ← Cursor
└── copilot/         # ← GitHub Copilot
```

Every file inside these directories does two things only:

1. Tells the agent to read `docs/ai-context.md` first
2. Adds anything that is genuinely specific to that tool (custom commands, model settings, etc.)

Nothing else belongs in these files.

---

## Switching between agents

There is no project level switch to flip. Each agent reads from the same `docs/ai-context.md`, so all agents share the same understanding of the project at all times.

To use a different agent, simply open that tool and ensure it has been pointed at its config file in `.agents/<agent-name>/`. See each agent's directory for first time setup notes.

---

## Adding a new agent

1. Create a directory under `.agents/<agent-name>/`
2. Create the agent's required config file inside it
3. Add a single line pointing to `docs/ai-context.md`
4. Add any agent-specific config below that line

That's it. All project conventions are already in `docs/ai-context.md`.

---

## Removing an agent

Delete its directory from `.agents/`. Nothing else needs to change.

---

## Important note on tool conventions

Most tools are hardwired to look for their config file in a specific location and don't provide a native way to change this. In this project, config files live inside `.agents/` instead, so a workaround is needed for each tool.

The most common approach is symlinking &mdash; creating a pointer from wherethe tool expects its file to where it actually lives. For example, Claude Code expects `CLAUDE.md` at the project root, so you would run:

```bash
ln -s .agents/claude/CLAUDE.md CLAUDE.md
```

This creates a `CLAUDE.md` at the root that points to the real file inside `.agents/claude/`. However, this behaviour isn't guaranteed across all operating systems or tool versions, so check each tool's documentation before relying on it.

See each agent's directory for notes specific to that tool.

---

## Updating project conventions

Edit `docs/ai-context.md` only. Every agent picks up the change automatically because their config files all point to it.
