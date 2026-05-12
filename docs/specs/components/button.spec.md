# Component Spec: Button

**Status:** Ready

> *Type annotations in this spec apply when TypeScript is the active language.
> CSS imports are `.css` or `.scss` depending on the active styles selection in `docs/project-brief.md`.*

---

## Purpose

A single paragraph describing what problem this component solves, who uses it,
and when. Avoid describing how it works — describe why it exists.

A reusable, accessible button covering every interactive call-to-action across the
application. Must support loading and disabled states and be usable by any team
without additional configuration.

---

## Interface

The props, events, and public methods that define how this component is used.
The agent will derive the interface directly from this section.

### Props

| Prop | Type | Required | Default | Description |
|------|------|:--------:|---------|-------------|
| `label` | `string` | ✓ | — | Visible button text |
| `variant` | `'primary' \| 'secondary' \| 'danger' \| 'ghost'` | | `'primary'` | Visual style |
| `size` | `'sm' \| 'md' \| 'lg'` | | `'md'` | Size preset |
| `disabled` | `boolean` | | `false` | Prevents interaction |
| `loading` | `boolean` | | `false` | Shows spinner; prevents interaction |
| `type` | `'button' \| 'submit' \| 'reset'` | | `'button'` | HTML button type |
| `onClick` | function | | — | Click handler; receives the click event |
| `ariaLabel` | `string` | | — | Overrides the accessible label |

### Events / Callbacks

| Event | Fires when |
|-------|-----------|
| `onClick` | User clicks and button is neither disabled nor loading |

---

## Behaviour

How the component behaves on first render, across its different states, and in
response to user interaction.

### Default / initial state
Renders as a native `<button>` with `type="button"`, the `primary` variant class,
and the `md` size class. Fully interactive.

### States

| State | Trigger | Result |
|-------|---------|--------|
| default | — | Fully interactive |
| hover | Pointer over | Visual feedback; no layout shift |
| focus | Keyboard focus | Visible ring (3:1 contrast min) |
| disabled | `disabled={true}` | HTML `disabled` + `aria-disabled="true"`; click blocked |
| loading | `loading={true}` | Spinner inline; `aria-busy="true"`; click blocked |

### Interaction rules
- When `loading` is `true` → spinner shown; label remains visible but muted
- When `disabled` OR `loading` → `onClick` must never fire
- `type="submit"` inside a `<form>` → form submits normally via the browser

---

## Accessibility

The accessibility requirements this component must meet. The agent must not
consider the component complete until all of these are satisfied.

- Must use a native `<button>` — never a `<div>` or `<span>`
- `disabled`: set both the HTML attribute AND `aria-disabled="true"`
- `loading`: set `aria-busy="true"`
- Focus ring: minimum 3:1 contrast (WCAG 2.1 AA)
- Spinner: `aria-hidden="true"`

---

## Error handling

How the component should behave when something goes wrong.

- If `onClick` throws, do not catch — let the error bubble
- Invalid `variant` falls back to `'primary'` with a `console.warn` in dev only

---

## Test cases

The agent will generate one test function per entry. IDs must be unique within
this spec and must match the test file exactly.

- [ ] **TC-01** — Renders a `<button>` with only the required `label` prop
- [ ] **TC-02** — Applies the correct CSS class for each `variant` value
- [ ] **TC-03** — Applies the correct CSS class for each `size` value
- [ ] **TC-04** — `onClick` fires when the button is enabled and clicked
- [ ] **TC-05** — `onClick` does NOT fire when `disabled={true}`
- [ ] **TC-06** — `onClick` does NOT fire when `loading={true}`
- [ ] **TC-07** — Spinner rendered and `aria-busy="true"` set when `loading={true}`
- [ ] **TC-08** — `aria-disabled="true"` present when `disabled={true}`
- [ ] **TC-09** — `type="submit"` triggers form submission
- [ ] **TC-10** — `ariaLabel` prop sets `aria-label` on the element

---

## Out of scope

Explicitly listing what this component does NOT cover prevents scope creep and
helps the agent avoid building more than is required.

- Icon-only buttons → use `IconButton` component
- Navigation / anchor behaviour → use `LinkButton` component
- Button groups → use `ButtonGroup` component

---

## Example usage

A short code example showing how the component is used in practice.

```js
import { Button } from './Button';

const saveBtn = new Button({
  label: 'Save changes',
  onClick: (e) => handleSave(e),
});

const deleteBtn = new Button({
  label: 'Delete account',
  variant: 'danger',
  loading: isDeleting,
});
```

---

## Notes for AI implementation

Additional context, constraints, and implementation guidance that the agent
should be aware of before writing any code.

- CSS: import from `./Button.css` or `./Button.scss` depending on active styles selection
- Spinner: `src/assets/spinner.svg` — import and inline; do not use `<img>`
- No animation libraries — CSS only
