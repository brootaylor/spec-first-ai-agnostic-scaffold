# Layout Spec: MainLayout

**Status:** Draft

> *Type annotations in this spec apply when TypeScript is the active language.
> CSS imports are `.css` or `.scss` depending on the active styles selection in `docs/project-brief.md`.*

---

## Purpose

A single paragraph describing what problem this layout solves, who uses it,
and when. Avoid describing how it looks — describe why it exists.

The primary layout wrapping all authenticated pages. Provides a consistent
structure with a header, main content area, and footer so individual pages
only need to concern themselves with their own content.

---

## Interface

The props that define how this layout is used.
The agent will derive the interface directly from this section.

### Props / Parameters

| Prop | Type | Required | Default | Description |
|------|------|:--------:|---------|-------------|
| `children` | element | ✓ | — | The page content to render in the main content area |
| `pageTitle` | `string` | ✓ | — | Sets the page `<title>` and main heading |

---

## Structure

A description of the regions this layout renders and their purpose.

| Region | Element | Purpose |
|--------|---------|---------|
| Header | `<header>` | Site navigation and global controls (e.g. theme toggle) |
| Main | `<main>` | Page content passed via `children` |
| Footer | `<footer>` | Secondary navigation and legal links |

---

## Components

The components this layout depends on. Each must have a spec in
`docs/specs/components/` before implementation can begin.

| Component | Spec |
|-----------|------|
| `ThemeToggle` | `docs/specs/components/theme-toggle.spec.md` |

---

## Behaviour

How the layout behaves on first render and in response to user interaction.

### Default / initial state
Renders the header, main content area containing `children`, and footer.
The `pageTitle` is applied to the document `<title>` and rendered as the
main `<h1>` on the page.

---

## Accessibility

The accessibility requirements this layout must meet.

- Must use semantic HTML landmark elements (`<header>`, `<main>`, `<footer>`)
- `pageTitle` must be reflected in both the document `<title>` and a visible `<h1>`
- A skip navigation link must be present to allow keyboard users to bypass the header

---

## Notes for AI implementation

Additional context, constraints, and implementation guidance that the agent
should be aware of before writing any code.

- The skip navigation link should point to `#main-content` and be visually hidden until focused
- CSS: import from `./MainLayout.css` or `./MainLayout.scss` depending on active styles selection
