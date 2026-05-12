# Tech-Agnostic Spec-First Development Scaffold

A starter template for building web projects using a spec-first approach.

Write the spec first. Then build — by hand, with an AI agent, or both.

> **NOTE:** *This is a work in progress and will be updated over time as I learn more about what works best.*

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

## Examples included

The scaffold comes with a small set of working examples to illustrate the patterns:

- **Feature:** Dark mode (`docs/features/dark-mode.md`)
- **Components:** Button, ThemeToggle (`docs/specs/components/`)
- **Page:** Dashboard (`docs/specs/pages/`)
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

See [WORKFLOW.md](./WORKFLOW.md) for prerequisites and the full step-by-step guide. The workflow covers how to choose your stack, write feature specs, write component/page/layout specs, and build by hand or with an AI agent. It also includes tips for writing good specs that lead to better output.

---

## Using an AI agent

See [AGENTS.md](./AGENTS.md) for instructions on setting up and switching between agents. Each agent has its own config file in `.agents/<agent-name>/` that tells it to read `docs/project-brief.md` for context. From there, the agent understands the project conventions and workflow without needing you to explain anything.
