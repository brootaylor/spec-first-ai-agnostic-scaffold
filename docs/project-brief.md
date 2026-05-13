# Project Brief

This file is the single source of truth for project context.

It is tech-agnostic — do not add anything here that is specific to any particular
tool, framework, or AI agent beyond what is selected in the Stack section below.

Agent-specific configs live in `.agents/`.

---

## What this project is

> *Describe your project here. For example:
> "A static informational website for a design system. It includes documentation, usage guidelines, and examples for the components and patterns in the design system. Users can browse the documentation, view code examples, and copy snippets for their own projects."*

---

## Stack

This section defines the framework and tooling for the project.
Mark exactly one option per category as `[active]`. Leave all others blank.

### Framework

The core framework for this project. Pick one.

| Framework | Active |
|-----------|--------|
| **Static Site Generators (SSG)** | |
| Eleventy *(11ty)* | |
| **Web Frameworks** | |
| Astro | |
| **Component Frameworks** | |
| React | |
| Svelte | |
| **No framework** | |
| Vanilla | `[active]` |

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

Applies to **Vanilla only**. SSG, web, and component frameworks manage their own build pipeline.

| Tool | Active |
|------|--------|
| Vite | `[active]` |
| None *(framework handles it)* | |

### Service worker

Optional. Defaults to `None`. See `docs/features/service-worker.md` for
full details on caching strategies and framework-specific implementation notes.

| Option | Active |
|--------|--------|
| None | `[active]` |
| Cache first *(assets)* + Network first *(pages)* — recommended for static sites | |
| Network first *(all)* — better for frequently updated content | |
| Stale while revalidate — serves cache immediately, updates in the background | |
| Custom — define your own strategy in `docs/features/service-worker.md` | |

### Storybook

Optional. Defaults to `None`. See `docs/features/storybook.md` for
setup instructions and framework-specific implementation notes.

| Option | Active |
|--------|--------|
| None | `[active]` |
| Storybook | |

### Constraints

Notes on combinations that don't make sense together.

- **Eleventy** — includes its own build pipeline. Build selection does not apply
- **Astro** — includes its own build pipeline. Build selection does not apply
- **React** — pair with Vite for a simple setup, or Next.js for a full meta-framework. Build selection does not apply
- **Svelte** — pair with Vite for a simple setup, or SvelteKit for a full meta-framework. Build selection does not apply
- **React + Jest** — include `@testing-library/react` and `@testing-library/jest-dom` as dev dependencies
- **Svelte + Jest** — include `@testing-library/svelte` as a dev dependency

### Setup instructions

Before writing any implementation code, the project dependencies and config files
need to be in place.

**If building by hand:**

- Set up `package.json` and any required config files
  (e.g. `vite.config.js`, `jest.config.js`) based on your active stack selections
- Check your chosen framework's documentation for the recommended Node.js version
  and update `.nvmrc` accordingly
- Refer to your chosen framework's documentation for the exact setup

**If using an AI agent:**

1. Check for the latest stable version of the active framework and use that version when populating `package.json`
2. Check the active framework's Node.js requirements and use the recommended LTS version of Node
3. Populate `package.json` with the correct scripts and dependencies for the active stack
4. Generate any required config files based on the active selections
5. Populate `.nvmrc` with the correct Node.js version for the active framework
6. Update the stack-specific section of `.gitignore` with any entries required by the active stack
7. If a service worker option is active, implement it following `docs/features/service-worker.md`
8. If Storybook is active, set it up following `docs/features/storybook.md`
9. Do not install any dependencies not directly required by the active stack selections

### Default starting files

- **Vanilla + Vite** — `src/index.html` is the default home page and `src/scripts/main.js` is the JavaScript file it references. Both are included as minimal starting files to build out
- **React** — `src/index.html` and `src/scripts/main.js` are the default starting files. Update `main.js` to mount the React app
- **Svelte** — `src/index.html` and `src/scripts/main.js` are the default starting files. Update `main.js` to mount the Svelte app
- **Astro** — pages and templating are managed by Astro's own file-based routing. Remove `src/index.html` and `src/scripts/main.js` if switching to Astro
- **Eleventy** — pages and templating are managed by Eleventy's own templating system. Remove `src/index.html` and `src/scripts/main.js` if switching to Eleventy

---

## Features and components

Understanding the difference between features and components is important for
working with this scaffold effectively.

A **feature** describes a piece of functionality from the user's perspective —
what they can do and why. Feature specs live in `docs/features/` and are written
in terms of user stories and acceptance criteria.

A **component** is a discrete, reusable piece of UI that implements part of a
feature. Component specs live in `docs/specs/components/` and define the
interface, behaviour, states, and test cases needed to build it.

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

> **Before writing any styles:**
>
> **If building by hand:**
>
> - Fill in `docs/design-tokens.md` with your token values
> - Implement the values in `src/styles/tokens.scss`
> - All styles should reference tokens rather than hardcoded values
>
> **If using an AI agent:**
>
> - Read `docs/design-tokens.md` before writing any styles
> - If the file is empty, stop and ask the user to fill it in first
> - All styles must reference tokens — never hardcoded values

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
  scripts/
    main.js                         # ← default starting file (Vanilla + Vite only)
  styles/
    tokens.scss                     # ← design token values (see docs/design-tokens.md)
    main.scss                       # ← global styles, imports tokens.scss
  lib/                              # ← shared utilities
  types/                            # ← global types (TypeScript only)
docs/
  project-brief.md                  # ← this file
  design-tokens.md                  # ← design token definitions
  features/                         # ← feature specs (user-facing and optional technical features)
  specs/
    _component-template.spec.md     # ← spec template
    components/                     # ← authoritative component specs
    pages/                          # ← page / view specs
    layouts/                        # ← layout specs
```

---

## Where to look

| Question | File |
|----------|------|
| What does a feature need to do? | `docs/features/<feature>.md` |
| What should a component do? | `docs/specs/components/<name>.spec.md` |
| What should a page look like? | `docs/specs/pages/<name>.spec.md` |
| What should a layout do? | `docs/specs/layouts/<name>.spec.md` |
