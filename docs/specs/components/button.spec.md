# Component Spec: Button

**Status:** Ready

---

## Purpose

> A single paragraph describing what problem this component solves, who uses it,
> and when. Avoid describing how it works — describe why it exists.

A reusable, accessible button covering every interactive call-to-action across the
application. Must support loading and disabled states and be usable by any team
without additional configuration.

---

## Interface

The props, attributes, and events that define how this component is used.
The agent will derive the implementation interface directly from this section.

### Props / Attributes

| Name | Type | Required | Default | Description |
|------|------|:--------:|---------|-------------|
| `label` | string | ✓ | — | Visible button text |
| `variant` | `primary` / `secondary` / `danger` / `ghost` | | `primary` | Visual style |
| `size` | `sm` / `md` / `lg` | | `md` | Size preset |
| `disabled` | boolean | | `false` | Prevents interaction |
| `loading` | boolean | | `false` | Shows spinner; prevents interaction |
| `type` | `button` / `submit` / `reset` | | `button` | HTML button type |

### Events / Callbacks

| Event | Fires when |
|-------|-----------|
| click / onClick / on:click | User clicks and button is neither disabled nor loading |

---

## Behaviour

How the component behaves on first render, across its different states, and in
response to user interaction.

### Default / initial state

Renders as a native `<button>` element with the `primary` variant and `md` size.
Fully interactive.

### States

| State | Trigger | Result |
|-------|---------|--------|
| default | — | Fully interactive |
| hover | Pointer over | Visual feedback; no layout shift |
| focus | Keyboard focus | Visible ring (3:1 contrast min) |
| disabled | `disabled` is true | HTML `disabled` attr + `aria-disabled="true"`; click blocked |
| loading | `loading` is true | Spinner inline; `aria-busy="true"`; click blocked |

### Interaction rules

- When `loading` is true → spinner shown; label remains visible but muted
- When `disabled` OR `loading` → click event must never fire
- `type="submit"` inside a `<form>` → form submits normally via the browser

---

## Accessibility

The accessibility requirements this component must meet. The agent must not
consider the component complete until all of these are satisfied.

- Must use a native `<button>` element — never a `<div>` or `<span>`
- `disabled`: set both the HTML attribute AND `aria-disabled="true"`
- `loading`: set `aria-busy="true"`
- Focus ring: minimum 3:1 contrast (WCAG 2.1 AA)
- Spinner: `aria-hidden="true"`

---

## Error handling

How the component should behave when something goes wrong.

- If the click handler throws, do not catch — let the error bubble
- Invalid `variant` falls back to `primary` with a `console.warn` in dev only

---

## Test cases

The agent will generate one test function per entry. IDs must be unique within
this spec and must match the test file exactly.

- [ ] **TC-01** — Renders a `<button>` with only the required `label`
- [ ] **TC-02** — Applies the correct CSS class for each `variant` value
- [ ] **TC-03** — Applies the correct CSS class for each `size` value
- [ ] **TC-04** — Click event fires when the button is enabled
- [ ] **TC-05** — Click event does NOT fire when `disabled` is true
- [ ] **TC-06** — Click event does NOT fire when `loading` is true
- [ ] **TC-07** — Spinner rendered and `aria-busy="true"` set when `loading` is true
- [ ] **TC-08** — `aria-disabled="true"` present when `disabled` is true
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

How this component is implemented depends on the active framework selection in
`docs/project-brief.md`.

**Vanilla:**

```html
<button class="btn btn--primary" type="button">Save changes</button>
```

**Astro:**

```astro
<Button label="Save changes" variant="primary" />
```

**React:**

```jsx
<Button label="Save changes" variant="primary" onClick={handleSave} />
```

**Svelte:**

```svelte
<Button label="Save changes" variant="primary" on:click={handleSave} />
```

---

## Notes for AI implementation

Additional context, constraints, and implementation guidance that the agent
should be aware of before writing any code.

- CSS: import from `./Button.css` or `./Button.scss` depending on active styles selection
- Spinner: `src/assets/spinner.svg` — import and inline; do not use `<img>`
- No animation libraries — CSS only
