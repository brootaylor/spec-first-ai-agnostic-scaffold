# /create-component

Scaffolds a new component following project conventions.
Will not write code without a spec — this is a hard gate.

## Usage

```
/create-component <ComponentName>
```

---

## Steps

### Step 1 — Spec check (required gate)
Look for `docs/specs/components/<component-name>.spec.md`.

- **Not found** → Stop. Tell the user:
  > "No spec found. Please create `docs/specs/components/<name>.spec.md`
  > using the template at `docs/specs/_template.spec.md` before continuing."
  Do not proceed under any circumstances.

- **Found** → Read it completely before doing anything else.

### Step 2 — Derive the TypeScript interface
From the spec's Props table. Show it to the user and confirm before writing files.

### Step 3 — Create the component folder
`src/components/<ComponentName>/` containing:

| File | Contents |
|------|----------|
| `<ComponentName>.ts` | Implementation scaffold |
| `<ComponentName>.test.ts` | One `it()` per `TC-##` in the spec, all failing |
| `<ComponentName>.module.css` | Empty skeleton |
| `<ComponentName>.spec.md` | Copy of `docs/specs/components/<name>.spec.md` |

### Step 4 — Write tests before implementation
All tests must be complete and failing before implementation begins.

### Step 5 — Implement
Write until all tests pass.

### Step 6 — Run tests
Run `npm test -- <ComponentName>` and confirm exit code 0.

### Step 7 — Output summary
```
✓ Created: src/components/<ComponentName>/ (4 files)
✓ Tests: N passing, 0 failing
⚠ Spec ambiguities flagged: <list or "none">
```

---

## Rules

- Never skip Step 1
- Never add props not listed in the spec
- One `it()` per `TC-##` — IDs must match the spec exactly
- Do not install new packages as part of this command
