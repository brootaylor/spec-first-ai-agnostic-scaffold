# Starter Project: Agnostic LLM Agent 'Scaffold'

This is my attempt at creating a starter project template *(scaffolding)* for building web applications with "Ai" agents using any large language model (LLM).

The idea is for it to be as agnostic as possible and not tied to any specific LLM or agent framework. Instead, focus on the overall architecture and workflow for spec-first development with "Ai" agents.

**NOTE:** *This is a work in progress and will be updated over time as I learn more about what works best.*

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

Before anything is built, a spec is written that defines its interface, behaviour, states, and test cases. An "Ai" coding agent then uses that spec to generate the implementation.

This scaffold supports specs for features, components, pages, and layouts. Each type lives in its own directory under `docs/specs/`. See `docs/ai-context.md` for an explanation of each type and when to use it.

The sequence for any new spec is:

1. Write a spec using `docs/specs/_component-template.spec.md` as a starting point
2. Run the agent command to scaffold the implementation (see `SETUP.md`)
3. Review the generated tests and implementation
4. Iterate

Feature requirements live in `docs/features/`. Each feature doc links to the specs it depends on, giving the agent the full picture before it writes a line of code.

---

## Adding or removing an agent

See `SETUP.md` for instructions.
