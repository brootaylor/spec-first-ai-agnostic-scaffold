# Tech-Agnostic Spec-First Development Scaffold

A starter template for building web projects using a tech-agnostic spec-first approach.

Write the spec first. Then build — by hand, with an AI agent, or both.

> **NOTE:** *This is a work in progress and will be updated over time as I learn more about what works best.*

---

## Getting started

If you have a GitHub account, click the **"Use this template"** button at the top of this repo to create a new repository with all the scaffold files as a clean starting point.

Alternatively:

- **Clone it** — `git clone https://github.com/brootaylor/tech-agnostic-spec-first-dev-scaffold.git`
- **Download as ZIP** — click **Code → Download ZIP** on the repo page

From there, follow [WORKFLOW.md](./WORKFLOW.md) to set up your project.

---

## Features

- **Spec-first workflow** — specs are written before any code is produced. The spec is the source of truth throughout, for humans and agents alike
- **Two ways to build** — handcrafted or AI-assisted. Both paths use the same specs and workflow
- **Tech-agnostic** — works with Vanilla, Astro, Eleventy, React, or Svelte out of the box. Framework, language, styles, testing tools, and build tool are all configurable via a simple stack selector in `docs/project-brief.md` — and new options can be added to suit any project
- **AI agent agnostic** — not tied to any specific AI agent. Includes config for Claude Code, Cursor, and GitHub Copilot out of the box, with a clear pattern for adding others
- **Design token foundation** — a template and file structure for defining the visual language of a project before writing any styles
- **Service worker support** — optional offline and caching support, with a strategy selector and framework-specific guidance built in
- **Living documentation** — specs double as project documentation. Keep them up to date and the whole project stays coherent for humans and agents alike

---

## Why spec-first?

Writing specs before code forces clarity. Before anyone — human or agent — writes a single line of implementation, the spec defines exactly what a component should do, what states it has, how it should behave, and what tests it needs to pass. This reduces guesswork, prevents scope creep, and makes it easier to review what gets produced.

The spec becomes the shared language for the project — if the output isn't right, the spec is the first place to look.

---

## Two ways to use this scaffold

**Handcrafted** — use the specs and workflow as directions for building the project yourself. The specs tell you exactly what to build and the workflow guides you through the process.

**AI-assisted** — use an AI coding agent of your choice to read the specs and generate the implementation. The `.agents/` directory contains configuration for Claude Code, Cursor, and GitHub Copilot. See [AGENTS.md](./AGENTS.md) for setup instructions.

Both paths follow the same workflow and use the same specs.

---

## Choosing your stack

[`docs/project-brief.md`](./docs/project-brief.md) includes a stack selector where you can mark your preferred framework, language, styles, testing tools, and build tool.

This is the single source of truth for the project — both humans and agents refer to it before doing anything.

---

## Design tokens

[`docs/design-tokens.md`](./docs/design-tokens.md) is a template for defining the visual language of your project — colours, spacing, typography, and other design constants.

Fill it in before writing any styles. Both humans and agents use it as the reference for all style decisions. Values are implemented in `src/styles/tokens.scss` and referenced throughout the codebase as CSS custom properties.

---

## Examples included

The scaffold comes with a small set of working examples to illustrate the patterns:

- **Feature:** Dark mode (`docs/features/dark-mode.md`)
- **Components:** Button, ThemeToggle (`docs/specs/components/`)
- **Page:** Home (`docs/specs/pages/`)
- **Layout:** MainLayout (`docs/specs/layouts/`)

These are real specs that follow the same conventions you would use in a production project. Use them as reference or replace them with your own.

---

## What's in this scaffold

```bash
my-project/
├── README.md                             # ← you are here
├── WORKFLOW.md                           # ← step-by-step guide to using this scaffold
├── AGENTS.md                             # ← optional AI agent setup
│
├── docs/
│   ├── project-brief.md                  # ← single source of truth for the project
│   ├── design-tokens.md                  # ← design token definitions
│   ├── features/                         # ← user-facing feature specs
│   └── specs/
│       ├── _component-template.spec.md   # ← spec template
│       ├── components/                   # ← component specs
│       ├── pages/                        # ← page / view specs
│       └── layouts/                      # ← layout specs
│
└── .agents/                              # ← optional AI agent config (see AGENTS.md)
    ├── claude/
    ├── cursor/
    └── copilot/
```

---

## How it works

This scaffold follows a spec-first workflow — specs are written before any code is produced. Each spec defines the interface, behaviour, states, and test cases for what's being built. From there, you build it yourself or hand it to an AI agent.

See [WORKFLOW.md](./WORKFLOW.md) for prerequisites and the full step-by-step guide.

---

## Using an AI agent

See [AGENTS.md](./AGENTS.md) for instructions on setting up and switching between agents. Each agent has its own strengths and weaknesses, so it's a matter of experimentation to see which one works best for you.

When using an agent, the workflow is the same — write the spec first, then ask the agent to implement it. The agent will read the spec, understand what's required, and generate the code accordingly.
