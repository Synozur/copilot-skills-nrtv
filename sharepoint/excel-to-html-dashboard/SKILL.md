---
name: Excel to Branded HTML Dashboard
description: Convert an Excel workbook stored in SharePoint into a self-contained, branded HTML dashboard that surfaces key data, tables, and summaries as readable web content. Use when a user asks to "turn a spreadsheet into a dashboard", "publish Excel data as a webpage", "create an HTML report from a workbook", "make our data visible without Excel", or "convert a spreadsheet to a branded page".
---

1. Locate the Excel file.
   - If the user specifies a file name or URL, retrieve it directly.
   - If the user is vague, search the current site or library for `.xlsx` files and present up to five recent matches for selection. Do not proceed until a specific file is confirmed.

2. Inspect the workbook structure before extracting content:
   - List all worksheets by name and tab color (if set)
   - Identify named ranges, Excel Tables (ListObjects), and chart objects
   - Note any sheets that appear to be raw data dumps vs. summary or report sheets (signal: a summary sheet often has fewer rows, more labels, and merged cells)
   - Ask the user which sheets to include if more than three sheets are present, unless one sheet is clearly named "Dashboard", "Summary", or "Report" — in that case default to that sheet and note the assumption

3. Extract content from each included sheet:
   - **Summary cells and KPIs:** single-value cells with adjacent labels (e.g., "Total Revenue: $1.2M") → extract as headline metric tiles
   - **Excel Tables:** extract headers and all data rows → render as HTML `<table>` with sortable column headers
   - **Named ranges with labels:** treat as labeled data blocks → render as definition lists or key-value pairs
   - **Charts:** note the chart title, type (bar, line, pie, etc.), and the data range it references → render as a descriptive card with the chart title and a plain-text summary of the data (do not attempt to reproduce the chart visually)
   - **Free-form text cells:** include headings and notes that appear to be commentary or instructions; omit formula-only cells

4. Determine branding signals in this order of preference:
   - Tab colors set on the included sheets (use as accent colors)
   - The SharePoint site's theme colors if accessible
   - If neither is available, use a clean neutral palette (white background, `#323130` text, `#0078D4` accent) and note this in the output
   - Prompt the user for a primary hex color only if they have explicitly said they want custom branding; otherwise proceed with the best available signal

5. Map workbook content to dashboard layout:
   - Workbook title or file name → page header
   - Each included sheet → a named `<section>` with a heading matching the sheet tab name
   - KPI/metric tiles → a horizontally arranged row of highlight cards at the top of each section
   - Tables → full-width below the KPI row
   - Chart description cards → placed adjacent to the table the chart references, or in a separate "Charts" subsection
   - Include a sticky top navigation bar with anchor links to each sheet section

6. Generate a self-contained HTML file:
   - Inline all CSS; do not reference external stylesheets or CDNs
   - Apply a responsive layout using CSS Grid or Flexbox
   - KPI tiles: bold value, smaller label, accent-colored top border
   - Tables: striped rows, sticky header row, horizontal scroll on narrow viewports
   - Mark the source file name and generated date in the page footer

7. Present the generated HTML to the user:
   - Show a concise preview summary: sheets included, number of tables, number of KPI tiles, any content skipped (e.g., charts rendered as text, sheets excluded)
   - Offer the HTML as a downloadable artifact or as inline code the user can copy

8. Do not:
   - Fabricate data values not present in the workbook
   - Include formulas, cell references, or Excel-specific syntax in the output
   - Modify or overwrite the original Excel file
   - Upload the HTML file to SharePoint without explicit user confirmation
   - Render personally identifiable information (names, email addresses, employee IDs) in a dashboard without first confirming the user intends this to be shared

9. If the workbook or any sheet is marked confidential (e.g., "CONFIDENTIAL", "INTERNAL ONLY" in a header row or sheet name), add a visible banner to the top of the generated HTML page reading: **"This content is marked confidential. Review distribution before sharing."**
