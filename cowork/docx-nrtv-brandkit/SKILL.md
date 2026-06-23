---
name: docx-nrtv-brandkit
description: >
  Generates Word documents (.docx) for the client Narrative Strategies using only
  the brand DNA — Montserrat fonts, the navy #103F72 palette, and the NARRATIVE
  logo — applied to a CLEAN, flexible layout built from scratch. Does NOT reproduce
  the official template's cover page, header/footer artwork, or fixed layout.
  Use when the user asks to "make a Narrative-branded Word doc", "apply Narrative
  Strategies branding to this", "use the Narrative fonts and colors", "NRTV brand
  styling without the template layout", "Narrative brand kit document", or wants a
  custom-layout doc that just carries the Narrative look. Do NOT use for the full
  official template with its cover image and exact layout — that is docx-nrtv-brand.
  Do NOT use for Synozur documents (use docx-synozur-brand) or non-Narrative work.
cowork:
  category: writing
  icon: DocumentBulletList
---

# Narrative Strategies — Brand Kit Word Generator

Produces client-ready `.docx` files that carry the **Narrative Strategies brand**
(fonts, colors, logo) on a clean layout you compose for the content at hand. This is
the "brand styling, my layout" path — for the pixel-exact official template (cover
photo, branded header/footer, page numbering), use **docx-nrtv-brand** instead.

The brand elements were extracted from the client's sample document and are bundled in
this skill: see [references/brand.md](references/brand.md) and `assets/`.

## When NOT to Use

- The user wants the **full official Narrative template** with its cover image and
  fixed layout → use `docx-nrtv-brand`.
- The document is for **Synozur** or any other org → use `docx-synozur-brand` or the
  generic `docx` skill.
- The deliverable is a spreadsheet, deck, PDF, or HTML → use `xlsx` / `pptx` / `pdf` / `html`.
- A plain, unbranded Word doc is fine → use the built-in `docx` skill.

## Brand Quick Reference

| Element | Value |
|---------|-------|
| Headings | Montserrat SemiBold, navy `#103F72` |
| H3 / minor | Montserrat Medium, navy `#103F72` |
| Body | Montserrat, ~10pt |
| Accents | Slate `#477499` / `#60769C`, steel `#80A0BC` |
| Fills | Pale blue `#E6EBF1` (zebra), light gray `#E8E8E8` (rules) |
| Logos | `assets/narrative-logo-full.png` (wordmark), `assets/narrative-mark.png` ("N") |

Full palette and usage rules: [references/brand.md](references/brand.md).

## Workflow

1. **Gather the content.** If the user supplied text, an outline, or a source file,
   use it. If facts are missing (names, dates, numbers), insert a clearly-marked
   placeholder like `[Add Q3 figure]` — never fabricate. Search M365 (`SearchM365`,
   `ListMessages`) first when the content lives in the user's workspace.
2. **Compose a content spec** as JSON for `scripts/build_doc.py` — pick a layout that
   fits the document (brief, memo, one-pager, report). Schema is documented at the top
   of the script: `title`, `subtitle`, `meta`, `logo` (`full`/`mark`/`none`), and a
   `blocks` list (`h1`/`h2`/`h3`/`p`/`bullet`/`number`/`quote`/`rule`/`table`).
3. **Write the spec** to `working/nrtv_content.json` (use the `Write` tool).
4. **Generate** with Bash:
   `python3 /mnt/user-config/.claude/skills/docx-nrtv-brandkit/scripts/build_doc.py working/nrtv_content.json output/<Name>.docx`
5. **Verify delivery (BLOCKING):** `Glob output/**/*.docx` to confirm the file exists.
   If missing, locate it and move it into `output/`, then re-check.
6. **Numeric accuracy:** any total, percentage, or delta in the document must be
   computed with a code tool, not by hand.
7. **Tell the user** the file is ready by its filename (e.g. "Your Narrative-branded
   brief is ready — Strategic-Brief.docx"). Note that Montserrat renders if installed
   on their machine; otherwise Word substitutes the nearest sans-serif.

## Output Format

A single `.docx` in `output/`, with: the NARRATIVE wordmark in the header, a navy title
block over a brand rule, Montserrat throughout, navy headings, and navy/pale-blue tables.
Layout is chosen per document — not a fixed template.

## Guardrails

- **Brand elements only, not the template layout** — this is the whole point of the
  skill. Do not copy the sample's cover page or header art; compose a fresh layout.
- **Logos on light backgrounds only** — the bundled logos are navy on transparent; no
  reversed (white) version exists. Never place them on a navy fill.
- **Never fabricate facts** (names, numbers, quotes, dates) — use visible placeholders.
- **Do not alter brand values** — keep `#103F72`, the Montserrat family, and the logos
  as defined in `references/brand.md` unless the user explicitly overrides them.
- **Confirm the file exists in `output/`** before reporting success.
