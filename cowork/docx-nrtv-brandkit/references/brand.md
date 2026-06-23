# Narrative Strategies — Brand Kit (extracted from client sample)

Source: client-provided `Sample.docx`. These are the **brand elements only** — fonts,
colors, and logos. The sample's cover page, header/footer art, and page layout are
intentionally NOT reproduced by this skill.

## Typography (Montserrat family)

| Role        | Typeface              | Notes |
|-------------|-----------------------|-------|
| Title       | Montserrat SemiBold   | All-caps optional, navy `#103F72` |
| Heading 1   | Montserrat SemiBold   | navy `#103F72`, ~14pt |
| Heading 2   | Montserrat SemiBold   | navy `#103F72`, ~12pt |
| Heading 3   | Montserrat Medium     | navy `#103F72`, ~10.5pt |
| Heading 4   | Montserrat            | slate `#60769C` |
| Body        | Montserrat            | ~10pt, near-black |
| Quote / callout | Montserrat        | slate `#60769C`, italic |

Montserrat is a Google font. If it isn't installed on the reader's machine, Word
falls back to the nearest sans-serif — the document still carries the brand name in
its style definitions, so no action is needed at generation time.

## Color palette (theme1.xml)

| Token        | Hex       | Use |
|--------------|-----------|-----|
| Navy (primary)   | `103F72` | headings, titles, logo, rules |
| Dark navy        | `0E2841` | deep accents, footer text |
| Slate blue       | `477499` | links, secondary headings, table header fill |
| Slate (muted)    | `60769C` | H4, quotes, captions |
| Steel blue       | `80A0BC` | light dividers, chart accents |
| Pale blue        | `E6EBF1` | table zebra fill, callout background |
| Light gray       | `E8E8E8` | hairline rules, table borders |
| White            | `FFFFFF` | page, reversed text on navy |

RGB quick reference: navy = (16, 63, 114); slate = (71, 116, 153); muted = (96, 118, 156);
pale = (230, 235, 241); gray = (232, 232, 232).

## Logos (in `assets/`)

| File | Dimensions | Use |
|------|-----------|-----|
| `narrative-logo-full.png` | 524×96 (≈5.46:1) | Primary lockup — "N" mark + NARRATIVE wordmark. Default for headers/cover line. Render ~1.6–2.0" wide to stay crisp. |
| `narrative-mark.png` | 90×108 (≈0.83:1) | Standalone "N" mark. Use small, in footers or as a corner accent (~0.3–0.4" tall). |

Logos are navy on transparent — place on white or pale-blue backgrounds only, never on
navy (no reversed version is provided).
