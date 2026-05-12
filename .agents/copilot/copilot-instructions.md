# GitHub Copilot — Agent Config

> Read `docs/project-brief.md` before doing anything else.
> All project conventions, workflow rules, and context live there.
> This file only contains additions specific to GitHub Copilot.

---

## Setup note

Copilot expects this file at `.github/copilot-instructions.md`. It lives here
instead at `.agents/copilot/copilot-instructions.md` as part of this project's
agent-agnostic structure. Symlinking is one option, though it isn't guaranteed
to work across all operating systems or agent versions:

```bash
ln -s .agents/copilot/copilot-instructions.md .github/copilot-instructions.md
```

---

## Copilot-specific notes

Before generating or editing anything, check whether a spec exists in the
relevant directory:

- `docs/specs/components/` — component specs
- `docs/specs/pages/` — page / view specs
- `docs/specs/layouts/` — layout specs

If no spec exists, tell the user to create one using
`docs/specs/_component-template.spec.md`.
