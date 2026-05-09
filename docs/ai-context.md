# AI Context

> This file is the single source of truth for AI agent context.
> It is tool-agnostic — do not add anything here that is specific to
> Claude Code, Cursor, Copilot, or any other tool.
> Tool-specific config lives in .agents/.
>
> All agents are instructed to read this file first.

---

## What this project is

A customer facing web application for Blah Blah Corp. Registered users can browse a product
catalogue, manage their account, and place orders. The frontend is a TypeScript SPA;
the backend lives in a separate repository (`blah-api`).

---

## Stack

| Layer              | Technology                        |
|--------------------|-----------------------------------|
| Language           | TypeScript (strict mode)          |
| Unit / integration | Vitest                            |
| End-to-end         | Playwright                        |
| Styles             | CSS Modules                       |
| HTTP               | Fetch API (no third-party client) |
| Linting            | ESLint + Prettier                 |
| Build              | Vite                              |

---

## File & folder conventions

```
src/
  components/
    <ComponentName>/
      <ComponentName>.ts          ← implementation
      <ComponentName>.test.ts     ← unit tests
      <ComponentName>.module.css  ← scoped styles
      <ComponentName>.spec.md     ← co-located spec
  lib/           ← shared utilities
  types/
    index.ts     ← global TypeScript types
docs/
  ai-context.md        ← this file
  architecture.md
  design-tokens.md
  features/            ← user-facing feature specs
  specs/
    _template.spec.md
    components/        ← authoritative component specs
```

---

## Code conventions

- **Named exports only** — no default exports anywhere
- **Explicit return types** on every function
- **No `any`** — use `unknown` and narrow with type guards
- CSS class names: `kebab-case`
- File names: `PascalCase` for components, `camelCase` for utilities
- Keep component files under 200 lines; extract helpers to `src/lib/`

---

## Workflow: spec → interface → tests → implementation

1. Read the component's `*.spec.md` before writing a single line of code
2. Derive the TypeScript interface from the spec's Props table
3. Write the test file first — all tests should fail at this point
4. Implement until all tests pass
5. Do not add props or behaviour not listed in the spec without flagging it

---

## What the AI must NOT do

| Rule | Reason |
|------|--------|
| No `console.log` | Use `src/lib/logger.ts` instead |
| No changes to `src/generated/` | Auto-generated at build time |
| No new npm dependencies without user approval | Keeps the dependency surface small |
| No tests that assert implementation details | Test observable behaviour only |
| No guessing when a spec is ambiguous | Stop and ask |

---

## Where to look for more context

| Question | File |
|----------|------|
| How does the system fit together? | `docs/architecture.md` |
| What does a feature need to do? | `docs/features/<feature>.md` |
| What should a component do? | `docs/specs/components/<name>.spec.md` |
| What design tokens exist? | `docs/design-tokens.md` |
