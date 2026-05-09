# Component Spec: [ComponentName]

> **Instructions for spec authors**
> Fill in every section before handing this to an AI agent or starting implementation.
> Vague or missing sections will produce vague or incorrect code.
> Delete this callout block when the spec is complete.

---

## Purpose

_One short paragraph. What problem does this component solve? Who uses it, and when?
Avoid describing how it works — describe why it exists._

---

## Interface

### Props / Parameters

| Prop | Type | Required | Default | Description |
|------|------|:--------:|---------|-------------|
| `prop1` | `string` | ✓ | — | … |
| `prop2` | `boolean` | | `false` | … |

### Events / Callbacks

| Event | Payload type | Fires when |
|-------|-------------|------------|
| `onFoo` | `FooEvent` | … |

### Public methods _(if applicable)_

Document any methods exposed via a ref or returned from the constructor.

---

## Behaviour

### Default / initial state
Describe exactly what the component renders and does on first mount with only the
required props supplied.

### States

| State | Trigger | Visual / functional result |
|-------|---------|---------------------------|
| loading | `loading={true}` | … |
| error | `error` prop set | … |
| empty | data array is `[]` | … |
| populated | data array has items | … |

### Interaction rules
- When the user does **X** → **Y** should happen
- When condition **Z** is true → component should …

---

## Accessibility

- Keyboard navigation requirements
- Required ARIA roles, labels, and live regions
- Focus management after actions
- Contrast and motion requirements

---

## Error handling

- What happens if required props are missing or invalid?
- What happens when an async operation fails?

---

## Test cases

_The AI will generate one test function per entry. IDs must be unique within this spec._

- [ ] **TC-01** — Renders with only required props
- [ ] **TC-02** — …

---

## Out of scope

_Explicitly list what this component does NOT do._

---

## Example usage

```ts
import { ComponentName } from './ComponentName';

const example = new ComponentName({ prop1: 'value' });
```

---

## Notes for AI implementation

_Gotchas, specific helper files to use, CSS class naming conventions,
links to related specs._
