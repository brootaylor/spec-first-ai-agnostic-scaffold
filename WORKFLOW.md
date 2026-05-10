# WORKFLOW.md

A step-by-step guide to using this scaffold to build a web project with an "Ai" coding agent.

---

## Step 1 — Set up the scaffold

Copy the scaffold into your project directory. Create any directories that don't exist yet:

```bash
docs/features/
docs/specs/components/
docs/specs/pages/
docs/specs/layouts/
src/components/
src/pages/
src/layouts/
.agents/claude/commands/
.agents/cursor/
.agents/copilot/
```

Commit everything to Git before you do anything else. This gives you a clean baseline to return to.

---

## Step 2 — Configure your agent

Open `.agents/<your-agent>/` and follow the setup notes in that directory to point your tool at the config file.

For example, if you're using Claude Code:

```bash
ln -s .agents/claude/CLAUDE.md CLAUDE.md
```

See `SETUP.md` for a full explanation of how agents are configured in this scaffold.

---

## Step 3 — Fill in `ai-context.md`

Open `docs/ai-context.md` and do two things:

**Describe your project** — replace the placeholder under "What this project is" with a plain description of what you're building and who it's for.

**Choose your stack** — mark exactly one option per category as `[active]` in the Stack section. For example:

| Framework                | Active     |
|--------------------------|------------|
| Eleventy (11ty)          |            |
| Astro                    |            |
| Vanilla *(no framework)* | `[active]` |

This is the first thing the agent reads. Getting it right before writing any specs saves time later.

---

## Step 4 — Write a feature spec

Pick the first feature you want to build. Create a spec for it in `docs/features/`.

A feature describes what a user can do, not how it's built. Use `docs/features/dark-mode.md` as a reference for the format — it covers the overview, user stories, acceptance criteria, and which components are required.

Don't start writing component specs yet. Finish the feature spec first.

---

## Step 5 — Write your specs

Look at the "Components required" section of your feature spec. For each item listed, create a spec in the relevant directory using `docs/specs/_component-template.spec.md` as your starting point:

| Spec type | Spec location | Generated code location |
|-----------|--------------|------------------------|
| Component | `docs/specs/components/` | `src/components/<Name>/` |
| Page | `docs/specs/pages/` | `src/pages/<Name>/` |
| Layout | `docs/specs/layouts/` | `src/layouts/<Name>/` |

Use `docs/specs/components/button.spec.md` as a reference for a complete example.

Set the status to `Draft` while writing. Change it to `Ready` only when every section is complete. The agent will not proceed with a `Draft` spec.

---

## Step 6 — Run the agent

Open your agent tool and ask it to scaffold the implementation based on the spec. If you're using Claude Code, a custom command is included:

```bash
/create-component Button
```

> **Note:** `/create-component` is a Claude Code-specific custom command defined in `.agents/claude/commands/create-component.md`. Other agents don't have this command out of the box — you'll need to prompt them directly, for example: *"Read the spec at `docs/specs/components/button.spec.md` and scaffold the implementation."*

The agent will:

1. Read the spec
2. Derive the interface
3. Write the tests first
4. Implement until all tests pass

If the agent stops and asks a question, that usually means the spec is ambiguous. Go back to the spec, clarify the relevant section, and re-run.

---

## Step 7 — Review the output

The generated code will appear in `src/` under the relevant directory *(see the table in Step 5)*. Check it against the spec:

- Does every `TC-##` in the spec have a corresponding passing test?
- Does the implementation match the behaviour described?
- Are the accessibility requirements met?

If something is wrong, update the spec first — then ask the agent to fix the implementation.

> ***NB**: Don't edit the implementation directly without updating the spec, or the two will drift apart.* The spec is the source of truth, and the agent relies on it to generate the correct code. If they get out of sync, the agent's output becomes unpredictable.

---

## Step 8 — Run it locally or deploy

How you run the project depends on your active stack selection in `docs/ai-context.md`.

**Vanilla + Vite:**

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

For deployment, [Netlify](https://www.netlify.com) works well with all three. Connect your Git repository, set the build command and output directory for your stack, and Netlify handles the rest. Refer to your chosen framework's documentation for the exact build settings.

---

## Step 9 — Iterate

Repeat Steps 4–7 for each feature. As the project grows, update `docs/ai-context.md` with any new conventions or constraints the agent needs to know about.

---

> ### The spec is the source of truth
>
> The spec files are the living documentation of your project.
> **Keep them up to date and the agent stays useful. Let them drift and the agent becomes unpredictable.**
>
> If the output isn't right, the spec is always the first place to look.
