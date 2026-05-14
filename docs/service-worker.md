# Service Worker

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

- [ ] **AC-01** — Previously visited pages are served from cache when the network is unavailable
- [ ] **AC-02** — A fallback `offline.html` page is served when the user is offline and the requested page has not been cached
- [ ] **AC-03** — The service worker is registered in the root layout or main entry file before any other scripts

### US-02 — Asset caching

> As a user, I want the site to load quickly on repeat visits by serving
> cached assets where possible.

- [ ] **AC-01** — Static assets (CSS, JS, fonts, images) are cached during the service worker `install` event
- [ ] **AC-02** — Cached assets are served immediately on repeat visits without a network round-trip
- [ ] **AC-03** — When a new version of the service worker is deployed, outdated caches are deleted during the `activate` event

---

## Caching strategy

Choose one strategy and mark it `[active]` in `docs/project-brief.md`. The strategy
selected there is the single source of truth — do not redefine it here.

The table below describes what each strategy does and when to choose it.

| Strategy | When to choose it | How it works |
|----------|-------------------|--------------|
| **Cache first *(assets)* + Network first *(pages)*** | Static documentation sites, marketing sites, component libraries — content changes infrequently | Assets (CSS, JS, images, fonts) are served from cache for speed. Pages are fetched from the network first for freshness, falling back to cache when offline. Recommended default. |
| **Network first *(all)*** | Sites where content changes frequently and stale data is a problem | Every request hits the network first. Cache is only used when the network fails. Slower on repeat visits but always fresh when online. |
| **Stale while revalidate** | Content that changes occasionally and where brief staleness is acceptable | Cache is served immediately (fast), while a network request updates the cache in the background. The updated version is shown on the next visit. |
| **Custom** | Projects with complex routing, authenticated content, or mixed static/dynamic pages | Define the strategy in this file below. |

> *If Custom is selected, describe the strategy here — which routes use which approach,
> what is never cached (e.g. API responses, authenticated pages), and why.*

---

## Offline fallback

When a user is offline and the requested page is not in the cache, the service
worker must serve a fallback page rather than showing a browser error.

**Requirements:**

- The fallback page must live at `src/offline.html` (or the framework equivalent — see Setup guidance below)
- It must contain no external dependencies — no CDN scripts, no externally hosted fonts, no images referenced by a third-party URL. Local assets that are included in the precache manifest are fine, as they will already be in the cache when this page is served
- It must communicate clearly that the user is offline and suggest they check their connection
- It must be added to the cache during the service worker `install` event so it is always available

**Minimal example:**

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>You're offline</title>
    <style>
      body {
        font-family: sans-serif;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        min-height: 100vh;
        margin: 0;
        padding: 1rem;
        text-align: center;
      }
    </style>
  </head>
  <body>
    <h1>You're offline</h1>
    <p>This page isn't available without a network connection. Check your connection and try again.</p>
  </body>
</html>
```

> The fallback page is intentionally minimal — it should not import tokens or global
> styles because those assets may not be cached yet on a first visit that goes offline.

---

## Cache versioning

Service worker caches must be versioned so that stale caches are cleaned up when a
new version of the site is deployed. Without this, users may receive outdated assets
indefinitely.

**Using `vite-plugin-pwa` (Vanilla + Vite, React + Vite):**

The plugin handles versioning automatically using asset content hashes. No manual
cache naming is required. The generated service worker includes a precache manifest
that is updated on every build.

**Using a manual `sw.js` (Eleventy, or any setup not using the plugin):**

- Name every cache with a version suffix: `const cacheName = 'site-cache-v1'`
- Increment the version whenever assets change: `'site-cache-v2'`, and so on
- Delete all caches that do not match the current name during the `activate` event:

```js
self.addEventListener('activate', (event) => {
  event.waitUntil(
    caches.keys().then((keys) =>
      Promise.all(
        keys
          .filter((key) => key !== cacheName)
          .map((key) => caches.delete(key))
      )
    )
  );
});
```

> Agents must not hardcode a cache name without a versioning mechanism. For plugin-based
> setups, confirm the plugin is generating a new manifest on each build. For manual
> setups, the version suffix in `cacheName` is the single source of truth — update it
> whenever cached assets change.

---

## Out of scope

Explicitly listing what this feature does NOT cover prevents scope creep and
helps the agent avoid building more than is required.

- Push notifications
- Background sync
- Full PWA (installable app, manifest, splash screens)
- Server-side caching
- Caching of authenticated or user-specific content
- Caching of API responses unless explicitly specified

---

## Setup guidance

The following covers the most common framework and tooling combinations. For Astro
and Eleventy with a plugin, refer to the relevant documentation links — do not adapt
the Vite examples without checking compatibility first.

---

### Vanilla + Vite

Use `vite-plugin-pwa`. It generates a service worker from your Vite config and
integrates with the existing `vite build` step — no additional npm script is needed.

**Install:**

```bash
npm install --save-dev vite-plugin-pwa
```

**`vite.config.js`:**

```js
import { defineConfig } from 'vite';
import { VitePWA } from 'vite-plugin-pwa';

export default defineConfig({
  plugins: [
    VitePWA({
      registerType: 'autoUpdate',
      // Precache all static assets produced by the build
      includeAssets: ['**/*.{js,css,html,svg,png,ico,woff2}'],
      workbox: {
        // Pages — network first, fall back to cache, then offline fallback
        navigationFallback: '/offline.html',
        runtimeCaching: [
          {
            urlPattern: ({ request }) => request.mode === 'navigate',
            handler: 'NetworkFirst',
          },
        ],
      },
    }),
  ],
});
```

**Register in `src/scripts/main.js`:**

```js
import { registerSW } from 'virtual:pwa-register';

registerSW({ immediate: true });
```

**Offline fallback:** place `src/offline.html` in the project root `public/` folder
so Vite copies it to the build output automatically.

---

### React + Vite

Setup is identical to Vanilla + Vite above. Register the service worker in
`src/scripts/main.jsx` (or `main.tsx`) before the app is mounted:

```jsx
import { registerSW } from 'virtual:pwa-register';
import { createRoot } from 'react-dom/client';
import App from './App';

registerSW({ immediate: true });

createRoot(document.getElementById('root')).render(<App />);
```

---

### Svelte + SvelteKit

SvelteKit has native service worker support. No plugin is required.

**Create `src/service-worker.js`:**

SvelteKit automatically registers any file at `src/service-worker.js`. A minimal
cache-first (assets) + network-first (pages) implementation:

```js
import { build, files, version } from '$service-worker';

const CACHE_NAME = `site-cache-${version}`;
const ASSETS = [...build, ...files];

self.addEventListener('install', (event) => {
  event.waitUntil(
    caches.open(CACHE_NAME).then((cache) => cache.addAll(ASSETS))
  );
});

self.addEventListener('activate', (event) => {
  event.waitUntil(
    caches.keys().then((keys) =>
      Promise.all(
        keys.filter((key) => key !== CACHE_NAME).map((key) => caches.delete(key))
      )
    )
  );
});

self.addEventListener('fetch', (event) => {
  if (event.request.mode === 'navigate') {
    // Network first for pages
    event.respondWith(
      fetch(event.request).catch(() =>
        caches.match(event.request).then((cached) => cached ?? caches.match('/offline.html'))
      )
    );
  } else {
    // Cache first for assets
    event.respondWith(
      caches.match(event.request).then((cached) => cached ?? fetch(event.request))
    );
  }
});
```

> SvelteKit injects `build`, `files`, and `version` automatically — do not import
> from anywhere else. The `version` value changes on every build, so the cache name
> is versioned automatically.

**Offline fallback:** place `offline.html` in the `static/` folder so SvelteKit
includes it in the build output.

---

### Eleventy

Eleventy has no built-in service worker support. Use a manual `sw.js` file.

**Create `src/sw.js`:**

```js
const cacheName = 'site-cache-v1';
const offlineUrl = '/offline.html';

const precacheAssets = [
  '/',
  offlineUrl,
  // Add paths to your compiled CSS and JS here, e.g.:
  // '/assets/main.css',
  // '/assets/main.js',
];

self.addEventListener('install', (event) => {
  event.waitUntil(
    caches.open(cacheName).then((cache) => cache.addAll(precacheAssets))
  );
});

self.addEventListener('activate', (event) => {
  event.waitUntil(
    caches.keys().then((keys) =>
      Promise.all(
        keys.filter((key) => key !== cacheName).map((key) => caches.delete(key))
      )
    )
  );
});

self.addEventListener('fetch', (event) => {
  if (event.request.mode === 'navigate') {
    event.respondWith(
      fetch(event.request).catch(() =>
        caches.match(event.request).then((cached) => cached ?? caches.match(offlineUrl))
      )
    );
  } else {
    event.respondWith(
      caches.match(event.request).then((cached) => cached ?? fetch(event.request))
    );
  }
});
```

**Register in your base layout** (e.g. `src/_includes/base.njk`):

```html
<script>
  if ('serviceWorker' in navigator) {
    navigator.serviceWorker.register('/sw.js');
  }
</script>
```

**Eleventy config** — ensure `sw.js` is passed through to the build output:

```js
// .eleventy.js
eleventyConfig.addPassthroughCopy('src/sw.js');
eleventyConfig.addPassthroughCopy('src/offline.html');
```

> **Cache versioning** — for Eleventy, the `cacheName` version suffix (`v1`, `v2` …)
> must be updated manually on each deploy. See the Cache versioning section above.

---

### Astro

Use `@vite-pwa/astro` (the official Astro PWA integration). Do not adapt the Vite
examples above — the Astro integration wraps the plugin differently.

```bash
npm install --save-dev @vite-pwa/astro
```

Refer to the [Astro PWA integration documentation](https://vite-pwa-org.netlify.app/frameworks/astro)
for full configuration. The offline fallback and cache versioning guidance in this
file still applies — only the plugin wiring differs.

---

## Notes for AI agents

- Read the active caching strategy selection in `docs/project-brief.md` before implementing — do not default to a strategy if none is marked active
- The service worker file must be served from the root of the build output so it controls the full site scope — verify the output path is `/sw.js`, not `/assets/sw.js` or similar
- Register the service worker in the root layout or main entry file, wrapped in a `'serviceWorker' in navigator` guard
- Always create `offline.html` — see the Offline fallback section above for content requirements and where to place the file per framework
- Do not cache API responses, authenticated routes, or user-specific content unless explicitly specified in this file
- For `vite-plugin-pwa` setups: add `vite-plugin-pwa` to `devDependencies` — no new npm scripts are needed as the plugin integrates with the existing `vite build` step
- For manual `sw.js` setups: follow the Cache versioning section above — do not hardcode a cache name without a versioning mechanism
- Add the service worker build output to `.gitignore` if the plugin generates it at a known path (e.g. `public/sw.js` for some plugin configurations) — confirm with the plugin's documentation. Do not add the `src/sw.js` source file to `.gitignore`
