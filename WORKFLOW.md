# WORKFLOW.md

A step-by-step guide to using this scaffold to build a web project — by hand or with an AI coding agent.

---

## Prerequisites

Before you begin, make sure you have the following installed:

**Always required:**

| Tool | Notes |
|------|-------|
| [Git](https://git-scm.com) | Required to clone this scaffold. Recommended for version control throughout development |
| [Node.js](https://nodejs.org) | Required by most tooling — install the LTS version |
| [npm](https://www.npmjs.com) | Comes with Node.js |
| A code editor | [VS Code](https://code.visualstudio.com) is a good option |

**Agent-specific:**

| Agent | Prerequisites |
|-------|--------------|
| Claude Code | Node.js + an [Anthropic API key](https://console.anthropic.com) |
| Cursor | Download the [Cursor app](https://cursor.sh) |
| GitHub Copilot | A GitHub account with [Copilot access](https://github.com/features/copilot) + the relevant IDE's extension |

**Stack-specific:**

All stack dependencies are installed via `npm install`. Refer to your chosen framework's documentation for any additional setup.

---

## Step 1 — Set up the scaffold

**Comes with the scaffold — no action needed:**

```bash
README.md
WORKFLOW.md
AGENTS.md
package.json
.gitignore
docs/project-brief.md
docs/design-tokens.md
docs/features/dark-mode.md
docs/specs/_component-template.spec.md
docs/specs/components/button.spec.md
docs/specs/components/theme-toggle.spec.md
docs/specs/pages/home.spec.md
docs/specs/layouts/main-layout.spec.md
src/index.html
src/scripts/main.js
src/styles/tokens.scss
src/styles/main.scss
.agents/claude/CLAUDE.md
.agents/claude/settings.json
.agents/claude/commands/create-component.md
.agents/cursor/rules
.agents/copilot/copilot-instructions.md
```

> The files above are part of the default scaffold. Many are placeholder examples — the spec files, feature docs, and style stubs are there to illustrate the patterns, not to be used as-is. Replace or modify them to suit your project.

**If building by hand** — these directories can be created as needed:

```bash
src/components/
src/pages/
src/layouts/
```

**If using an AI agent** — the agent will create any missing directories as needed when scaffolding components, pages, and layouts.

You'll notice `package.json` is intentionally minimal — it contains only the project name and version. Once you've chosen your stack in `docs/project-brief.md` (Step 3), it needs to be populated with the correct dependencies for your chosen framework, language, testing tools, and build tool.

**If building by hand** — set up `package.json` and any required config files (e.g. `vite.config.js`, `jest.config.js`) yourself based on your stack selections. Also update the stack-specific section of `.gitignore` with any entries required by your chosen framework (e.g. `dist/` for Vite, `_site/` for Eleventy, `.astro/` for Astro). Refer to your chosen framework's documentation for the exact setup.

**If using an AI agent** — the agent will populate `package.json` and generate any required config files before writing any code.

Two default starting files are included for the Vanilla + Vite stack:

- `src/index.html` — the default home page Vite serves
- `src/scripts/main.js` — the JavaScript file referenced by `index.html`

If building with React or Svelte, these files are also used — `main.js` needs to be updated to mount the app for the active framework. If you switch to Astro or Eleventy, remove these two files — those frameworks manage their own pages and templating.

Commit everything to Git before you do anything else. This gives you a clean baseline to return to.

---

## Step 2 — Configure your agent

Open `.agents/<your-agent>/` and follow the setup notes in that directory to point your agent at the config file.

For example, if you're using Claude Code:

```bash
ln -s .agents/claude/CLAUDE.md CLAUDE.md
```

See `AGENTS.md` for a full explanation of how agents are configured in this scaffold.

---

## Step 3 — Fill in `project-brief.md`

Open `docs/project-brief.md` and do two things:

**Describe your project** — replace the placeholder under "What this project is" with a plain description of what you're building and who it's for.

**Choose your stack** — open `docs/project-brief.md` and mark exactly one option per category as `[active]`. Categories to configure:

- Framework
- Language
- Styles
- Unit testing
- E2E testing
- Build *(Vanilla only)*

For example, the Framework category looks like this:

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

This is the first thing the agent reads. Getting it right before writing any specs saves time later.

---

## Step 4 — Define your design tokens

`docs/design-tokens.md` is a template for defining the visual language of your project — colours, spacing, typography, and other design constants.

**If building by hand** — fill in `docs/design-tokens.md` with your token values, then implement them in `src/styles/tokens.scss` before writing any styles.

**If using an AI agent** — the agent must read `docs/design-tokens.md` before writing any styles. If the file is empty, it will stop and ask you to fill it in first.

> **If using an AI agent:** once you've filled in `docs/project-brief.md` and `docs/design-tokens.md`, prompt the agent to begin setup: *"Read `docs/project-brief.md` and complete the initial project setup."*

---

## Step 5 — Write a feature spec

Pick the first feature you want to build. Create a spec for it in `docs/features/`.

A feature describes what a user can do, not how it's built. Use `docs/features/dark-mode.md` as a reference for the format — it covers the overview, user stories, acceptance criteria, and which components are required.

Don't start writing component specs yet. Finish the feature spec first.

---

## Step 6 — Write your specs

Look at the "Components required" section of your feature spec. For each item listed, create a spec in the relevant directory using `docs/specs/_component-template.spec.md` as your starting point:

| Spec type | Spec location | Generated code location |
|-----------|--------------|------------------------|
| Component | `docs/specs/components/` | `src/components/<Name>/` |
| Page | `docs/specs/pages/` | `src/pages/<Name>/` |
| Layout | `docs/specs/layouts/` | `src/layouts/<Name>/` |

Use `docs/specs/components/button.spec.md` as a reference for a complete example.

Set the status to `Draft` while writing. Change it to `Ready` only when every section is complete. The agent will not proceed with a `Draft` spec.

---

## Step 7 — Build

Once the spec status is set to `Ready`, it's time to build.

**If building by hand** — use the spec as your blueprint. The interface, behaviour, states, accessibility requirements, and test cases are all defined. Work through them in order: interface first, tests next, then implementation.

**If using an AI agent** — open your agent and ask it to scaffold the implementation based on the spec. If you're using Claude Code, a custom command is included:

```bash
/create-component Button
```

> **If using an AI agent:**
>
> To scaffold a single spec:
> *"Read `docs/specs/components/button.spec.md` and scaffold the implementation."*
>
> To scaffold all ready specs at once:
> *"Read all specs in `docs/specs/` with a status of `Ready` and scaffold the implementation for each one."*

> **Note:** `/create-component` is a Claude Code-specific custom command defined in `.agents/claude/commands/create-component.md`. Other agents don't have this command out of the box — you'll need to prompt them directly, for example: *"Read the spec at `docs/specs/components/button.spec.md` and scaffold the implementation."*

The agent will:

1. Read the spec
2. Derive the interface
3. Write the tests first
4. Implement until all tests pass

If the agent stops and asks a question, that usually means the spec is ambiguous. Go back to the spec, clarify the relevant section, and re-run.

---

## Step 8 — Review the output

The generated code will appear in `src/` under the relevant directory *(see the table in Step 6)*. Check it against the spec:

- Does every `TC-##` in the spec have a corresponding passing test?
- Does the implementation match the behaviour described?
- Are the accessibility requirements met?

If something is wrong, update the spec first — then ask the agent to fix the implementation.

> ***NB**: Don't edit the implementation directly without updating the spec, or the two will drift apart. The spec is the source of truth, and the agent relies on it to generate the correct code. If they get out of sync, the agent's output becomes unpredictable.*

---

## Step 9 — Run it locally or deploy

How you run the project depends on your active framework selection in `docs/project-brief.md`.

**Vanilla + Vite:**

```bash
npm install
npm run dev
```

**React + Vite:**

```bash
npm install
npm run dev
```

**React + Next.js:**

```bash
npm install
npm run dev
```

**Svelte + Vite:**

```bash
npm install
npm run dev
```

**Svelte + SvelteKit:**

```bash
npm install
npm run dev
```

**Astro:**

```bash
npm install
npm run dev
```

**Eleventy:**

```bash
npm install
npx @11ty/eleventy --serve
```

For deployment, [Netlify](https://www.netlify.com) works well with all of these frameworks. Connect your Git repository, set the build command and output directory for your framework, and Netlify handles the rest. Refer to your chosen framework's documentation for the exact build settings.

---

## Step 10 — Iterate

Repeat Steps 5–8 for each feature. As the project grows, update `docs/project-brief.md` with any new conventions or constraints the agent needs to know about.

---

> ### The spec is the source of truth
>
> The spec files are the living documentation of your project.
> **Keep them up to date and the agent stays useful. Let them drift and the agent becomes unpredictable.**
>
> If the output isn't right, the spec is always the first place to look.
