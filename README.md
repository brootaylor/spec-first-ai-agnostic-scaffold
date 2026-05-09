# Starter Project: Agnostic LLM Agent Scaffold

This is a starter project template for building web applications with AI agents using any large language model (LLM).

It provides a spec-first development workflow, where component specifications are written before implementation.

AI agents can then generate code based on these specs, ensuring alignment with requirements and test cases from the outset.

---

## Getting started

```bash
npm install
npm run dev
```

| Command | What it does |
|---------|-------------|
| `npm run dev` | Start the development server |
| `npm run build` | Type-check and build for production |
| `npm test` | Run unit and integration tests (Vitest) |
| `npm run e2e` | Run end-to-end tests (Playwright) |
| `npm run lint` | Lint the codebase |

---

## Tech stack

| Layer | Technology |
|-------|------------|
| Language | TypeScript (strict mode) |
| Unit / integration tests | Vitest |
| End-to-end tests | Playwright |
| Styles | CSS Modules |
| HTTP | Fetch API |
| Build | Vite |

---

## Project structure

```
my-project/
├── README.md               ← you are here
├── AGENTS.md               ← AI agent setup and conventions
│
├── docs/
│   ├── ai-context.md       ← single source of truth for AI agents
│   ├── architecture.md     ← system design decisions
│   ├── design-tokens.md    ← CSS naming conventions
│   ├── features/           ← user-facing feature specs
│   └── specs/
│       ├── _template.spec.md
│       └── components/     ← authoritative component specs
│
├── .agents/                ← AI agent config (see AGENTS.md)
│   ├── claude/
│   ├── cursor/
│   └── copilot/
│
├── src/
│   ├── components/         ← one folder per component
│   ├── lib/                ← shared utilities
│   └── types/
│       └── index.ts        ← global TypeScript types
│
└── tests/
    └── e2e/                ← Playwright end-to-end tests
```

---

## How development works

This project follows a **spec-first workflow**. Before any component is built,
a spec is written that defines its interface, behaviour, states, and test cases.
An AI coding agent then uses that spec to generate the implementation.

The sequence for any new component is:

1. Write a spec in `docs/specs/components/` using `docs/specs/_template.spec.md`
2. Run the agent command to scaffold the component (see `AGENTS.md`)
3. Review the generated tests and implementation
4. Iterate

Feature requirements live in `docs/features/`. Each feature doc links to the
component specs it depends on, giving the agent the full picture before it
writes a line of code.

---

## Contributing

- Read `docs/ai-context.md` for coding conventions before making changes
- Every new component needs a spec before implementation begins
- Tests are written before implementation — see the workflow above
- Do not modify files in `src/generated/` — these are auto-generated at build time
