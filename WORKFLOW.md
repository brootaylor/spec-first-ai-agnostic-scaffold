# WORKFLOW.md

A step-by-step guide to using this scaffold to build a web project — by hand or with an AI coding agent.

---

## Prerequisites

Before you begin, make sure you have the following installed:

> **Note:** A GitHub account is required if you want to use the "Use this template" button on the repository page. Cloning or downloading the ZIP does not require one.

**Always required:**

| Tool | Notes |
|------|-------|
| A terminal | Required to run commands throughout this workflow. macOS and Linux have one built in. On Windows, [Git Bash](https://gitforwindows.org) or [Windows Terminal](https://aka.ms/terminal) are good options |
| [Git](https://git-scm.com) | Required to clone this scaffold. Recommended for version control throughout development |
| [Node.js](https://nodejs.org) | Required by most tooling — install the LTS version |
| [npm](https://www.npmjs.com) | Comes with Node.js |
| A code editor | [VS Code](https://code.visualstudio.com) is a good option |

---

## Step 1 — Set up the scaffold

> **Before doing anything else — commit everything to Git.** This gives you a clean baseline to return to.

**Comes with the scaffold — no action needed:**

```bash
README.md
WORKFLOW.md
AGENTS.md
LICENSE
package.json
.gitignore
.nvmrc
.markdownlint.json
docs/project-brief.md
docs/design-tokens.md
docs/service-worker.md
docs/storybook.md
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

**If building by hand:** these directories can be created as needed:

```bash
src/components/
src/pages/
src/layouts/
```

**If using an AI agent:** the agent will create any missing directories as needed when scaffolding components, pages, and layouts.

---

## Step 2 — Configure your agent

> If you're not using an agent, skip this step.

Before setting up your agent, make sure you have what it needs:

| Agent | Prerequisites |
|-------|--------------|
| Claude Code | Node.js + an [Anthropic API key](https://console.anthropic.com) |
| Cursor | Download the [Cursor app](https://cursor.sh) |
| GitHub Copilot | A GitHub account with [Copilot access](https://github.com/features/copilot) + the relevant IDE's extension |

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

**Choose your stack** — mark exactly one option per category as `[active]`. Categories to configure:

- Framework
- Language
- Styles
- Unit testing
- E2E testing
- Build *(Vanilla only)*
- Service worker *(optional — defaults to None)*
- Storybook *(optional — defaults to None)*

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

## Step 4 — Complete your project setup

Now that your stack is selected, `package.json` needs to be populated with the correct dependencies.

**If building by hand:**

- Set up `package.json` and any required config files (e.g. `vite.config.js`, `jest.config.js`) based on your active stack selections
- Check your chosen framework's documentation for the recommended Node.js version and update `.nvmrc` accordingly
- Update the stack-specific section of `.gitignore` with any entries required by your chosen framework (e.g. `dist/` for Vite, `_site/` for Eleventy, `.astro/` for Astro)
- Refer to your chosen framework's documentation for the exact setup

**If using an AI agent:** prompt the agent to begin setup:

*"Read `docs/project-brief.md` and complete the initial project setup."*

> **Note:** This covers `package.json`, config files, `.nvmrc`, and `.gitignore` only. Design tokens and specs come later.

The agent will:

- Populate `package.json` with the correct scripts and dependencies
- Generate any required config files
- Populate `.nvmrc` with the correct Node.js version for the active framework
- Update the stack-specific section of `.gitignore`

Two default starting files are included for the Vanilla + Vite stack:

- `src/index.html` — the default home page Vite serves
- `src/scripts/main.js` — the JavaScript file referenced by `index.html`

If building with React or Svelte, these files are also used — `main.js` needs to be updated to mount the app for the active framework. If you switch to Astro or Eleventy, remove these two files — those frameworks manage their own pages and templating.

> **Commit your work.** Once setup is complete and dependencies are in place, commit before moving on.

---

## Step 5 — Define your design tokens

`docs/design-tokens.md` is a template for defining the visual language of your project — colours, spacing, typography, and other design constants.

**If building by hand:**

- Fill in `docs/design-tokens.md` with your token values
- Implement the values in `src/styles/tokens.scss` before writing any styles

**If using an AI agent:**

- Fill in `docs/design-tokens.md` with your token values first
- Then prompt the agent: *"Read `docs/design-tokens.md` and implement the values in `src/styles/tokens.scss`."*
- If the file is empty, the agent will stop and ask you to fill it in first

> **Commit your work.** Once your tokens are defined and implemented, commit before moving on.

---

## Step 6 — Write a feature spec

Pick the first feature you want to build. Create a spec for it in `docs/features/`.

A feature describes what a user can do, not how it's built. Use `docs/features/dark-mode.md` as a reference for the format — it covers the overview, user stories, acceptance criteria, and which components are required.

> **Note:** `docs/features/` is for user-facing feature specs only. Technical configuration docs like service worker and Storybook live directly in `docs/`.

Don't start writing component specs yet. Finish the feature spec first.

---

## Step 7 — Write your specs

Look at the "Components required" section of your feature spec. For each item listed, create a spec in the relevant directory using `docs/specs/_component-template.spec.md` as your starting point:

| Spec type | Spec location | Generated code location |
|-----------|--------------|------------------------|
| Component | `docs/specs/components/` | `src/components/<Name>/` |
| Page | `docs/specs/pages/` | `src/pages/<Name>/` |
| Layout | `docs/specs/layouts/` | `src/layouts/<Name>/` |

Use `docs/specs/components/button.spec.md` as a reference for a complete example.

Set the status to `Draft` while writing. Change it to `Ready` only when every section is complete. The agent will not proceed with a `Draft` spec.

---

## Step 8 — Build

Once the spec status is set to `Ready`, it's time to build.

**If building by hand:**

- Use the spec as your blueprint
- The interface, behaviour, states, accessibility requirements, and test cases are all defined
- Work through them in order: interface first, tests next, then implementation

**If using an AI agent:**

To scaffold a single spec, prompt the agent:

*"Read `docs/specs/components/button.spec.md` and scaffold the implementation."*

To scaffold all ready specs at once:

*"Read all specs in `docs/specs/` with a status of `Ready` and scaffold the implementation for each one."*

If you're using Claude Code, a custom command is also available as a shorthand:

```bash
/create-component Button
```

> **Note:** `/create-component` is a Claude Code-specific custom command defined in `.agents/claude/commands/create-component.md`. Other agents don't support it — use the prompt examples above instead.

The agent will:

1. Read the spec
2. Derive the interface
3. Write the tests first
4. Implement until all tests pass

If the agent stops and asks a question, that usually means the spec is ambiguous. Go back to the spec, clarify the relevant section, and re-run.

---

## Step 9 — Review the output

The generated code will appear in `src/` under the relevant directory *(see the table in Step 7)*. Check it against the spec:

- Does every `TC-##` in the spec have a corresponding passing test?
- Does the implementation match the behaviour described?
- Are the accessibility requirements met?

**If something is wrong**, there are two likely causes:

- **The spec is ambiguous** — update the spec first to clarify, then ask the agent to fix the implementation.
- **The spec is clear but the output is incorrect** — re-prompt the agent with the relevant section highlighted: *"Re-read the Behaviour section of `docs/specs/components/button.spec.md` and correct the implementation."*

> **Note:** Don't edit the implementation directly without updating the spec, or the two will drift apart. The spec is the source of truth, and the agent relies on it to generate correct code. If they get out of sync, the agent's output becomes unpredictable.

Once everything checks out, update the spec status to `Complete`.

> **Commit your work.** Once the spec is marked `Complete` and all tests are passing, commit before moving on.

---

## Step 10 — Run it locally or deploy

All frameworks install dependencies via `npm install`. Most are then started with `npm run dev` — Eleventy is the exception:

**Most frameworks (Vanilla + Vite, React, Svelte, Astro):**

```bash
npm install
npm run dev
```

**Eleventy:**

```bash
npm install
npx @11ty/eleventy --serve
```

For deployment, [Netlify](https://www.netlify.com) and [Vercel](https://vercel.com) both work well with all of these frameworks. Connect your Git repository, set the build command and output directory for your framework, and they handle the rest. Refer to your chosen framework's documentation for the exact build settings.

---

## Step 11 — Iterate

Once a spec is marked `Complete` and committed, return to Step 6 and repeat the cycle for the next feature — writing the feature spec, then the component specs, building, and reviewing.

As the project grows, update `docs/project-brief.md` with any new conventions or constraints the agent needs to know about.

---

## The spec is the source of truth

The spec files are the living documentation of your project. **Keep them up to date and the agent stays useful. Let them drift and the agent becomes unpredictable.**

If the output isn't right, the spec is always the first place to look.
