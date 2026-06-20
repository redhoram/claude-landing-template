---
description: Spin up a strong draft for a page/section from scratch — Designer → Builder → QA. For the 0→1 moment; polish interactively after.
---

User request: $ARGUMENTS

This is for **building a strong first draft** (0→1). After it's done, further polish happens interactively in the main session (or `/polish`) — DON'T re-run this command for small tweaks.

Run in order, don't skip:

0. **Clean the workspace**: delete old `.craft/design.md`, `.craft/build-notes.md`, `.craft/qa-report.md` if present. Do NOT delete `.gitkeep`.
1. Call the **designer** subagent with the request above. Wait until `.craft/design.md` is written.
2. Call the **builder** subagent to implement. Wait until `.craft/build-notes.md` is written.
3. Call the **qa** subagent to check the result. Wait until `.craft/qa-report.md` is written.
4. Show the user a summary: design direction, what was built, and QA status + punch-list.
   - If QA is **NEEDS WORK**: offer to re-run from **builder** (using `.craft/qa-report.md` as the fix list) → qa. Don't loop automatically without user confirmation.
5. **Visual verification in the main session**: start the dev server, look at the result in the browser, check responsiveness. This step is REQUIRED — the design isn't done until it's actually seen.

If any subagent reports a fatal problem, stop and report to the user.
