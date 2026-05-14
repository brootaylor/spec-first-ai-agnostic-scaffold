# AGENTS.md

AGENTS.md explains how AI coding agents are set up in this project.
The pattern is agent-agnostic — it works with any capable coding agent.

---

## The core idea

All project context that an AI agent needs lives in one place:

```bash
docs/project-brief.md
```

`project-brief.md` is tech-agnostic. It describes the project, the stack, the coding conventions, and the workflow the agent must follow. It is the single source of truth — nothing is duplicated across agent-specific config files.

---

## How an agent reads this scaffold

Agents don't run in the background — they only read the project context when you actively invoke them in their respective agent.

When you fire up an agent, the sequence is:

1. You open your agent of choice (e.g. Claude Code, Cursor, Copilot, etc.)
2. The agent looks for its config file at its hardwired default location. A symlink (or file copy) there points to the real file inside `.agents/<agent-name>/`
3. That config file tells the agent to read `docs/project-brief.md`
4. The agent now has the full project context and is ready to work

From that point it understands your conventions, your workflow, and where everything lives — without you having to explain any of it each time.

---

## Agent config structure

Each supported agent has its own directory inside `.agents/`:

```bash
.agents/
├── claude/     # ← Claude Code (Anthropic)
├── cursor/     # ← Cursor
├── copilot/    # ← GitHub Copilot
└── ...         # ← add any agent that has a config file convention
```

Every file inside these directories does two things only:

1. Tells the agent to read `docs/project-brief.md` first
2. Adds anything that is genuinely specific to that agent (custom commands, model settings, etc.)

Nothing else belongs in these files.

---

## How agent config files are wired up

Most agents are hardwired to look for their config file in a specific location
and don't provide a native way to change this. In this project, config files
live inside `.agents/` instead, so a workaround is needed for each agent.

The most common approach is symlinking — creating a pointer from where the agent
expects its file to where it actually lives. For example, Claude Code expects
`CLAUDE.md` at the project root, so you would run:

```bash
ln -s .agents/claude/CLAUDE.md CLAUDE.md
```

This creates a `CLAUDE.md` at the root that points to the real file inside
`.agents/claude/`.

**macOS / Linux:** symlinking works as shown above.

**Windows:** `ln -s` requires either Developer Mode or an elevated terminal
(run as Administrator). If neither is an option, copy the file instead of
symlinking it and keep the two in sync manually:

```bash
copy .agents\copilot\copilot-instructions.md .github\copilot-instructions.md
```

**Git and symlinks:** symlinks are tracked by Git and work correctly on macOS
and Linux. If your team includes Windows users, consider adding root-level
symlinks to `.gitignore` and documenting the manual setup step instead, to
avoid broken links for collaborators who don't have symlink support enabled.

See each agent's directory for wiring notes specific to that agent.

---

## Switching between agents

There is no project-level switch to flip. Each agent reads from the same
`docs/project-brief.md`, so all agents share the same understanding of the
project at all times.

To use a different agent, open that agent and ensure it has been pointed at its
config file in `.agents/<agent-name>/`. See each agent's directory for first
time setup notes.

---

## Adding a new agent

1. Create a directory under `.agents/<agent-name>/`
2. Create the agent's required config file inside it
3. In that config file, instruct the agent to read `docs/project-brief.md` first. See `.agents/claude/CLAUDE.md` for a concrete example of how this looks in practice
4. Add any agent-specific config below that instruction
5. Create a symlink (or file copy) from the agent's expected location to the file you just created — see [How agent config files are wired up](#how-agent-config-files-are-wired-up) above

That's it. All project conventions are already in `docs/project-brief.md`.

---

## Removing an agent

1. Remove the symlink (or file copy) at the project root or wherever the agent expected it:

```bash
rm CLAUDE.md
```

2. Delete its directory from `.agents/`:

```bash
rm -rf .agents/<agent-name>
```

Nothing else needs to change.

---

## Updating project conventions

Edit `docs/project-brief.md` only. Every agent picks up the change automatically
because their config files all point to it.

---

## Troubleshooting

**The agent isn't reading `docs/project-brief.md`.**

Check that the symlink (or file copy) exists at the location the agent expects.
You can verify a symlink is wired up correctly with:

```bash
ls -la
```

Look for an entry like `CLAUDE.md -> .agents/claude/CLAUDE.md`. If it's missing,
follow the setup steps in [How agent config files are wired up](#how-agent-config-files-are-wired-up).

**The agent reads the config file but ignores the project brief.**

Some agents require an explicit instruction in the config file to read external
files — a path alone isn't always enough. Check the agent's documentation and
review how the existing configs in `.agents/` handle this to use them as a
reference.

**The agent produces output that contradicts the project brief.**

The brief may be incomplete or ambiguous in the area the agent is working in.
Go back to `docs/project-brief.md`, clarify the relevant section, and re-run.
Do not edit the agent's output directly to paper over a brief that needs updating.
