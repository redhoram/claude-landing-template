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

A template framework for **landing pages & simple apps** — heavy on design & content, light on logic. Sibling of [`_pipeline-template`](https://github.com/redhoram/claude-pipeline-template) (for complex CRUD apps), but optimized for iterative visual work.

### Philosophy: visual loop, not a batch pipeline

Design is iterative & visual (see → change → see again). Forcing a five-stage batch pipeline here just kills that loop. So this framework has **two modes**:

- **0→1 — `/craft [page/section]`**: spin up a strong draft from scratch via 4 subagents (writer → designer → builder → qa). Copy first: the writer sets the message hierarchy and exact headlines/CTAs, then the designer lays them out. For getting a fast foundation.
- **1→great — interactive / `/polish [target]`**: polish in the main session with live preview. This is where the design gets sharp.

Batch pipelines suit CRUD; visual polish needs eyes on the screen.

### Difference from `_pipeline-template`

| | `_pipeline-template` (complex CRUD) | `_landing-template` (landing & simple apps) |
|---|---|---|
| Mode | Batch, doc-driven, fire-and-forget | Visual loop + interactive |
| Agents | planner → designer → coder → tester → reviewer | writer → designer → builder → qa |
| Final gate | Reviewer (SHIP/BLOCK, security-focused) | QA (punch-list, UI/UX-focused) |
| Command | `/ship` | `/craft` (0→1) + `/polish` (1→great) |
| Verification | build/lint/test + scenarios | live preview: render, responsive, console |

### Contents

- `CLAUDE.md` — the heart: brand/design system + design principles + quality budget + workflow. **Fill in the placeholders first.**
- `.claude/agents/` — `writer`, `designer`, `builder`, `qa`
- `.claude/commands/` — `craft`, `polish`
- `.claude/skills/` — 4 bundled skills the agents enforce (matrix below)
- `.craft/` — handoff workspace (`copy.md`, `design.md`, `build-notes.md`, `qa-report.md`)

### Skill matrix

Each agent reads only the skills that belong to its stage — documented here so the mapping is auditable:

| Skill | Used by | Enforces |
|---|---|---|
| `conversion-copy` | writer | Headline formulas + specificity test, PAS-vs-AIDA arc choice, honest proof hierarchy, objection preemption, CTA/microcopy and language rules |
| `premium-design` | designer | Palette discipline, typography metrics, intentional motion, marketing-vs-product intensity |
| `ux-research` | designer + qa | User + JTBD grounding, 3-5 named psychology principles per surface, usability checklist, dark-pattern hard-lines; its 10-question diagnostic (severity 0-4) runs in the visual taste loop |
| `web-quality` | builder | Write-time patterns that hit the budget numbers: LCP preload, CLS dimensions, INP feedback, bundle discipline, Tailwind v4 idiom — adapted from Google Chrome team's [web-quality-skills](https://github.com/addyosmani/web-quality-skills) (MIT) |

### Prerequisites

- [Claude Code](https://claude.com/claude-code) installed — `/craft` and `/polish` are **Claude Code slash commands**, typed inside a Claude Code session in the project folder (they're not npm scripts).
- Node.js 18+ and npm (the default stack is Vite-based).

### Start a new project

1. Copy `_landing-template` → rename the folder
2. Fill in `CLAUDE.md` — especially the **Brand & Design System** section (this is what keeps output consistent & sharp)
3. Scaffold the stack (default Vite + React + TS + Tailwind v4 + lucide-react) — or skip this: `/craft` auto-scaffolds when `package.json` doesn't exist yet
4. `git init`
5. Open Claude Code in the folder → run `/craft [page/section]`

### Standard

What sets the output apart from instant generators: **bold in design, disciplined in code.** Details in the principles & quality budget inside `CLAUDE.md`.

And **fail loud, not silent**: the copy and design specs carry READY/BLOCKED status flags, the builder declares BLOCKED instead of looping forever on a broken build, and QA never claims visual checks it can't perform headless — visual judgment happens in the main session, with eyes on the live preview.

### Credit

**Author**
- Redho Ramadhani — [linkedin.com/in/redhoramadhanihamid](https://id.linkedin.com/in/redhoramadhanihamid) · [github.com/redhoram](https://github.com/redhoram)

Built with [Claude Code](https://claude.com/claude-code).
