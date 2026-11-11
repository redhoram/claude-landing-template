---
description: Set or reset the project's brand system (palette, typography, rhythm, motion, voice) into .craft/brand.md. Runs the curator on its own, outside /craft.
---

Notes from the user: $ARGUMENTS

You are the Creative Manager. Use this to set the brand system the first time, or to redo it after a rebrand. `/craft` already runs the curator by itself when the Brand section of `CLAUDE.md` is empty, so you only need this command for a deliberate brand pass.

1. If `.craft/brand.md` exists, MOVE it to `.craft/archive/<YYYYMMDD-HHMM>/brand.md` first so the previous system is never lost. Tell the user in one line that you archived it.
2. If there is no visual reference (URL or style description) in `CLAUDE.md` or in the notes above, ask the user ONE question: *"Any site or app you love the look of? Drop a link or describe the vibe."* If they skip it, proceed without and never re-ask.
3. **Model override**: read the `## Model override` table in `CLAUDE.md`. If the curator is listed, pass that model when spawning it.
4. Call the **curator** subagent with the notes above. Wait until `.craft/brand.md` is written. If its first line is `STATUS: BLOCKED`, stop and show the user exactly what is blocked.
5. Show the user a short summary: direction, palette with roles, typography, and the assumptions the curator made. Ask them to confirm or correct the assumptions before the next `/craft`.

Don't run the rest of the craft chain from here. A brand system is set once; pages use it.
