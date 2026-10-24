---
name: seo-content-strategist
description: Use when writing page copy, SEO decided at write time, not patched at QA. Keyword placement, heading hierarchy as content structure, meta description as ad copy, JSON-LD planning, and alt text that serves both readers and search.
---

# SEO Content Strategist

Core belief: SEO is a **writing decision, not a QA finding**. The heading hierarchy IS the
message hierarchy; the meta description IS ad copy; keywords land naturally where the copy
is already strongest. If SEO gets bolted on after the build, the copy and the markup fight
each other: decide both together, in `.craft/copy.md`.

## 1. Heading hierarchy = content structure

- Exactly ONE H1 per page: it carries the core promise AND the primary keyword, naturally.
- H2s mark the page's sections in the persuasion arc order; H3s subdivide. Never skip a
  level for styling (h2 → h4 is a QA finding you created at write time).
- Write headings people search for: the user's words (see `conversion-copy` language rules),
  not internal jargon.

## 2. Keyword prominence: natural placement only

- Primary keyword appears in: the H1, the first paragraph, the `<title>`, and (when the
  page owns its URL) the slug. Once each is enough: placement beats repetition.
- Secondary keywords go in H2s ONLY where they fit the message; never bend a heading to
  stuff a keyword. A heading that reads awkwardly loses more visitors than it gains clicks.
- Record the chosen primary keyword at the top of the copy's SEO notes so the Designer
  and Builder preserve the placements.

## 3. Meta tags: organic ad copy

- `<title>`: ≤60 chars, core promise + keyword, brand at the end ("Promise: Brand").
- Meta description: <155 chars, written as ad copy: outcome + differentiator + a soft CTA.
  It doesn't affect ranking; it affects CLICK-THROUGH. Write it like the one sentence that
  wins the click on a results page.
- Both go into `.craft/copy.md` under **SEO notes**: the Builder implements them verbatim.

## 4. Structured data (JSON-LD)

- When the content type warrants it (product, FAQ, article, review), specify WHICH
  JSON-LD type in the copy's SEO notes and which on-page content feeds it (FAQ questions
  map 1:1 to the FAQ section's real copy: never invent Q&As for the markup).
- No content type match → write "JSON-LD: none warranted" so QA knows it was a decision,
  not an omission.

## 5. Alt text: for readers first, search second

- Every meaningful image gets alt text describing what it SHOWS in context ("dashboard
  filtering candidates by skill": not "image1", not a keyword string).
- Decorative images: empty `alt=""`, because decoration described is noise for screen readers.
- Specify alt text in the copy/design spec for every named image asset, so the Builder
  never invents it.

## Done check

- [ ] One H1 = core promise + primary keyword; H2/H3 sequence has no skipped levels
- [ ] Primary keyword: H1 + first paragraph + title (+ slug when applicable), each once
- [ ] `<title>` ≤60 chars and meta description <155 chars written as ad copy, in SEO notes
- [ ] JSON-LD type chosen (or "none warranted") with its content source named
- [ ] Alt text written for every meaningful image; `alt=""` marked for decorative ones

> Credits: adapted from the `seo-content-strategist` skill in
> [antigravity-landing-template](https://github.com/redhoram/antigravity-landing-template) (same author, MIT).
