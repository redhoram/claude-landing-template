<p align="center">
  <img src="https://img.shields.io/badge/Claude%20Code-Template-D97757?logo=anthropic&logoColor=white" alt="Claude Code Template">
  <img src="https://img.shields.io/badge/Visual-Loop-informational" alt="Visual Loop">
  <img src="https://img.shields.io/badge/license-MIT-blue.svg" alt="MIT License">
</p>

<p align="center">
  <a href="README.md">English</a> | <a href="README.id.md">Bahasa Indonesia</a>
</p>

---

# _landing-template

A template framework for **landing pages & simple apps**: heavy on design & content, light on logic. Sibling of [`_pipeline-template`](https://github.com/redhoram/claude-pipeline-template) (for complex CRUD apps), but optimized for iterative visual work.

### Philosophy: visual loop, not a batch pipeline

Design is iterative & visual (see → change → see again). Forcing a five-stage batch pipeline here just kills that loop. So this framework has **two modes**:

- **0→1 with `/craft [page/section]`**: spin up a strong draft from scratch via subagents (curator and optimizer when needed → copywriter → composer → developer → qa), then a taste loop and the inspector's verdict. Copy first: the copywriter sets the message hierarchy and exact headlines/CTAs, then the composer lays them out. For getting a fast foundation.
- **1→great, interactive or `/polish [target]`**: polish in the main session with live preview. This is where the design gets sharp.

Batch pipelines suit CRUD; visual polish needs eyes on the screen.

- **QA looks, not just greps**: after the static checks, the QA serves the production build, captures headless screenshots at 375, 768, and 1280px (above the fold and full page), and judges them itself. Severity 3+ visual findings mean NEEDS WORK. Hover, motion, and console are still checked live in the main session.
- **Honest copy by source**: the copywriter takes claims, numbers, testimonials, and logos only from the `Content sources` section of `CLAUDE.md`; everything else is marked illustrative. Indonesian AI clichés are filtered too, and the bundled `humanizer` skill runs on the copy.
- **Audit trail and commit**: each `/craft` run archives the previous `.craft/` files instead of deleting them, and on PASS offers a commit of the built files, staged by explicit path. It never pushes without your confirmation.
- **Model override**: change any agent's model per project in `CLAUDE.md`, without editing the agent file.
- **Two stacks, picked per page**: Astro for pages meant to be found through search (the content is in the HTML before any JavaScript runs, and React loads only for the interactive parts) and Vite + React for app-like pages. `/craft` picks one from the brief and records it, or you fix it in `CLAUDE.md`.

### Difference from `_pipeline-template`

| | `_pipeline-template` (complex CRUD) | `_landing-template` (landing & simple apps) |
|---|---|---|
| Mode | Batch, doc-driven, fire-and-forget | Visual loop + interactive |
| Agents | planner → drafter → coder → tester → gatekeeper (→ deployer after SHIP) | curator → optimizer → copywriter → composer → developer → qa → inspector |
| Final gate | Gatekeeper (SHIP/BLOCK, security-focused) | Inspector (SHIP/REVISE/HOLD on brief, brand, and taste), after the QA punch-list |
| Command | `/ship` (new feature) + `/fix` (revision) | `/craft` (0→1) + `/polish` (1→great) + `/brand` + `/seo-audit` |
| Verification | build/lint/test + scenarios + screenshots | QA screenshots + live preview: render, responsive, console |

### Contents

- `CLAUDE.md`: the heart of the template, holding brand/design system + design principles + quality budget + workflow. **Fill in the placeholders first.**
- `.claude/agents/`: `curator`, `optimizer`, `copywriter`, `composer`, `developer`, `qa`, `inspector`
- `.claude/commands/`: `craft`, `polish`, `brand`, `seo-audit`
- `.claude/skills/`: 10 bundled skills the agents enforce (matrix below)
- `.craft/`: handoff workspace (`brief.md`, `brand.md`, `seo.md`, `copy.md`, `design.md`, `build-notes.md`, `qa-report.md`, `taste-notes.md`, `verdict.md`, `shots/`), with past runs in `.craft/archive/`

### Skill matrix

Each agent reads only the skills that belong to its stage: documented here so the mapping is auditable:

| Skill | Used by | Enforces |
|---|---|---|
| `conversion-copy` | copywriter | Headline formulas + specificity test, PAS-vs-AIDA arc choice, honest proof hierarchy, objection preemption, CTA/microcopy and language rules |
| `seo-content-strategist` | optimizer + copywriter + qa | SEO decided at write time: heading hierarchy as content structure, keyword placement, title/meta as ad copy, JSON-LD choice, alt text; recorded in copy.md's SEO notes; QA verifies the build matches them |
| `humanizer` | copywriter | Removes AI writing patterns from the finished copy: staged contrasts, one-line closers, forced triads, inflated claims, bold labels, filler |
| `premium-design` | curator + composer | Palette discipline, typography metrics, intentional motion, marketing-vs-product intensity |
| `ux-research` | composer + qa | User + JTBD grounding, 3-5 named psychology principles per surface, usability checklist, interaction states and microcopy (pending, loading, failure, focus, touch targets), dark-pattern hard-lines; its 10-question diagnostic (severity 0-4) is split between QA screenshots and the live taste loop |
| `web-quality` | developer | Write-time patterns that hit the budget numbers: LCP preload, CLS dimensions, INP feedback, bundle discipline, Tailwind v4 idiom; adapted from Google Chrome team's [web-quality-skills](https://github.com/addyosmani/web-quality-skills) (MIT) |
| `antislop` | composer + developer + qa | Core filter adapted from anti-slop: a purpose test for every visual technique, 38 rules in three tiers, the Design Read with ENERGY/RHYTHM/MOTION dials, and a Delivery Gate report with evidence |
| `antislop-ui` | curator + composer + developer + qa | Generic AI UI patterns with tell, why, and fix: default gradients, glassmorphism everywhere, bento grids, fake terminals, eyebrow badges, invented stats, dead controls |
| `antislop-layoutmobile` | developer + qa | Reflow from phone to desktop: breakpoints, fluid scale, collapsing grids, overflow, tap targets, mobile navigation |
| `antislop-human` | curator + developer + qa | Contrast computed with `contrast-check.py`, keyboard and focus, color-only feedback, UI states, zoom |

### Prerequisites

- [Claude Code](https://claude.com/claude-code) installed: `/craft` and `/polish` are **Claude Code slash commands**, typed inside a Claude Code session in the project folder (they're not npm scripts).
- Node.js and npm. Two stacks ship with the template: **Astro** for pages meant to be found through search (content is in the HTML before any JavaScript runs; needs a recent Node.js, see Astro's `engines` field) and **Vite** for app-like interactive pages (Node.js 18+). Both use React, TypeScript, Tailwind v4, and lucide-react.
- A Chromium-based browser (Chrome, Edge, or Chromium) so the QA can take headless screenshots. Without one, the QA falls back to a checklist for the main session.

### Start a new project

1. Copy `_landing-template` → rename the folder
2. Fill in `CLAUDE.md`: especially the **Brand & Design System** section (this is what keeps output consistent & sharp; leave it empty and the curator sets it for you) and **Content sources** (what the copywriter may claim)
3. Leave **Chosen stack** in `CLAUDE.md` on `auto` (Astro when the brief says the page is meant to be found through search, Vite otherwise) or fix it to one. `/craft` scaffolds it when `package.json` doesn't exist yet
4. `git init`
5. Open Claude Code in the folder → run `/craft [page/section]`

### Standard

What sets the output apart from instant generators: **bold in design, disciplined in code.** Details in the principles & quality budget inside `CLAUDE.md`.

And **fail loud, not silent**: the brand, SEO plan, copy, and design specs carry READY/BLOCKED status flags, the inspector returns a firm SHIP, REVISE, or HOLD, the developer declares BLOCKED instead of looping forever on a broken build, and QA never claims a visual check it didn't do: it judges its own screenshots, says "not checked" when no browser is available, and leaves hover, motion, and console to the main session with eyes on the live preview.

### Credit

**Author**
- Redho Ramadhani: [linkedin.com/in/redhoramadhanihamid](https://id.linkedin.com/in/redhoramadhanihamid) · [github.com/redhoram](https://github.com/redhoram)

**Included skills adapted from others**
- `antislop` and its companion skills: adapted from [anti-slop](https://github.com/miqdadbadjuber/anti-slop) v3.2.23 by miqdadbadjuber, MIT License (`.claude/skills/antislop/LICENSE`). Changes: no install wizard or mode question, a fixed mode per agent, a theme toggle only when asked, and no em dash or emoji characters.
- `humanizer` v3.1.0 by Siqi Chen, MIT License (`.claude/skills/humanizer/LICENSE`), included unchanged; its examples keep the dashes and emoji it teaches you to remove.

Built with [Claude Code](https://claude.com/claude-code).
