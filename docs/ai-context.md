# AI Context

This file is the single source of truth for "Ai" agent context.

It is agent-agnostic &mdash; do not add anything here that is specific to Claude Code, Cursor, Copilot, or any other agent/tool.

Agent-specific configs live in `.agents/`.

---

## What this project is

> *Describe your project here. For example:
> "A customer facing web application for ABC Corp. Registered users can browse
> a product catalogue, manage their account, and place orders."*

---

## File & folder conventions

```bash
src/
  components/
    <ComponentName>/
      <ComponentName>.ts          # ← implementation
      <ComponentName>.test.ts     # ← unit tests
      <ComponentName>.module.css  # ← scoped styles
      <ComponentName>.spec.md     # ← co-located spec
  lib/                            # ← shared utilities
  types/
    index.ts                      # ← global TypeScript types
docs/
  ai-context.md                   # ← this file
  features/                       # ← user-facing feature specs
  specs/
    _template.spec.md
    components/                   # ← authoritative component specs
```

---

## Where to look for more context

| Question | File |
|----------|------|
| What does a feature need to do? | `docs/features/<feature>.md` |
| What should a component do? | `docs/specs/components/<name>.spec.md` |
