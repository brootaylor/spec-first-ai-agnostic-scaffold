# Spec-First Scaffold for Any AI Agent

A starter template for building web applications with "Ai" agents using any large language model (LLM).

It is agnostic to any specific LLM or agent — the focus is on the architecture and workflow for spec-first development, not the tool you use to build it.

> **NOTE:** *This is a work in progress and will be updated over time as I learn more about what works best.*

---

## Why spec-first?

Writing specs before code forces clarity. Before an agent writes a single line of implementation, it knows exactly what a component should do, what states it has, how it should behave, and what tests it needs to pass. This reduces guesswork, prevents scope creep, and makes it easier to review what the agent produces.

It also means the spec becomes the shared language between you and the agent — if the output isn't right, the spec is the first place to look.

---

## Choosing your stack

`docs/ai-context.md` includes a stack selector where you can mark your preferred framework, language, styles, testing tools, and build tool. The agent reads this before doing anything and uses it to make the right implementation decisions. Switching stack is as simple as changing the active selection.

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
├── SETUP.md                              # ← "Ai" agent setup and conventions
│
├── docs/
│   ├── ai-context.md                     # ← single source of truth for "Ai" agents
│   ├── features/                         # ← user-facing feature specs
│   └── specs/
│       ├── _component-template.spec.md   # ← spec template
│       ├── components/                   # ← component specs
│       ├── pages/                        # ← page / view specs
│       └── layouts/                      # ← layout specs
│
└── .agents/                              # ← "Ai" agent config (see SETUP.md)
    ├── claude/
    ├── cursor/
    └── copilot/
```

---

## How it works

This scaffold follows a spec-first workflow — specs are written before any code is generated. Each spec defines the interface, behaviour, states, and test cases for what's being built. The agent uses the spec to generate the implementation.

See `WORKFLOW.md` for the full step-by-step guide.

---

## Adding or removing an agent

See `SETUP.md` for instructions.
