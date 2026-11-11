---
description: Audit SEO on a page that already exists (headings, title, meta, structured data, alt text, agreement with the SEO plan). Runs the optimizer in audit mode and reports; changes nothing.
---

Target: $ARGUMENTS

Use this to check a page that is already built or live. For a new page, `/craft` runs the optimizer in plan mode before the copy is written.

1. If the target is empty, audit the page(s) in the current project. If it names a file, a route, or a URL, audit that.
2. **Model override**: read the `## Model override` table in `CLAUDE.md`. If the optimizer is listed, pass that model when spawning it.
3. Call the **optimizer** subagent in **audit mode** with the target. Wait until `.craft/seo-audit.md` is written. If it was not written, stop and tell the user.
4. Show the user the status, the findings by severity, and the punch-list. Say plainly what the optimizer did not check (it has no search data, so keyword choices are assumptions).
5. Offer to apply the fixes yourself, as the Creative Manager. Do not change code before the user agrees.
