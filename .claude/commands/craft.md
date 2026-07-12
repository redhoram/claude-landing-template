---
description: Spin up a strong draft for a page/section from scratch — Writer → Designer → Builder → QA. For the 0→1 moment; polish interactively after.
---

User request: $ARGUMENTS

This is for **building a strong first draft** (0→1). After it's done, further polish happens interactively in the main session (or `/polish`) — DON'T re-run this command for small tweaks.

Run in order, don't skip:

0. **Reference check + workspace clean**: if no visual reference (URL or style description) exists in `CLAUDE.md`'s Brand section, ask the user ONE question: *"Any site or app you love the look of? Drop a link or describe the vibe — I'll use it as the taste benchmark."* If they answer, use it; if they skip or give nothing, proceed without it and never re-ask. Then delete old `.craft/copy.md`, `.craft/design.md`, `.craft/build-notes.md`, `.craft/qa-report.md` if present. Do NOT delete `.gitkeep`.
   *Fresh repo note*: if `package.json` doesn't exist yet, that's fine — the **builder** scaffolds the project per `CLAUDE.md`'s Stack as its step 0. Don't scaffold here, don't skip the writer or designer.
1. Call the **writer** subagent with the request above. Wait until `.craft/copy.md` is written. If its first line is `STATUS: DRAFT — blocked`, stop here (see **Fatal** below) — don't design around missing copy.
2. Call the **designer** subagent with the request. It reads `.craft/copy.md` as the copy source of truth and lays it out. Wait until `.craft/design.md` is written. If its first line is `STATUS: DRAFT — blocked`, stop here (see **Fatal** below) — don't send a blocked spec to the builder.
3. Call the **builder** subagent to implement. Wait until `.craft/build-notes.md` is written.
4. Call the **qa** subagent to check the result. Wait until `.craft/qa-report.md` is written.
5. Show the user a summary: copy strategy (core promise), design direction, what was built, and QA status + punch-list.
   - If QA is **NEEDS WORK**: offer to re-run from **builder** (using `.craft/qa-report.md` as the fix list) → qa. Don't loop automatically without user confirmation.
6. **Visual taste loop (REQUIRED)**: start the dev server and look at the result in the browser. Three layers — don't skip any:
   - *Behavior*: answer the 10-question diagnostic from `.claude/skills/ux-research/SKILL.md` §5 while driving the page; every "no" gets a severity (0-4) and severity 3+ goes straight to the punch-list.
   - *Function*: responsive at 375/768/1280px, no horizontal scroll, no console errors.
   - *Taste*: run the `premium-design` Done Check against what you see — zero raw colors? display+body fonts set? every interactive element has a deliberate hover state? Does it feel intentional, or does it still look like a template? If anything is flat/generic, add it to the punch-list. The design isn't done until it passes the taste check, not just the function check.

**Fatal = stop the chain.** Fatal means any of: a subagent finished without writing its output file (`.craft/copy.md` / `.craft/design.md` / `.craft/build-notes.md` / `.craft/qa-report.md`), the copy or design spec says `STATUS: DRAFT — blocked`, or `.craft/build-notes.md` contains a `## BLOCKED` section. On any of these: stop, show the user exactly what's blocked and why, and wait for their call — don't improvise around it and don't re-run the chain hoping it fixes itself.
