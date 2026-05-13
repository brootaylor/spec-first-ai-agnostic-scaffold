# Feature: Storybook

**Status:** Draft

---

## Overview

Add Storybook to the project to develop, document, and showcase UI components
in isolation. This makes it easier to build and review components independently
of the full application, and provides a living style guide for the design system.

> **Note:** This spec covers React, Svelte, and plain JavaScript as worked examples.
> Storybook supports other frameworks too — and a handcrafted Storybook instance
> can be configured to suit any project's specific needs. See the
> [Storybook documentation](https://storybook.js.org/docs) for the full list of
> supported frameworks and configuration options.

---

## Key

A reference for the prefixes used throughout this document.

| Prefix | Stands for | Description |
|--------|------------|-------------|
| `US-##` | User Story | A feature requirement from the user's perspective |
| `AC-##` | Acceptance Criteria | A condition that must be met for the story to be complete |

---

## User stories

Each user story describes a requirement from the user's perspective, followed by
the acceptance criteria that must be met for it to be considered complete.

### US-01 — Component development in isolation

> As a developer, I want to build and view components in isolation so I can
> develop and test them without needing the full application running.

- [ ] **AC-01** — Storybook runs locally via `npm run storybook`
- [ ] **AC-02** — Each component has at least one story showing its default state
- [ ] **AC-03** — Component props / attributes can be adjusted interactively in the Storybook UI

### US-02 — Component documentation

> As a developer or designer, I want to see documentation for each component
> alongside its visual representation so I can understand how to use it.

- [ ] **AC-01** — Each story includes a description of the component and its variants
- [ ] **AC-02** — Props / attributes are documented in the Storybook controls panel
- [ ] **AC-03** — Usage examples are visible alongside the rendered component

### US-03 — Design system showcase

> As a stakeholder, I want to browse all components and patterns in one place
> so I can review the design system without needing access to the codebase.

- [ ] **AC-01** — Storybook can be built as a static site via `npm run build-storybook`
- [ ] **AC-02** — The static build can be deployed independently of the main project
- [ ] **AC-03** — All components are browsable and searchable in the built output

---

## Out of scope

Explicitly listing what this feature does NOT cover prevents scope creep and
helps the agent avoid building more than is required.

- Visual regression testing (e.g. Chromatic)
- Accessibility testing addons
- Automated story generation
- Integration with a CMS or design tool

---

## Setup guidance

The following covers React, Svelte, and plain JavaScript as worked examples. Storybook
supports other options too — refer to the
[Storybook documentation](https://storybook.js.org/docs) for setup instructions.
A handcrafted Storybook instance can also be configured independently of these examples.

### React

```bash
npx storybook@latest init
```

Storybook detects React automatically. Stories use `.stories.jsx` or `.stories.tsx`.

```jsx
// src/components/Button/Button.stories.jsx
export default {
  title: 'Components/Button',
  component: Button,
};

export const Primary = {
  args: { label: 'Click me', variant: 'primary' },
};
```

### Svelte

```bash
npx storybook@latest init
```

Storybook detects Svelte automatically. Stories use `.stories.js` or `.stories.svelte`.

```js
// src/components/Button/Button.stories.js
import Button from './Button.svelte';

export default {
  title: 'Components/Button',
  component: Button,
};

export const Primary = {
  args: { label: 'Click me', variant: 'primary' },
};
```

### Plain JavaScript

```bash
npx storybook@latest init --type html
```

Stories use `.stories.js` and return HTML strings or DOM elements.

```js
// src/components/Button/Button.stories.js
export default {
  title: 'Components/Button',
};

export const Primary = () => `
  <button class="btn btn--primary">Click me</button>
`;
```

---

## Notes for AI agents

- Run `npx storybook@latest init` and let Storybook auto-detect the active framework
- If auto-detection fails, pass the `--type` flag manually based on the active framework selection in `docs/project-brief.md`
- Add a `storybook-static/` entry to `.gitignore` after setup
- Add the following scripts to `package.json`:
  - `"storybook": "storybook dev -p 6006"`
  - `"build-storybook": "storybook build"`
- Write at least one story per component that has a spec with status `Ready` or `Complete`
- Story files should be co-located with the component: `src/components/<Name>/<Name>.stories.{js|jsx|ts|tsx|svelte}`
