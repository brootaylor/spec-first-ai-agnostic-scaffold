# Component Spec: ThemeToggle

**Status:** Draft

> *Type annotations in this spec apply when TypeScript is the active language.
> CSS imports are `.css` or `.scss` depending on the active styles selection in `docs/project-brief.md`.*

---

## Purpose

> A single paragraph describing what problem this component solves, who uses it,
> and when. Avoid describing how it works — describe why it exists.

A toggle control that allows users to switch between light and dark colour
schemes. It reflects the current scheme and updates it immediately when
activated. Used in the main navigation so it is accessible from every page.

---

## Interface

The props, events, and public methods that define how this component is used.
The agent will derive the interface directly from this section.

### Props / Parameters

| Prop | Type | Required | Default | Description |
|------|------|:--------:|---------|-------------|
| `initialTheme` | `'light' \| 'dark'` | | `'light'` | The theme to apply on first render if no stored preference exists |

### Events / Callbacks

| Event | Payload | Fires when |
|-------|---------|------------|
| `onChange` | `'light' \| 'dark'` | The user activates the toggle |

---

## Behaviour

How the component behaves on first render, across its different states, and in
response to user interaction.

### Default / initial state

On first render, the component checks `localStorage` for a stored `color-scheme`
preference. If found, it applies that. If not, it checks the OS preference via
`prefers-color-scheme`. If neither is set, it falls back to `initialTheme`.
The current scheme is reflected visually in the toggle.

### States

| State | Trigger | Visual / functional result |
|-------|---------|---------------------------|
| light | Theme is `'light'` | Toggle reflects light mode is active |
| dark | Theme is `'dark'` | Toggle reflects dark mode is active |

### Interaction rules

- When the user activates the toggle → the theme switches immediately
- When the theme switches → `data-theme` on the root `<html>` element is updated
- When the theme switches → the new preference is saved to `localStorage` under the key `color-scheme`
- When the theme switches → `onChange` fires with the new theme value

---

## Accessibility

The accessibility requirements this component must meet. The agent must not
consider the component complete until all of these are satisfied.

- Must use a native `<button>` element
- Must have an `aria-label` that reflects the current state, e.g. `"Switch to dark mode"` or `"Switch to light mode"`
- Must be keyboard operable — activatable with `Enter` and `Space`
- Focus ring must meet WCAG 2.1 AA contrast requirements
- Icon or visual indicator must not be the only means of conveying the current state

---

## Error handling

How the component should behave when something goes wrong.

- If `localStorage` is unavailable, fall back to OS preference or `initialTheme` silently — do not throw
- If an invalid `initialTheme` value is passed, fall back to `'light'` and emit a `console.warn` in development only

---

## Test cases

The agent will generate one test function per entry. IDs must be unique within
this spec and must match the test file exactly.

- [ ] **TC-01** — Renders with no props and defaults to `initialTheme`
- [ ] **TC-02** — Applies stored `localStorage` preference on first render
- [ ] **TC-03** — Applies OS `prefers-color-scheme` when no stored preference exists
- [ ] **TC-04** — Activating the toggle switches the theme
- [ ] **TC-05** — Activating the toggle updates `data-theme` on the root `<html>` element
- [ ] **TC-06** — Activating the toggle saves the new preference to `localStorage`
- [ ] **TC-07** — `onChange` fires with the correct theme value when toggled
- [ ] **TC-08** — `aria-label` reflects the current state correctly
- [ ] **TC-09** — Falls back gracefully when `localStorage` is unavailable

---

## Out of scope

Explicitly listing what this component does NOT cover prevents scope creep and
helps the agent avoid building more than is required.

- Displaying a text label alongside the toggle — icon only
- Animating the theme transition
- Supporting more than two themes

---

## Example usage

A short code example showing how the component is used in practice.

```js
import { ThemeToggle } from './ThemeToggle';

const toggle = new ThemeToggle({
  initialTheme: 'light',
  onChange: (theme) => console.log('Theme changed to:', theme),
});
```

---

## Notes for AI implementation

Additional context, constraints, and implementation guidance that the agent
should be aware of before writing any code.

- Read `docs/features/dark-mode.md` for full feature context before implementing
- Apply the theme by setting `document.documentElement.setAttribute('data-theme', theme)`
- All colour values in the app use CSS custom properties scoped to `[data-theme="light"]` and `[data-theme="dark"]` — this component only needs to toggle the attribute
- CSS: import from `./ThemeToggle.css` or `./ThemeToggle.scss` depending on active styles selection
- No animation libraries — CSS transitions only
