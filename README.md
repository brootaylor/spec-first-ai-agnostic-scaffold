# Starter Project: Agnostic LLM Agent 'Scaffold'

This is my attempt at creating a starter project template *(scaffolding)* for building web applications with "Ai" agents using any large language model (LLM).

The idea is for it to be agnostic to any specific LLM or agent framework, and instead focus on the overall architecture and workflow for spec-first development with "Ai" agents.

**NOTE:** *This is a work in progress and will be updated over time as I learn more about what works best.*

---

## What's in this scaffold

```bash
my-project/
├── README.md               # ← you are here
├── SETUP.md               # ← "Ai" agent setup and conventions
│
├── docs/
│   ├── ai-context.md       # ← single source of truth for "Ai" agents
│   ├── features/           # ← user facing feature specs
│   └── specs/
│       ├── _template.spec.md
│       └── components/     # ← authoritative component specs
│
└── .agents/                # ← "Ai" agent config (see SETUP.md)
    ├── claude/
    ├── cursor/
    └── copilot/
```

---

## How it works

Before any component is built, a spec is written that defines its interface, behaviour, states, and test cases. An "Ai" coding agent then uses that spec to generate the implementation.

The sequence for any new component is:

1. Write a spec in `docs/specs/components/` using `docs/specs/_template.spec.md`
2. Run the agent command to scaffold the component (see `SETUP.md`)
3. Review the generated tests and implementation
4. Iterate

Feature requirements live in `docs/features/`. Each feature doc links to the component specs it depends on, giving the agent the full picture before it writes a line of code.

---

## Adding or removing an agent

See `SETUP.md` for instructions.
