---
name: morning-briefing
description: Composes and sends a daily morning briefing email covering five industry news articles, open communications needing replies, priority client updates, top committed tasks, and today's schedule. Trigger with "send my morning briefing", "morning brief", or run on a daily schedule.
---

# Morning Briefing

Generate and send a personalized daily briefing email. Gather everything in parallel, format as clean scannable HTML, and send it.

## When to use
- The user says "morning briefing", "morning brief", "brief me", "start my day".
- Runs automatically on a daily schedule (see Setup below).

## What to gather

Collect these five sections. Run the lookups in parallel where possible.

### 1. Five news articles relevant to the person's industry
- Use `web_search` to pull the top five stories from the **past 24 hours** relevant to the person's industry and role (infer from their job title, company, and recent work — e.g. a CTO at a consulting firm gets enterprise/AI/technology-strategy news).
- For each: a one-line headline, a one-sentence "why it matters" framed for the person's role, the source, and the date.
- Only use stories you can trace to a current web source. Discard anything outside the 24-hour window.

### 2. Open communications & replies needed
- Check email (`ListMessages`, `SearchM365`) and Teams (`ListChats`, `ListChatMessages`) from the **previous day**.
- Surface threads where the person owes a reply or an action: who is waiting, what they asked, and the specific next step owed.
- **Exclude distribution-list / broadcast traffic.** Skip any message addressed to a distribution list, group alias, or large cc where the person is only copied (not in the To: line directly and not named with an explicit ask). These are FYI/broadcast threads — the person has no action. Examples of patterns to drop: MVP/community DLs, vendor escalation threads addressed to a partner alias where the person is merely cc'd, "reply-all" announcements. A thread only belongs here when the person is a **direct, named recipient with a specific reply or action owed**.

### 3. Priority client updates
- Scan email, Teams, and any project sources for client-facing developments: escalations, ticket numbers, deadlines, blockers, status changes.
- List each with the client name, the development, and any reference IDs.
- **Same distribution-list filter applies.** Only include updates from threads where the person is a direct participant or owner. Drop developments that arrived via a DL/group alias on which the person is just one of many cc's and carries no ownership — those are noise, not priority client signal.

### 4. Top five committed tasks, deliverables & to-dos
- Look **across tasks, emails, Teams, and projects** for the person's five highest-priority open commitments.
- Phrase each as a concrete action with the owner of the next step and any dependency (e.g. "Pull tenant ID from X → send to Y for ticket Z").

### 5. Today's schedule
- Use `ListCalendarView` (with the person's time zone) for today.
- List events chronologically. Flag conflicts/overlaps. Respect privacy: show private/personal events as time blocks ("Private appointment"), not raw titles.
- If there are no timed meetings, say so and note any all-day items.

## Formatting & send

- Subject line: `Morning Briefing — [today's date]` (e.g. "Morning Briefing — May 31, 2026").
- Body: clean HTML, one `<h2>` header per section, scannable and concise. Suggested style:
  - Body: `font-family: 'Segoe UI', Arial, sans-serif; color:#1a1a1a; line-height:1.5; max-width:760px;`
  - Section headers: `color:#810FFB; font-size:18px;` (swap in your own brand color)
- Save the HTML to `output/` first, then send with `SendEmailWithAttachments(to=[<the person's email>], subject=..., body_file_path=..., content_type="HTML")`.
- Before claiming it's sent, confirm the file exists with `Glob output/**/*`.

## Notes
- Never fabricate facts (names, numbers, dates, ticket IDs). If a section has no data, say so rather than filling the gap.
- Keep every section tight — this is a scan-in-60-seconds email, not a report.
