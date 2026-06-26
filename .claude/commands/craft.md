---
description: Spin up a strong draft for a page/section from scratch — Designer → Builder → QA. For the 0→1 moment; polish interactively after.
---

User request: $ARGUMENTS

This is for **building a strong first draft** (0→1). After it's done, further polish happens interactively in the main session (or `/polish`) — DON'T re-run this command for small tweaks.

Run in order, don't skip:

0. **Reference check + workspace clean**: if no visual reference (URL or style description) exists in `CLAUDE.md`'s Brand section, ask the user once: *"Any site or app you love the look of? Drop a link or describe the vibe — I'll use it as the taste benchmark."* Wait briefly for a reply; if none comes or they skip, proceed without it. Then delete old `.craft/design.md`, `.craft/build-notes.md`, `.craft/qa-report.md` if present. Do NOT delete `.gitkeep`.
1. Call the **designer** subagent with the request above. Wait until `.craft/design.md` is written.
2. Call the **builder** subagent to implement. Wait until `.craft/build-notes.md` is written.
3. Call the **qa** subagent to check the result. Wait until `.craft/qa-report.md` is written.
4. Show the user a summary: design direction, what was built, and QA status + punch-list.
   - If QA is **NEEDS WORK**: offer to re-run from **builder** (using `.craft/qa-report.md` as the fix list) → qa. Don't loop automatically without user confirmation.
5. **Visual taste loop (REQUIRED)**: start the dev server and look at the result in the browser. Two layers — don't skip either:
   - *Function*: responsive at 375/768/1280px, no horizontal scroll, no console errors.
   - *Taste*: run the `premium-design` Done Check against what you see — zero raw colors? display+body fonts set? every interactive element has a deliberate hover state? Does it feel intentional, or does it still look like a template? If anything is flat/generic, add it to the punch-list. The design isn't done until it passes the taste check, not just the function check.

If any subagent reports a fatal problem, stop and report to the user.
