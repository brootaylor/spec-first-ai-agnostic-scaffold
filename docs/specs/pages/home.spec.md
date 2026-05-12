# Page Spec: Home

**Status:** Draft

---

## Purpose

> A single paragraph describing what problem this page solves, who uses it,
> and when. Avoid describing how it looks — describe why it exists.

The default landing page for the project. The first page a visitor sees —
it should communicate the project's purpose clearly and direct users to the
most important content or actions.

---

## Route

| Route | Access |
|-------|--------|
| `/` | Public |

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
| `SiteNav` | `docs/specs/components/site-nav.spec.md` |
| `Hero` | `docs/specs/components/hero.spec.md` |
| `ComponentGrid` | `docs/specs/components/component-grid.spec.md` |
| `SiteFooter` | `docs/specs/components/site-footer.spec.md` |

---

## Behaviour

How the page behaves on first load and in response to user interaction.

### Default / initial state

Describe what the page renders and does when first visited.

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

## Example usage

How this page is implemented depends on the active framework selection in
`docs/project-brief.md`.

**Vanilla:**

```html
<!-- src/index.html -->
<!DOCTYPE html>
<html lang="en">
  <head><title>Home</title></head>
  <body>…</body>
</html>
```

**Astro:**

```astro
<!-- src/pages/index.astro -->
---
import MainLayout from '../layouts/MainLayout.astro';
---
<MainLayout pageTitle="Home">
  <!-- page content -->
</MainLayout>
```

**React:**

```jsx
// src/pages/Home.jsx
export function Home() {
  return (
    <MainLayout pageTitle="Home">
      {/* page content */}
    </MainLayout>
  );
}
```

**Svelte:**

```svelte
<!-- src/pages/Home.svelte -->
<MainLayout pageTitle="Home">
  <!-- page content -->
</MainLayout>
```

---

## Notes for AI implementation

Additional context, constraints, and implementation guidance that the agent
should be aware of before writing any code.

- This is a public page — no authentication required
- Each component listed above needs its own spec written before implementation begins
- `ComponentGrid` should link to individual component documentation pages
