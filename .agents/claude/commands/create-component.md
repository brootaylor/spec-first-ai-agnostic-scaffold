# /create-component

Scaffolds a new component following project conventions.
The agent will not write any code without a spec. No exceptions.

## Usage

```bash
/create-component <ComponentName>
```

---

## Steps

### Step 1 — Spec check

Look for `docs/specs/components/<component-name>.spec.md`.

- **Not found** → Stop. Tell the user:
  > "No spec found. Please create `docs/specs/components/<name>.spec.md`
  > using the template at `docs/specs/_component-template.spec.md` before continuing."
  Do not proceed under any circumstances.

- **Found** → Read it completely before doing anything else.

### Step 2 — Derive the interface

From the spec's Props table. Use the active language selection in `docs/ai-context.md`
to determine whether to generate a TypeScript interface or a JavaScript equivalent.
Show it to the user and confirm before writing files.

### Step 3 — Create the component folder

`src/components/<ComponentName>/` containing:

| File | Contents |
|------|----------|
| `<ComponentName>.{js\|ts}` | Implementation scaffold |
| `<ComponentName>.test.{js\|ts}` | One `it()` per `TC-##` in the spec, all failing |
| `<ComponentName>.{css\|scss}` | Empty skeleton |
| `<ComponentName>.spec.md` | Copy of `docs/specs/components/<name>.spec.md` |

File extensions follow the active stack selection in `docs/ai-context.md`.

### Step 4 — Write tests before implementation

All tests must be complete and failing before implementation begins.

### Step 5 — Implement

Write until all tests pass.

### Step 6 — Run tests

Run the test command for the active unit testing tool in `docs/ai-context.md`:

- **Jest** → `npm test`
- **None** → skip this step

Confirm all tests pass before finishing.

### Step 7 — Output summary

```bash
✓ Created: src/components/<ComponentName>/ (4 files)
✓ Tests: N passing, 0 failing
⚠ Spec ambiguities flagged: <list or "none">
```

---

## Rules

- Never skip Step 1
- Never add props not listed in the spec
- One `it()` per `TC-##` — IDs must match the spec exactly
- File extensions must match the active stack selection in `docs/ai-context.md`
- Do not install new packages as part of this command
