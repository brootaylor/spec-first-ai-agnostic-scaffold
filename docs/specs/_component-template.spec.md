# Component Spec: [ComponentName]

**Status:** Draft

---

## Status key

The status of this spec determines whether an agent may proceed with implementation.

| Status | Meaning |
|--------|---------|
| `Draft` | Spec is incomplete — do not implement |
| `Ready` | Spec is complete — agent may proceed |
| `In progress` | Currently being implemented |
| `Complete` | Implemented and tested |

---

## Purpose

A single paragraph describing what problem this component solves, who uses it,
and when. Avoid describing how it works — describe why it exists.

_Replace this with your component's purpose._

---

## Interface

The props, attributes, and events that define how this component is used.
The agent will derive the implementation interface directly from this section.

### Props / Attributes

| Name | Type | Required | Default | Description |
|------|------|:--------:|---------|-------------|
| `prop1` | string | ✓ | — | … |
| `prop2` | boolean | | `false` | … |

### Events / Callbacks

| Event | Fires when |
|-------|------------|
| change / onChange / on:change | … |

### Public methods _(if applicable)_

Document any methods exposed via a ref or returned from the constructor.

---

## Behaviour

How the component behaves on first render, across its different states, and in
response to user interaction.

### Default / initial state

Describe exactly what the component renders and does on first mount with only
the required props supplied.

### States

| State | Trigger | Visual / functional result |
|-------|---------|---------------------------|
| state-a | … | … |
| state-b | … | … |

### Interaction rules

- When the user does **X** → **Y** should happen
- When condition **Z** is true → component should …

---

## Accessibility

The accessibility requirements this component must meet. The agent must not
consider the component complete until all of these are satisfied.

- Keyboard navigation requirements
- Required ARIA roles, labels, and live regions
- Focus management after actions
- Contrast and motion requirements

---

## Error handling

How the component should behave when something goes wrong.

- What happens if required props are missing or invalid?
- What happens when an async operation fails?

---

## Test cases

The agent will generate one test function per entry. IDs must be unique within
this spec and must match the test file exactly.

- [ ] **TC-01** — Renders with only required props
- [ ] **TC-02** — …

---

## Out of scope

Explicitly listing what this component does NOT cover prevents scope creep and
helps the agent avoid building more than is required.

- …

---

## Example usage

How this component is implemented depends on the active framework selection in
`docs/project-brief.md`.

**Vanilla:**

```html
<div class="component-name">…</div>
```

**Astro:**

```astro
<ComponentName prop1="value" />
```

**React:**

```jsx
<ComponentName prop1="value" onChange={handleChange} />
```

**Svelte:**

```svelte
<ComponentName prop1="value" on:change={handleChange} />
```

---

## Notes for AI implementation

Additional context, constraints, and implementation guidance that the agent
should be aware of before writing any code.

- Gotchas, specific helper files to use, CSS class naming conventions, links to related specs.
