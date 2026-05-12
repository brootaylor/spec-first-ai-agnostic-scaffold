# Design Tokens

Design tokens are the named values that define the visual language of this project.
They are defined once and referenced everywhere — in components, pages, and layouts.

> *Fill in the tables below with your project's token values before writing any styles.
> Delete any categories that don't apply. Add new categories as needed.*

---

## How to use tokens

Tokens are defined as CSS custom properties in `src/styles/tokens.scss` and are
available globally. Reference them in any stylesheet like this:

```scss
.example {
  color: var(--color-primary);
  padding: var(--space-sm) var(--space-md);
  font-size: var(--text-base);
}
```

---

## Colour

| Token | Value | Usage |
|-------|-------|-------|
| `--color-primary` | | Primary actions, links |
| `--color-secondary` | | Secondary actions |
| `--color-neutral-100` | | … |
| `--color-neutral-900` | | … |
| `--color-error` | | Error states |
| `--color-success` | | Success states |

---

## Spacing

Spacing tokens follow a consistent scale. All values are in `rem`.

| Token | Value | Usage |
|-------|-------|-------|
| `--space-xs` | | … |
| `--space-sm` | | … |
| `--space-md` | | … |
| `--space-lg` | | … |
| `--space-xl` | | … |

---

## Typography

### Font families

| Token | Value | Usage |
|-------|-------|-------|
| `--font-sans` | | Body text |
| `--font-mono` | | Code blocks |

### Font sizes

| Token | Value | Usage |
|-------|-------|-------|
| `--text-xs` | | … |
| `--text-sm` | | … |
| `--text-base` | | Body text |
| `--text-lg` | | … |
| `--text-xl` | | … |

### Font weights

| Token | Value | Usage |
|-------|-------|-------|
| `--weight-regular` | | Body text |
| `--weight-medium` | | … |
| `--weight-bold` | | Headings |

### Line heights

| Token | Value | Usage |
|-------|-------|-------|
| `--leading-tight` | | Headings |
| `--leading-normal` | | Body text |
| `--leading-loose` | | … |

---

## Border

| Token | Value | Usage |
|-------|-------|-------|
| `--radius-sm` | | … |
| `--radius-md` | | … |
| `--radius-lg` | | … |
| `--border-width` | | … |
| `--border-color` | | … |

---

## Shadows

| Token | Value | Usage |
|-------|-------|-------|
| `--shadow-sm` | | … |
| `--shadow-md` | | … |
| `--shadow-lg` | | … |

---

## Notes

> *Any additional context, decisions, or constraints about the token system.*
