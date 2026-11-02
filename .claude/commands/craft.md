---
description: Spin up a strong draft for a page/section from scratch. Brief, then curator and optimizer when needed, copywriter, composer, developer, qa, a taste loop, and the inspector's verdict. For the 0→1 moment; polish interactively after.
---

User request: $ARGUMENTS

This is for **building a strong first draft** (0→1). After it's done, further polish happens interactively in the main session (or `/polish`): DON'T re-run this command for small tweaks.

Run in order, don't skip:

0. **Brief and workspace clean.**
   - *Brief*: read `CLAUDE.md` and the request. Ask the user only for what is missing, in ONE message of at most three short questions: the page's goal, who it is for, and a visual reference (a site or app they love the look of, or a described vibe). If the Brand section already has a reference, don't ask for one. If they skip or give nothing, proceed and never re-ask. Write the answers and any known scope to `.craft/brief.md`, including whether the page is meant to be found through search, and a `Stack:` line (`Astro` or `Vite`) picked by the rule in the Stack section of `CLAUDE.md`. Every later agent works to that stack.
   - *Workspace clean*: if `.craft/` holds files from a previous run (`brief.md`, `seo.md`, `copy.md`, `design.md`, `build-notes.md`, `qa-report.md`, `taste-notes.md`, `verdict.md`, `shots/`), MOVE them into `.craft/archive/<YYYYMMDD-HHMM>/` so an old run is never read by mistake and the history survives. Do NOT touch `brand.md` (it belongs to the project, not to one run), `.gitkeep`, or existing archive folders.
   - **Model override**: read the `## Model override` table in `CLAUDE.md`. Whenever you call a subagent listed there, pass that model when spawning it.
   - *Fresh repo note*: if `package.json` doesn't exist yet, that's fine; the **developer** scaffolds the project per `CLAUDE.md`'s Stack as its step 0. Don't scaffold here, don't skip the copywriter or composer.
1. **Brand (only when needed).** If the Brand section of `CLAUDE.md` still holds placeholders AND `.craft/brand.md` does not exist, call the **curator** subagent. Wait until `.craft/brand.md` is written. If its first line is `STATUS: BLOCKED`, stop here (see **Fatal** below). Otherwise skip this step.
2. **SEO plan (only when needed).** If `.craft/brief.md` says the page is meant to be found through search, call the **optimizer** subagent in plan mode. Wait until `.craft/seo.md` is written. If its first line is `STATUS: BLOCKED`, stop here (see **Fatal**). If it says `STATUS: SKIPPED`, continue. If the page is not search-driven, skip this step.
3. Call the **copywriter** subagent with the request above. It follows `.craft/seo.md` and the voice in `.craft/brand.md` when they exist. Wait until `.craft/copy.md` is written. If its first line is `STATUS: BLOCKED`, stop here (see **Fatal**); don't design around missing copy.
4. Call the **composer** subagent with the request. It reads `.craft/copy.md` as the copy source of truth and `.craft/brand.md` as the brand source of truth, and lays them out. Wait until `.craft/design.md` is written. If its first line is `STATUS: BLOCKED`, stop here (see **Fatal**); don't send a blocked spec to the developer.
5. Call the **developer** subagent to implement. Wait until `.craft/build-notes.md` is written.
6. Call the **qa** subagent to check the result. Wait until `.craft/qa-report.md` is written.
7. **Visual taste loop (REQUIRED)**: start the dev server and look at the result in the browser. QA's screenshots in `.craft/shots/` are the first look; this loop covers what a still image can't (hover, motion, scrolling, console). Three layers, don't skip any:
   - *Behavior*: answer the 10-question diagnostic from `.claude/skills/ux-research/SKILL.md` §5 while driving the page; every "no" gets a severity (0-4) and severity 3+ goes straight to the punch-list.
   - *Function*: responsive at 375/768/1280px, no horizontal scroll, no console errors.
   - *Taste*: run the `premium-design` Done Check against what you see: zero raw colors? display+body fonts set? every interactive element has a deliberate hover state? Does it feel intentional, or does it still look like a template? If anything is flat/generic, add it to the punch-list. The design isn't done until it passes the taste check, not just the function check.
   Write what you saw, finding by finding with its severity, to `.craft/taste-notes.md`. The inspector reads it.
8. Call the **inspector** subagent for the final verdict. Wait until `.craft/verdict.md` is written.
9. Show the user a summary: copy strategy (core promise), design direction, what was built, QA status, and the inspector's verdict with its reasons.
   - If the verdict is **REVISE** or QA is **NEEDS WORK**: offer to re-run from the **developer** (using `.craft/verdict.md` and `.craft/qa-report.md` as the fix list) → qa → taste loop → inspector. Don't loop automatically without user confirmation.
   - If the verdict is **SHIP**: offer to commit. Stage ONLY the files listed in `.craft/build-notes.md`, by explicit path, never `git add -A`. Use the author in the `Git` line of `CLAUDE.md` Conventions. Never push without the user's explicit confirmation.
   - If the verdict is **HOLD**: show what blocks the judgment and wait for the user's call.

**Fatal = stop the chain.** Fatal means any of: a subagent finished without writing its output file (`.craft/brand.md` / `.craft/seo.md` / `.craft/copy.md` / `.craft/design.md` / `.craft/build-notes.md` / `.craft/qa-report.md` / `.craft/verdict.md`), the brand, SEO plan, copy, or design spec says `STATUS: BLOCKED`, or `.craft/build-notes.md` contains a `## BLOCKED` section. On any of these: stop, show the user exactly what's blocked and why, and wait for their call. Don't improvise around it and don't re-run the chain hoping it fixes itself.
