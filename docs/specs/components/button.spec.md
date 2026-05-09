# Component Spec: Button

**Status:** Ready for implementation
**Last updated:** 2025-01

---

## Purpose

A reusable, accessible button covering every interactive call-to-action across the
application. Must support loading and disabled states and be usable by any team
without additional configuration.

---

## Interface

### Props

| Prop | Type | Required | Default | Description |
|------|------|:--------:|---------|-------------|
| `label` | `string` | ✓ | — | Visible button text |
| `variant` | `'primary' \| 'secondary' \| 'danger' \| 'ghost'` | | `'primary'` | Visual style |
| `size` | `'sm' \| 'md' \| 'lg'` | | `'md'` | Size preset |
| `disabled` | `boolean` | | `false` | Prevents interaction |
| `loading` | `boolean` | | `false` | Shows spinner; prevents interaction |
| `type` | `'button' \| 'submit' \| 'reset'` | | `'button'` | HTML button type |
| `onClick` | `(event: MouseEvent) => void` | | — | Click handler |
| `ariaLabel` | `string` | | — | Overrides the accessible label |

### Events

| Event | Payload | Fires when |
|-------|---------|-----------|
| `onClick` | `MouseEvent` | User clicks and button is neither disabled nor loading |

---

## Behaviour

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

- Must use a native `<button>` — never a `<div>` or `<span>`
- `disabled`: set both the HTML attribute AND `aria-disabled="true"`
- `loading`: set `aria-busy="true"`
- Focus ring: minimum 3:1 contrast (WCAG 2.1 AA)
- Spinner: `aria-hidden="true"`

---

## Error handling

- If `onClick` throws, do not catch — let the error bubble
- Invalid `variant` falls back to `'primary'` with a `console.warn` in dev only

---

## Test cases

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

- Icon-only buttons → use `IconButton` component
- Navigation / anchor behaviour → use `LinkButton` component
- Button groups → use `ButtonGroup` component

---

## Example usage

```ts
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

- CSS Modules: import from `./Button.module.css`
- Spinner: `src/assets/spinner.svg` — import and inline; do not use `<img>`
- No animation libraries — CSS only
- Class names must match design tokens exactly:
  `btn`, `btn--primary`, `btn--loading`, etc. (see `docs/design-tokens.md`)
