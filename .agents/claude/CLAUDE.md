# Claude Code — Agent Config

> Read `docs/ai-context.md` before doing anything else.
> All project conventions, workflow rules, and context live there.
> This file only contains additions specific to Claude Code.

---

## Setup note

Claude Code expects to find this file at the project root as `CLAUDE.md`.
It lives here instead at `.agents/claude/CLAUDE.md` as part of this project's
agent-agnostic structure. Point Claude Code at this path when starting a session,
or symlink it: `ln -s .agents/claude/CLAUDE.md CLAUDE.md`

---

## Claude Code-specific notes

Custom slash commands are in `.agents/claude/commands/`.
Model and context file settings are in `.agents/claude/settings.json`.

When a custom command exists for a task (e.g. `/create-component`), use it
rather than improvising — the commands encode the required workflow.
