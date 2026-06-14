---
name: PowerPoint to Branded HTML Dashboard
description: Convert a PowerPoint file stored in SharePoint into a self-contained, branded HTML dashboard page that reflects the presentation's visual identity, structure, and key content. Use when a user asks to "turn a deck into a dashboard", "publish slides as a webpage", "create an HTML summary from a presentation", or "convert PowerPoint to a branded page".
---

1. Locate the PowerPoint file.
   - If the user specifies a file name or URL, retrieve it directly.
   - If the user is vague, search the current site or library for `.pptx` files and present up to five recent matches for selection. Do not proceed until a specific file is confirmed.

2. Extract content from the presentation:
   - Slide titles (used as section headings)
   - Body text, bullet points, and speaker notes (if present)
   - Data tables and charts (convert to descriptive text or HTML tables)
   - Image alt text or descriptive captions where images are significant
   - Slide order (preserve as page section order)

3. Extract branding signals from the presentation:
   - Primary and accent colors from slide backgrounds and shape fills (use hex values where determinable)
   - Font families used for headings and body text
   - Logo or wordmark presence (note position: header, footer, or corner)
   - Overall layout direction (wide/horizontal, vertical stack, grid)
   - If branding signals cannot be reliably extracted, use a clean neutral palette (white background, dark text, blue accent) and note this in the output.

4. Map the presentation structure to dashboard sections:
   - First slide → page header (title, subtitle, optional logo placeholder)
   - Section-divider slides (slides with only a title and no body) → section headers
   - Content slides → cards or panels, one per slide
   - Final slide → footer or call-to-action block

5. Generate a self-contained HTML file:
   - Inline all CSS; do not reference external stylesheets or CDNs
   - Use extracted brand colors and fonts (fall back to system-safe font stacks if custom fonts are not web-safe)
   - Apply a responsive grid layout using CSS Grid or Flexbox
   - Each slide becomes a `<section>` with a heading, body content, and a subtle card style (border, shadow, or background tint drawn from brand palette)
   - Include a sticky top navigation bar with anchor links to each section if the deck has five or more slides
   - Mark the generated date in the page footer

6. Present the generated HTML to the user:
   - Show a concise preview summary: number of sections, colors used, font choices, and any content that could not be converted (e.g., embedded videos, complex diagrams)
   - Offer the HTML as a downloadable artifact or as inline code the user can copy

7. Do not:
   - Fabricate content not present in the slides
   - Include raw base64-encoded images unless the user explicitly requests it
   - Modify or overwrite the original PowerPoint file
   - Upload the HTML file to SharePoint without explicit user confirmation

8. If the presentation contains confidential markers (e.g., "CONFIDENTIAL", "INTERNAL ONLY" in the footer or title), add a visible banner to the top of the generated HTML page reading: **"This content is marked confidential. Review distribution before sharing."**
