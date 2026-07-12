---
name: ux-research
description: Use when writing a design spec or judging a built page. Behavioral grounding for the Designer — who the user is, which psychology principles apply, ethics hard-lines — and a 10-question usability diagnostic the QA delegates to the main-session taste loop.
---

# UX Research

Core belief: `premium-design` decides whether the page **looks** right; this skill decides
whether it **works for a human**. Every flow, hierarchy, and layout decision must trace to
a reason about the user — "looks clean" is not a reason. A beautiful page that confuses
users is a failed page.

## 1. Ground the design first (Designer, before any visual decision)

Answer in 2-3 sentences at the top of `.craft/design.md`, derived from the request +
`.craft/copy.md` (its Audience & core promise section) + `CLAUDE.md` — NOT from an
invented persona document:

- **Who** lands on this page, and **what job** are they hiring it to do (JTBD)?
- **Context of use**: device (landing = mobile-first reality), how they arrived
  (ad, search, shared link), and what they were doing right before.
- If the audience is genuinely unknowable AND it changes the design → open question
  in the spec; otherwise decide and record the assumption.

## 2. Principle picker — 3-5 per surface, named in the spec

Pick ONLY what fits this surface type; list them in `.craft/design.md` under
**Principles used**, each with WHERE it's applied. Unnamed psychology = decoration.

| Surface | Reach for these first |
|---|---|
| Landing / marketing | Visual hierarchy (one focal point per viewport), Hick's law (ONE primary CTA), social proof near the ask, loss-framing in CTA copy only when true, Von Restorff (the single accent earns attention) |
| Pricing section | Anchoring (order & reference price), chunking of plan differences, compare ≤4 things, transparency beats decoy tricks |
| Signup / waitlist / contact form | Progressive disclosure (ask ONLY what this step needs), goal gradient (show progress), inline validation, error prevention over error messages |
| Feature / product tour section | Recognition over recall (show, don't describe), consistency of pattern per feature card, calm rhythm — persuasion lives in hero and CTA, not everywhere |
| FAQ / objection section | Serial-position effect (strongest answers first and last), plain-language questions users actually ask, one honest answer per objection |

## 3. Usability heuristics — design-time checklist (Designer)

Condensed from Nielsen's 10 + Krug; check while writing the section breakdown:

1. **Self-evident purpose** — 5 seconds on the hero answers: what is this, for whom, why care?
2. **Match the visitor's language** — headings use the user's words, not internal jargon.
3. **Visible status** — every action (form submit, nav click) gives feedback within 100ms.
4. **One path** — the page has ONE primary action; secondary links never compete with it.
5. **Error prevention** — constrain inputs (types, formats shown), disable invalid submits.
6. **Recognition over recall** — nothing requires remembering an earlier section to understand.
7. **Trunk test** — on any scroll position: where am I, what can I do here, where's the CTA?
8. **Minimalism with a job** — every element competes for attention; cut what doesn't serve the core promise.
9. **Errors that help** — form errors in plain language, next to the field, with the fix.
10. **No manual needed** — if a section needs explanation to be understood, redesign it.

## 4. Ethics hard-lines (violating any = design spec is rejected)

- No fake scarcity or countdown timers that reset.
- No confirmshaming ("No thanks, I hate saving money").
- No dark defaults: opt-ins unchecked; the cheaper/lighter choice never hidden.
- No roach motel: leaving (unsubscribe, close popup) as easy as entering.
- Persuasion serves the USER's goal; a principle that only serves conversion at the
  user's expense doesn't get used. People-facing products doubly so.

## 5. Quick diagnostic — 10 questions (QA delegates; main session runs it with eyes on the preview)

The QA is headless: it writes this diagnostic into its report checklist. The main
session answers them while driving the live preview (craft step 6 / polish step 2).
Each "no" = finding with **severity 0-4** + one-line evidence.

1. Within 5 seconds on the hero: is it obvious what this page offers and for whom?
2. Is the primary CTA visually the #1 element, and above the fold at 375px AND 1280px?
3. Does every interactive element give feedback (hover state, submit response)?
4. Can you tell what the product actually does from the page alone (not the pitch)?
5. Does the section order follow the copy's persuasion arc (`.craft/copy.md` flow)?
6. Do form errors appear inline, near the field, in plain language?
7. Is anything essential hidden behind hover-only or below unexpected folds?
8. Mobile 375px: no horizontal scroll, tap targets comfortable, CTA reachable?
9. Empty/loading states: does anything flash, jump, or appear broken while loading?
10. Any §4 ethics violation on screen?

Severity scale: **0** cosmetic · **1** minor annoyance · **2** hurts task completion ·
**3** visitor likely bounces · **4** catastrophic/ethics — severity 3+ = NEEDS WORK
regardless of how good it looks.

## Done check

**Designer:**
- [ ] design.md opens with who + JTBD + context (from copy.md/request, not invented)
- [ ] **Principles used**: 3-5 principles, each mapped to a concrete section
- [ ] §3 checklist passed on the section breakdown
- [ ] Zero §4 violations

**QA / main session:**
- [ ] 10-question diagnostic in the QA report checklist, answered in the taste loop
- [ ] Severity 3+ findings explicitly on the punch-list

> Credits: adapted for this template from the `ux-research` skill in
> [claude-pipeline-template](https://github.com/redhoram/claude-pipeline-template) (same author);
> psychology base from [Nuclear-Marmalade/ux-psychology-skill](https://github.com/Nuclear-Marmalade/ux-psychology-skill) (MIT),
> heuristics condensed in our own words from Nielsen Norman Group and Steve Krug's *Don't Make Me Think*.
