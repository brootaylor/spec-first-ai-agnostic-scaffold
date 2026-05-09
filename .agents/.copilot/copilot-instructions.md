# GitHub Copilot — Agent Config

> Read `docs/ai-context.md` before doing anything else.
> All project conventions, workflow rules, and context live there.
> This file only contains additions specific to GitHub Copilot.

---

## Setup note

Copilot expects this file at `.github/copilot-instructions.md`. It lives here
instead at `.agents/copilot/copilot-instructions.md` as part of this project's
agent-agnostic structure. Symlink it when setting up:
`ln -s .agents/copilot/copilot-instructions.md .github/copilot-instructions.md`

---

## Copilot-specific notes

When suggesting a new component, check whether a spec exists in
`docs/specs/components/` before generating code. If no spec exists,
tell the user to create one using `docs/specs/_template.spec.md`.
