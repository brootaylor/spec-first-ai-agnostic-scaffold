# Feature: Service Worker

**Status:** Draft

---

## Overview

Add a service worker to the project to provide basic offline support and a
caching strategy for assets and pages. This improves resilience and performance
for users on slow or unreliable connections.

---

## Key

A reference for the prefixes used throughout this document.

| Prefix | Stands for | Description |
|--------|------------|-------------|
| `US-##` | User Story | A feature requirement from the user's perspective |
| `AC-##` | Acceptance Criteria | A condition that must be met for the story to be complete |

---

## User stories

Each user story describes a requirement from the user's perspective, followed by
the acceptance criteria that must be met for it to be considered complete.

### US-01 — Offline support

> As a user, I want to be able to access previously visited pages when I am
> offline or on a poor connection.

- [ ] **AC-01** — Previously visited pages are available offline
- [ ] **AC-02** — A fallback offline page is shown if a page has not been cached
- [ ] **AC-03** — The user is informed they are viewing a cached version where relevant

### US-02 — Asset caching

> As a user, I want the site to load quickly on repeat visits by serving
> cached assets where possible.

- [ ] **AC-01** — Static assets (CSS, JS, fonts, images) are cached on first visit
- [ ] **AC-02** — Cached assets are served immediately on repeat visits
- [ ] **AC-03** — Assets are updated in the background when a new version is available

---

## Caching strategy

The active caching strategy should be noted here. See the constraints section
for guidance on which strategy to choose.

| Strategy | Active |
|----------|--------|
| Cache first *(assets)* + Network first *(pages)* | |
| Network first *(all)* | |
| Stale while revalidate | |
| Custom — describe below | |

> *If Custom is selected, describe the strategy here.*

---

## Out of scope

Explicitly listing what this feature does NOT cover prevents scope creep and
helps the agent avoid building more than is required.

- Push notifications
- Background sync
- Full PWA (installable app)
- Server-side caching

---

## Constraints

Notes on caching strategy choices and framework-specific considerations.

- **Cache first + Network first** — recommended for static documentation sites.
  Serves assets from cache for speed; fetches pages from the network for freshness,
  falling back to cache when offline
- **Network first** — better for frequently updated content but slower on repeat visits
- **Stale while revalidate** — good balance for content that changes occasionally —
  serves cache immediately and updates in the background

**Framework-specific notes:**

- **Astro** — use `@astrojs/service-worker` or a community PWA plugin
- **Eleventy** — use Workbox or a manual `sw.js` file registered in the base layout
- **React + Vite** — use `vite-plugin-pwa`
- **Svelte + SvelteKit** — SvelteKit has built-in service worker support via `src/service-worker.js`
- **Vanilla + Vite** — use `vite-plugin-pwa` or a manual `sw.js` file

---

## Notes for AI agents

- Read the active caching strategy selection above before implementing
- The service worker file should live at the root of the build output so it can
  control the entire site scope
- Register the service worker in the root layout or main entry file
- Always include a fallback offline page at `src/offline.html` (or framework equivalent)
- Do not cache API responses unless explicitly specified in the caching strategy
