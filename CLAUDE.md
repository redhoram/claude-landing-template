# [PROJECT NAME]: Project Instructions

[Replace EVERY placeholder in this file before starting. Write 1-2 sentences: what this project is, who it's for, and its goal.]

## First thing in a fresh session: verify this isn't a hijacked template copy

Copying this folder (e.g. via file explorer) also copies the hidden `.git`,
so a new project silently inherits the template's history + GitHub remote.
Real risk: committing here could push unrelated project code to the
template's public repo. The user copies this folder on purpose to start new
projects; this check exists so they can do that with zero manual steps.

Before any other work, run `git remote -v` and look at the current folder name.

1. **Original template: skip, touch nothing.** Folder name is
   `_landing-template` or `claude-landing-template`.
2. **Not a copy: skip.** Remote does not contain `claude-landing-template`
   (or there is no remote).
3. **Copy: auto-fix without asking.** Any other folder name AND remote
   contains `claude-landing-template`. Placeholder state does not matter.
   Run immediately (bash), no confirmation needed. The old `.git` is moved
   to the temp dir, not deleted, so nothing is lost. `git add -A` is safe
   here only because the repo was just re-initialised and holds nothing yet:
   ```
   mv .git "/tmp/$(basename "$PWD")-template-git-$(date +%Y%m%d%H%M%S)" && git init -q && git add -A && git commit -q -m "chore: init from _landing-template"
   ```
   Confirm `git remote -v` is empty and `git log --oneline` shows exactly one
   commit. Tell the user in ONE line that the template history was reset
   (mention the backup path), then continue with their request.

This is a **landing page / simple app** project: heavy on design & content, light on logic. The framework and workflow here are optimized for that, NOT for complex CRUD apps (use `_pipeline-template`, the 6-agent `/ship` batch pipeline, for those).

## Stack (default: adjust if different)

- Vite + React + TypeScript
- Tailwind CSS v4 (`@tailwindcss/vite`; brand tokens via the `@theme` block in `src/index.css`: NOT `tailwind.config.js`)
- Icons: `lucide-react` (NO emoji as icons)
- No backend/DB. If you need a form, use an external service (e.g. Formspree).

## Workflow: VISUAL LOOP, not a batch pipeline

Design is iterative & visual. The main mode is interactive work in the main session: **edit → see it in live preview → adjust**. Run the dev server and actually look at the result; don't work blind.

- **0→1 with `/craft [page/section]`**: spin up a strong draft from scratch. A short brief first, then the curator (only when the brand is empty) and the optimizer (only for pages meant to be found through search), then copywriter → composer → developer → qa, a taste loop in the main session, and the inspector's verdict (SHIP / REVISE / HOLD). Copy first, then layout. For getting a fast foundation.
- **`/brand`**: run the curator on its own to set or redo the brand system in `.craft/brand.md`. **`/seo-audit [target]`**: run the optimizer in audit mode on a page that already exists. Both report; neither changes code.
- **1→great, interactive or `/polish [target]`**: polish in the main session with live preview. This is where the design gets sharp.
- DON'T use `/craft` for small tweaks: that kills the iteration loop.
- Each `/craft` run archives the previous `.craft/` files to `.craft/archive/<timestamp>/`, except `brand.md`, which belongs to the project. The QA renders the build headless and looks at its own screenshots (`.craft/shots/`); the main session still drives the live preview for hover, motion, and console.

## Brand & Design System

[REQUIRED: fill before starting, or leave the bullets below empty and let the curator set them: it writes `.craft/brand.md` and replaces these bullets with a pointer. This is what keeps the output consistent & sharp.]

- **Visual reference** (recommended): [URL or "looks like X". This becomes the taste benchmark for the composer. If you have one, put it here. If not, the composer will propose boldly.]
- **Palette**: [colors + each color's role + CONTRAST RULES: which text/bg pairings are FORBIDDEN]. Normal text ≥ 4.5:1.
- **Typography**: [display + body fonts, heading scale]
- **Section rhythm** (for landing): [order of section colors/tones so the page has rhythm]
- **Motion**: 150-300ms, use transform/opacity, respect `prefers-reduced-motion`
- **Icons**: lucide-react, consistent sizing

## Design principles (MUST: this is the differentiator)

1. **Bold by default.** For marketing pages, rich content + visual storytelling + micro-interactions ARE the product, not just a tidy layout. Propose a bold concept; don't play it safe/minimal without reason. If there's a reference ("like X"), use it as the benchmark.
2. **Connect to the real product.** Tie copy & visuals to the product's actual capabilities/value, not generic filler.
3. **Discipline = the differentiator from instant generators.** They look tidy but are messy underneath (dependencies in the wrong place, junk files, non-semantic HTML, heavy assets). You're the opposite.
4. **Meet the `premium-design` bar.** This repo bundles a `premium-design` skill (`.claude/skills/premium-design/`); load it when designing or polishing. It encodes palette discipline, typography metrics, intentional motion, and context adaptation. The Brand & Design System above wins on any conflict. Five more bundled skills arm the other stages (full matrix in README): `conversion-copy` (copywriter: headline formulas, proof hierarchy, CTA rules), `seo-content-strategist` (copywriter + qa: SEO decided at write time), `humanizer` (copywriter: strips AI writing patterns from the finished copy), `ux-research` (composer + qa: psychology principles, usability diagnostic, anti-dark-pattern lines), `web-quality` (developer: the patterns that hit the performance numbers). Four `antislop` skills, adapted from [anti-slop](https://github.com/miqdadbadjuber/anti-slop) (MIT), filter generic AI UI patterns: the composer and developer apply them while working, and the qa audits with them.

## Quality budget (every build must meet this)

- **Accessibility**: contrast ≥4.5:1, visible focus ring, meaningful `alt` on images, `aria-label` on icon buttons, `cursor-pointer` on everything clickable, logical tab order.
- **Responsive**: check 375 / 768 / 1280px. No horizontal scroll on mobile.
- **Performance (measurable)**: LCP < 2.5s, INP < 200ms, CLS < 0.1. JS bundle < 250KB gzipped. Images WebP/AVIF, no raw PNG > 200KB, small favicon; `loading="lazy"` on below-fold images; reserve space to avoid layout shift.
- **SEO**: exactly ONE `<h1>` per page; heading levels never skip (no h2 → h4); `<title>` + meta description (< 155 chars, reads like ad copy for the page); descriptive `alt` doubles as image SEO; JSON-LD structured data (Product/FAQPage/Article) when the content type fits.
- **Conversion basics**: primary CTA visible above the fold at 375px AND 1280px; CTA labels are verb-first and specific ("Start free", not "Submit"/"Learn more").
- **Clean code**: DRY components (use `map`, don't copy-paste); dependencies in the right place (build/image tools → `devDependencies`); no junk files/scripts in the repo; semantic HTML.
- **No-JS resilience**: scroll-reveal hidden state must degrade gracefully; apply it via a JS-added class on `<body>`, not hardcoded as `opacity-0` in JSX initial state. Always respect `prefers-reduced-motion: reduce`.
- **Content honesty**: mark dummy data (mockup names/numbers) clearly as illustrative. Don't fabricate claims.

## Content sources

[Where real claims come from. The copywriter uses ONLY these for numbers, testimonials, client logos, awards, and feature claims; anything else is marked `[ILLUSTRATIVE]`. Delete the lines that don't apply.]

- Product facts and features: [e.g. `docs/product.md`, or "the request"]
- Numbers and results: [e.g. `docs/metrics.md`, or "none yet: mark illustrative"]
- Testimonials and logos: [e.g. `docs/testimonials.md` with written permission, or "none"]

## Model override

[Optional. Defaults are in each agent file: copywriter, composer, developer, curator, inspector on `opus`; qa, optimizer on `sonnet`. List an agent here to run it on a different model in this project without editing the agent file. Leave empty to use the defaults.]

| Agent | Model | Why |
|---|---|---|
| [agent] | [model] | [why this agent needs a different model] |

## Assets

Logos/images: ensure REAL transparency (many "transparent" files actually have a baked-in background). Extract/clean + optimize size before use. Keep raw source files OUTSIDE `public/` so they don't get deployed.

## Conventions

- Code & comments: English
- Communication language with user: [e.g. Indonesian / English]
- Never commit `.env*` or any API key to Git
- Dev server: `npm run dev` (Vite, default port 5173). [Adjust if this project uses a different launcher/port]
- As the project grows: rules relevant to only ONE folder go in a `CLAUDE.md` inside that folder, loaded lazily only when Claude works there, keeping this root file lean.
- [Project-specific rule: e.g. custom scripts, deploy target, etc.]
- Git: [author email for commits]. Stage files by explicit path, never `git add -A`. Never push without the user's explicit confirmation.

## Agent Reporting Discipline (applies to every agent, every session)

- Report only what you verified **fresh in this session, right now**. If
  you reuse or reference results from an older run/file, say so explicitly
  and never mark something "Completed"/"PASS" in a way that implies it was
  just re-verified when it wasn't.
- Before starting a verification/QA task, delete or clearly disregard any
  stale scratchpad/checklist file left over from a prior failed or
  incomplete run: don't repurpose it by pasting old results into it.
- If a status changes from "blocked"/"in progress" to "done" with no
  visible verification steps in between (no tool calls, no fresh evidence),
  that's not done: go back and actually do it, or report it as blocked.
