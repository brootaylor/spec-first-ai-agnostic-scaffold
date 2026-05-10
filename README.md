# Starter Project: Agnostic LLM Agent 'Scaffold'

This is my attempt at creating a starter project template *(scaffolding)* for building web applications with "Ai" agents using any large language model (LLM).

The idea is for it to be agnostic to any specific LLM or agent framework, and instead focus on the overall architecture and workflow for spec-first development with "Ai" agents.

**NOTE:** *This is a work in progress and will be updated over time as I learn more about what works best.*

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
