# Page Spec: Dashboard

**Status:** Draft

> *Type annotations in this spec apply when TypeScript is the active language.
> CSS imports are `.css` or `.scss` depending on the active styles selection in `docs/ai-context.md`.*

---

## Purpose

A single paragraph describing what problem this page solves, who uses it,
and when. Avoid describing how it looks — describe why it exists.

The main landing page for authenticated users. Provides an overview of the
user's account, recent activity, and quick access to key actions.

---

## Route

| Route | Access |
|-------|--------|
| `/dashboard` | Authenticated users only |

---

## Layout

The layout this page uses.

| Layout | Spec |
|--------|------|
| `MainLayout` | `docs/specs/layouts/main-layout.spec.md` |

---

## Components

The components this page is composed of. Each must have a spec in
`docs/specs/components/` before implementation can begin.

| Component | Spec |
|-----------|------|
| `ComponentA` | `docs/specs/components/component-a.spec.md` |
| `ComponentB` | `docs/specs/components/component-b.spec.md` |

---

## Behaviour

How the page behaves on first load and in response to user interaction.

### Default / initial state

Describe what the page renders and does when first visited by an authenticated user.

### States

| State | Trigger | Result |
|-------|---------|--------|
| loading | Page is fetching data | … |
| error | Data fetch fails | … |
| populated | Data loads successfully | … |

---

## Accessibility

The accessibility requirements this page must meet.

- Page title must be set to reflect the current page
- Landmark regions must be present (header, main, footer)
- Focus must move to the main content area on navigation

---

## Notes for AI implementation

Additional context, constraints, and implementation guidance that the agent
should be aware of before writing any code.

- This page is protected — unauthenticated users must be redirected to `/`
- Replace `ComponentA` and `ComponentB` with the actual components this page requires
