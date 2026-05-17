---
name: Content Expiration Sentinel
description: Identify potentially outdated or unmanaged content in SharePoint by analyzing activity, ownership, and content signals, and flag items that likely require review.
---

1. Scan documents and pages in this site or library.

2. For each item, evaluate signals including:
   - last modified date
   - last accessed (if available)
   - presence of an owner or author
   - content indicators such as "policy", "procedure", or "guideline" in title or text

3. Identify items that are likely to require review based on:
   - long periods without updates (e.g., significantly older than similar content in the library)
   - missing or unclear ownership
   - indicators that the content is authoritative or reference material

4. If explicit review metadata exists (for example: review date, expiration date), use it to refine the assessment.

5. Classify flagged items into:
   - High Priority (likely outdated and high-impact content)
   - Medium Priority (possibly outdated or unclear ownership)
   - Low Priority (older but likely low-risk content)

6. Output a prioritized report including:
   - document or page title (with link if available)
   - last modified date
   - owner (if known)
   - reason for flag (for example: no recent updates, missing owner)

7. Summarize patterns observed (for example: clusters of outdated content, ownership gaps).

8. Do not modify, move, or delete content. Output findings only.