---
name: web-quality
description: Use when implementing UI code — the patterns that hit the quality budget's numbers (LCP ≤2.5s, INP ≤200ms, CLS <0.1, bundle <250KB gzipped) at write time. Image/font loading, layout stability, interaction responsiveness, bundle discipline, Tailwind v4 idiom.
---

# Web Quality

Core belief: the quality budget's numbers are hit **while writing the code**, not by
optimizing afterwards. Every image tag, font declaration, and dependency choice either
respects the budget or borrows against it. Google measures at the 75th percentile of
real visits — median-fast is not fast.

## 1. LCP ≤ 2.5s — the hero renders first

- **Preload the LCP image** (usually the hero) and mark its priority:
  ```html
  <link rel="preload" href="/hero.webp" as="image" fetchpriority="high" />
  <img src="/hero.webp" fetchpriority="high" alt="..." width="1200" height="800" />
  ```
- LCP content lives in the **initial HTML** — never behind a spinner, a JS-only render,
  or a scroll-reveal that starts hidden (see CLAUDE.md no-JS resilience rule).
- Modern formats: WebP/AVIF with `srcset` + `sizes` so mobile never downloads desktop pixels.
- Fonts never block the headline: `font-display: swap` on every `@font-face`; preload
  the display font's woff2 only (`<link rel="preload" as="font" type="font/woff2" crossorigin>`).
- No render-blocking scripts in `<head>` — Vite's defaults are correct; don't add
  synchronous third-party tags above the content.

## 2. CLS < 0.1 — nothing jumps

- **Every** `<img>`, `<video>`, `<iframe>` gets `width`+`height` attributes or a CSS
  `aspect-ratio` — no exceptions, including logos and avatars.
- Reserve space for anything that loads late (embeds, maps): a container with
  `min-height` before the content arrives.
- Web font shift: pair `font-display: swap` with a metric-compatible fallback
  (`size-adjust` / system stack close in metrics) so swap doesn't reflow the page.
- Animations move things with `transform`/`opacity` ONLY — animating height, margin,
  or top is a layout shift you wrote on purpose.
- Never insert content ABOVE the user's current viewport position (banners that push
  the page down = CLS by design).

## 3. INP ≤ 200ms — every tap answers fast

- Event handlers finish visibly in <100ms: give **immediate visual feedback first**
  (class toggle, disabled state), then do heavy work after yielding
  (`requestIdleCallback` / `setTimeout(0)` / React `useTransition` for non-urgent state).
- No long tasks >50ms on the main thread during interaction: chunk loops, defer
  analytics, lazy-import heavy widgets on first interaction
  (`import('./heavy')` inside the handler, `{ once: true }`).
- Debounce input-driven work (search, resize handlers); don't recalc layout per keystroke.
- React: memoize genuinely expensive subtrees (`React.memo`), keep state close to where
  it changes so a keystroke doesn't re-render the page.

## 4. Bundle < 250KB gzipped — every dependency auditions

- Before `npm install`: does the platform or 20 lines of code already do this?
  Date formatting, class joining, simple carousels rarely deserve a dependency.
- Icons: `lucide-react` per-icon imports are tree-shaken — never import the whole set;
  never inline verbose SVG blobs when an icon exists.
- Below-the-fold heavy components (video players, carousels, maps): `React.lazy` +
  dynamic `import()` so the first paint never pays for them.
- Images/fonts are static assets, never imported into the JS bundle as base64.
- After build: check `dist/assets/*.js` gzipped total against 250KB — the QA will.

## 5. Stack idiom (this template's defaults)

- Tailwind v4: brand tokens live in the `@theme` block in `src/index.css` —
  NOT `tailwind.config.js`. Every color traces to a token (premium-design rule).
- `loading="lazy"` + `decoding="async"` on every below-the-fold image; NEVER on the LCP/hero image.
- Scroll-reveal: hidden state applied via a JS-added class on `<body>` (no-JS resilience),
  `IntersectionObserver` with `unobserve` after trigger, respect `prefers-reduced-motion`.
- Static hosting assumption: no server tricks available — everything above must be
  achieved in markup and build output.

## Done check

- [ ] Hero/LCP image: preloaded, `fetchpriority="high"`, WebP/AVIF, srcset, NOT lazy
- [ ] Every media element has dimensions or aspect-ratio; zero layout jump on load
- [ ] Fonts: swap + metric fallback + woff2 preload for the display font
- [ ] Interactions: instant visual feedback; heavy work deferred; no >50ms tasks
- [ ] Each new dependency justified; heavy below-fold components lazy-loaded
- [ ] `dist` JS gzipped < 250KB; below-fold images lazy; motion transform/opacity only

> Credits: adapted for this template from `core-web-vitals` and `performance` in
> [addyosmani/web-quality-skills](https://github.com/addyosmani/web-quality-skills) (MIT),
> trimmed to the write-time patterns a static Vite + React landing page actually uses.
