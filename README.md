# _landing-template

> 🇮🇩 [Versi Bahasa Indonesia](./README.id.md)

A template framework for **landing pages & simple apps** — heavy on design & content, light on logic. Sibling of `_pipeline-template` (for complex CRUD apps), but optimized for iterative visual work.

## Philosophy: visual loop, not a batch pipeline

Design is iterative & visual (see → change → see again). Forcing a five-stage batch pipeline here just kills that loop. So this framework has **two modes**:

- **0→1 — `/craft [page/section]`**: spin up a strong draft from scratch via 3 subagents (designer → builder → qa). For getting a fast foundation.
- **1→great — interactive / `/polish [target]`**: polish in the main session with live preview. This is where the design gets sharp.

Batch pipelines suit CRUD; visual polish needs eyes on the screen.

## Difference from `_pipeline-template`

| | `_pipeline-template` (complex CRUD) | `_landing-template` (landing & simple apps) |
|---|---|---|
| Mode | Batch, doc-driven, fire-and-forget | Visual loop + interactive |
| Agents | planner → designer → coder → tester → reviewer | designer → builder → qa |
| Final gate | Reviewer (SHIP/BLOCK, security-focused) | QA (punch-list, UI/UX-focused) |
| Command | `/ship` | `/craft` (0→1) + `/polish` (1→great) |
| Verification | build/lint/test + scenarios | live preview: render, responsive, console |

## Contents

- `CLAUDE.md` — the heart: brand/design system + design principles + quality budget + workflow. **Fill in the placeholders first.**
- `.claude/agents/` — `designer`, `builder`, `qa`
- `.claude/commands/` — `craft`, `polish`
- `.claude/skills/` — `premium-design` (bundled design-quality skill: palette, typography, motion, context adaptation)
- `.craft/` — handoff workspace (`design.md`, `build-notes.md`, `qa-report.md`)

## Start a new project

1. Copy `_landing-template` → rename the folder
2. Fill in `CLAUDE.md` — especially the **Brand & Design System** section (this is what keeps output consistent & sharp)
3. Scaffold the stack (default Vite + React + TS + Tailwind v4 + lucide-react)
4. `git init`

## Standard

What sets the output apart from instant generators: **bold in design, disciplined in code.** Details in the principles & quality budget inside `CLAUDE.md`.
