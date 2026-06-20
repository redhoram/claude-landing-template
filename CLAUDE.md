# [PROJECT NAME] — Project Instructions

[Replace EVERY placeholder in this file before starting. Write 1-2 sentences: what this project is, who it's for, and its goal.]

This is a **landing page / simple app** project — heavy on design & content, light on logic. The framework and workflow here are optimized for that, NOT for complex CRUD apps (use the separate batch pipeline for those).

## Stack (default — adjust if different)

- Vite + React + TypeScript
- Tailwind CSS v4 (`@tailwindcss/vite`; brand tokens via the `@theme` block in `src/index.css` — NOT `tailwind.config.js`)
- Icons: `lucide-react` (NO emoji as icons)
- No backend/DB. If you need a form, use an external service (e.g. Formspree).

## Workflow: VISUAL LOOP, not a batch pipeline

Design is iterative & visual. The main mode is interactive work in the main session: **edit → see it in live preview → adjust**. Run the dev server and actually look at the result; don't work blind.

- **0→1 — `/craft [page/section]`**: spin up a strong draft from scratch (designer → builder → qa). For getting a fast foundation.
- **1→great — interactive / `/polish [target]`**: polish in the main session with live preview. This is where the design gets sharp.
- DON'T use `/craft` for small tweaks — that kills the iteration loop.

## Brand & Design System

[REQUIRED — fill before starting. This is what keeps the output consistent & sharp.]

- **Palette**: [colors + each color's role + CONTRAST RULES: which text/bg pairings are FORBIDDEN]. Normal text ≥ 4.5:1.
- **Typography**: [display + body fonts, heading scale]
- **Section rhythm** (for landing): [order of section colors/tones so the page has rhythm]
- **Motion**: 150–300ms, use transform/opacity, respect `prefers-reduced-motion`
- **Icons**: lucide-react, consistent sizing

## Design principles (MUST — this is the differentiator)

1. **Bold by default.** For marketing pages, rich content + visual storytelling + micro-interactions ARE the product, not just a tidy layout. Propose a bold concept; don't play it safe/minimal without reason. If there's a reference ("like X"), use it as the benchmark.
2. **Connect to the real product.** Tie copy & visuals to the product's actual capabilities/value, not generic filler.
3. **Discipline = the differentiator from instant generators.** They look tidy but are messy underneath (dependencies in the wrong place, junk files, non-semantic HTML, heavy assets). You're the opposite.

## Quality budget (every build must meet this)

- **Accessibility**: contrast ≥4.5:1, visible focus ring, meaningful `alt` on images, `aria-label` on icon buttons, `cursor-pointer` on everything clickable, logical tab order.
- **Responsive**: check 375 / 768 / 1280px. No horizontal scroll on mobile.
- **Performance**: light assets (optimized/WebP images, small favicon, lazy-load heavy stuff), reserve space to avoid layout shift.
- **Clean code**: DRY components (use `map`, don't copy-paste); dependencies in the right place (build/image tools → `devDependencies`); no junk files/scripts in the repo; semantic HTML.
- **Content honesty**: mark dummy data (mockup names/numbers) clearly as illustrative. Don't fabricate claims.

## Assets

Logos/images: ensure REAL transparency (many "transparent" files actually have a baked-in background). Extract/clean + optimize size before use. Keep raw source files OUTSIDE `public/` so they don't get deployed.

## Conventions

- Code & comments: English
- Communication language with user: [e.g. Indonesian / English]
- Never commit `.env*` or any API key to Git
- [Project-specific rule — e.g. dev port, launcher, etc.]
