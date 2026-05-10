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

## Stack

This section defines the framework and tooling the agent must use.
Mark exactly one option per category as `[active]`. Leave all others blank.

### Framework

The core framework for this project. Pick one.

| Framework | Active |
|-----------|--------|
| Eleventy (11ty) | |
| Astro | |
| Vanilla (no framework) | `[active]` |

### Language

| Language | Active |
|----------|--------|
| TypeScript | |
| JavaScript | `[active]` |

### Styles

| Approach | Active |
|----------|--------|
| Plain CSS | `[active]` |
| Sass | |

### Unit testing

| Tool | Active |
|------|--------|
| Jest | `[active]` |
| None | |

### E2E testing

| Tool | Active |
|------|--------|
| Playwright | |
| None | `[active]` |

### Build

| Tool | Active |
|------|--------|
| Vite | `[active]` |
| None (framework handles it) | |

### Constraints

Notes on combinations that don't make sense together.

- **Astro** includes its own build pipeline — set Build to `None` when using Astro
- **Eleventy** includes its own build pipeline — set Build to `None` when using Eleventy

### Agent instructions

When the stack selection is read, the agent must complete the following before writing any implementation code:

1. Populate `package.json` with the correct scripts and dependencies for the active stack
2. Generate any required config files (e.g. `vite.config.js`, `jest.config.js`, `astro.config.mjs`) based on the active selections
3. Do not install any dependencies not directly required by the active stack selections

---

## Features and components

Understanding the difference between features and components is important for
working with this scaffold effectively.

A **feature** describes a piece of functionality from the user's perspective —
what they can do and why. Feature specs live in `docs/features/` and are written
in terms of user stories and acceptance criteria.

A **component** is a discrete, reusable piece of UI that implements part of a
feature. Component specs live in `docs/specs/components/` and define the
interface, behaviour, states, and test cases an agent needs to build it.

A feature will typically depend on one or more components. The feature spec
lists which components are required before implementation can begin.

---

## Other spec types

Beyond features and components, the following spec types may be added to
`docs/specs/` as a project grows:

| Type | Location | Describes |
|------|----------|-----------|
| Pages / Views | `docs/specs/pages/` | A full page composed of multiple components |
| Layouts | `docs/specs/layouts/` | Reusable page structure wrapping content |
| Hooks | `docs/specs/hooks/` | Reusable logic shared across components |

The following are better suited to standalone reference docs in `docs/` rather
than specs:

| Type | Location | Describes |
|------|----------|-----------|
| Services / API | `docs/services.md` | How the frontend communicates with the backend |
| Design tokens | `docs/design-tokens.md` | Colours, spacing, typography, and other design constants |

---

## File & folder conventions

File extensions follow the active stack selection in the Stack section above.

```bash
src/
  components/
    <ComponentName>/
      <ComponentName>.{js|ts}       # ← implementation
      <ComponentName>.test.{js|ts}  # ← unit tests
      <ComponentName>.{css|scss}    # ← styles
      <ComponentName>.spec.md       # ← co-located spec
  pages/
    <PageName>/
      <PageName>.{js|ts}            # ← implementation
      <PageName>.test.{js|ts}       # ← unit tests
      <PageName>.{css|scss}         # ← styles
      <PageName>.spec.md            # ← co-located spec
  layouts/
    <LayoutName>/
      <LayoutName>.{js|ts}          # ← implementation
      <LayoutName>.{css|scss}       # ← styles
      <LayoutName>.spec.md          # ← co-located spec
  lib/                              # ← shared utilities
  types/                            # ← global types (TypeScript only)
docs/
  ai-context.md                   # ← this file
  features/                       # ← user-facing feature specs
  specs/
    _component-template.spec.md   # ← spec template
    components/                   # ← authoritative component specs
    pages/                        # ← page / view specs
    layouts/                      # ← layout specs
```

---

## Where to look for more context

| Question | File |
|----------|------|
| What does a feature need to do? | `docs/features/<feature>.md` |
| What should a component do? | `docs/specs/components/<name>.spec.md` |
| What should a page look like? | `docs/specs/pages/<name>.spec.md` |
| What should a layout do? | `docs/specs/layouts/<name>.spec.md` |
