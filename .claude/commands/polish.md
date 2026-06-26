---
description: A quick improvement pass on existing UI — a11y, responsive, micro-interactions, cleanliness. For 1→great iteration.
---

Target: $ARGUMENTS

This is for **iterating (1→great)** on existing UI, not building from scratch. Work directly & interactively (don't use batch subagents):

1. Read `CLAUDE.md` (quality budget + design system) and the target code.
2. Start the dev server, look at the current state in live preview — two layers: *function* (responsive 375/768/1280, console errors) and *taste* (run the `premium-design` Done Check: zero raw colors? deliberate hover states? intentional, not generic? Would a senior designer call this premium?).
3. Fix what's lacking, ordered by impact:
   - Accessibility (contrast, focus ring, `alt`, `aria-label`, `cursor-pointer`)
   - Responsiveness & layout shift
   - Micro-interactions that bring it to life (150-300ms, transform/opacity, respect `prefers-reduced-motion`)
   - Clean code (DRY, dependencies in the right place, light assets)
4. Verify each change in the preview — don't work blind.
5. Report briefly to the user: what was improved + evidence (screenshot/observation).

For a new page/section or a big change, use `/craft`, not this.
