# Feature: User Authentication

**Status:** Approved for v1
**Last updated:** 2025-01

---

## Overview

Allow visitors to create accounts and allow returning users to sign in and sign out.
Authentication is a prerequisite for all personalised features in the application.

---

## User stories

### US-01 — Sign up

> As a new visitor, I want to create an account with my email and password.

- [ ] **AC-01** — Valid email + password (min 8 chars, 1 uppercase, 1 number)
- [ ] **AC-02** — Duplicate email shows inline error; no account created
- [ ] **AC-03** — Success redirects to `/dashboard`
- [ ] **AC-04** — Confirmation email sent via `src/lib/mailer.ts`
- [ ] **AC-05** — Password never stored or logged in plain text

### US-02 — Sign in

> As a returning user, I want to sign in with my credentials.

- [ ] **AC-01** — Invalid credentials → "Invalid email or password" (no enumeration)
- [ ] **AC-02** — 5 failed attempts → 15 min lockout with countdown
- [ ] **AC-03** — "Remember me" → 30-day session; without it → session-only
- [ ] **AC-04** — Success redirects to originally requested URL or `/dashboard`

### US-03 — Sign out

> As a signed-in user, I want to sign out from any page.

- [ ] **AC-01** — Token invalidated server-side on sign-out
- [ ] **AC-02** — Redirect to `/`
- [ ] **AC-03** — URL never contains session tokens

---

## Out of scope (v1)

- OAuth / social sign-in
- Two-factor authentication
- Magic-link / password-less sign-in

---

## Components required

| Component | Spec |
|-----------|------|
| `SignUpForm` | `docs/specs/components/sign-up-form.spec.md` |
| `SignInForm` | `docs/specs/components/sign-in-form.spec.md` |
| `AuthGuard` | `docs/specs/components/auth-guard.spec.md` |

---

## Notes for AI agents

- All auth logic flows through `src/lib/auth.ts` — never implement token
  handling inline in a component
- All three user stories require E2E coverage in `tests/e2e/auth.test.ts`
- Password hashing is server-side — the client sends raw passwords over HTTPS
