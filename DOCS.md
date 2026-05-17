# Enterprise AI Skills Documentation

This document covers all six AI skills in this repository — three personal skills built for **Copilot Cowork** and three organizational skills built for **Copilot in SharePoint**. Each section explains what the skill does, when to use it, how it works, and how to put it into practice.

---

## Table of Contents

**Copilot Cowork Skills**
1. [Decision Log Builder](#1-decision-log-builder)
2. [Pre-Commitment Capacity Check](#2-pre-commitment-capacity-check)
3. [Stakeholder Intelligence Brief](#3-stakeholder-intelligence-brief)

**Copilot in SharePoint Skills**
4. [Content Expiration Sentinel](#4-content-expiration-sentinel)
5. [Onboarding Path Synthesizer](#5-onboarding-path-synthesizer)
6. [Process Compliance First-Pass](#6-process-compliance-first-pass)

**Summary**
- [Copilot Cowork vs SharePoint Skills](#copilot-cowork-vs-sharepoint-skills)
- [How Skills Scale in an Organization](#how-skills-scale-in-an-organization)

---

# Copilot Cowork Skills

---

## 1. Decision Log Builder

### What It Is

Decision-making is continuous and scattered — across emails, meetings, and chat threads. The Decision Log Builder consolidates those dispersed decisions into a single, structured record with dates, owners, rationale, and source links. It solves the common problem of teams losing track of what was decided, by whom, and why — especially across long-running projects.

### When to Use It

- After a busy quarter, when you need a clear record of every significant call your team made
- Before a project retrospective, to reconstruct the sequence of decisions and who owned them
- When a stakeholder asks "why did we go with this approach?" and you need to find the original context quickly
- When preparing to onboard someone new to a workstream and want to give them decision history without sitting through hours of recordings
- When you notice conflicting directions across workstreams and need to surface whether a formal decision was ever made

### How It Works

The skill begins by confirming the review window — defaulting to the last 30 days if none is specified. It then searches in parallel across email, Teams messages, and calendar meetings for language that signals a finalized decision: phrases like "we decided," "agreed to," "final call," "going with," or "signed off." 

From those results, it filters out opinions, open discussions, and proposals still awaiting approval — retaining only items that establish clear direction. Each qualifying decision is captured with its date, a one-sentence summary, identifiable participants, stated rationale (never inferred), accountable owner, and a linked reference back to the original source.

Where the same decision appears across multiple sources — for example, a meeting and a follow-up confirmation email — the skill merges them into a single entry. It flags two categories of risk: decisions with no clear owner and decisions that appear to conflict across sources. The final output is a structured table followed by a short narrative on key themes, ownership gaps, and conflicting directions.

### How to Build It

Place the `SKILL.md` file at:

```
cowork/
  decision-log-builder/
    SKILL.md
```

The front matter must include `name`, `description`, and `cowork` metadata with a `category` and `icon` field. No additional configuration files are required.

### How to Use It

- *"Log all decisions from the past month across my email and Teams."*
- *"What did we decide on the Henderson project? Build me a decision log."*
- *"Why was this approach approved? Show me the decision history."*
- *"What have we agreed to in the last six weeks? Capture it in a table."*
- *"Build a decision log for the Q2 planning workstream."*

### Example Output

| Date | Decision | Owner | Source |
|------|----------|-------|--------|
| May 3 | Proceed with vendor A for the data integration layer | J. Torres | [msg_12] |
| May 9 | Defer the mobile release to Q3 | Unassigned ⚠️ No owner | [evt_4], [msg_17] |
| May 14 | Approve revised scope excluding legacy migration | R. Patel | [chat_6] |

**Key Themes & Risks:** Three of seven decisions lack a named owner, creating execution risk in the integration track. Two decisions — on release scope — show conflicting language across sources and should be reviewed before the next milestone.

### Key Design Principles

- **Source-grounded output only.** Every decision entry must trace to a specific email, meeting, or chat. Nothing is fabricated or inferred.
- **Rationale is captured, not constructed.** If the reason for a decision wasn't explicitly stated in the source material, the field is left blank.
- **Flags, not fixes.** The skill surfaces ownership gaps and conflicts — it does not attempt to resolve them or assign owners on the user's behalf.

---

## 2. Pre-Commitment Capacity Check

### What It Is

Professionals routinely overcommit because they agree to new work based on intuition rather than actual availability. The Pre-Commitment Capacity Check reviews a person's real workload — calendar, sent email, and recent Teams conversations — before they say yes to a new engagement, SOW, or project. It produces a concrete recommendation with named tradeoffs, not a generic "you're busy."

### When to Use It

- Before signing a statement of work or accepting a new client engagement
- When a colleague asks if you can lead a project and you want an honest answer before responding
- When evaluating whether the current quarter can absorb an additional commitment
- Before agreeing to a delivery deadline that feels optimistic
- When a proposal or estimate has been shared and you want to stress-test whether your team can actually deliver it

### How It Works

If a document — such as a SOW, proposal, or estimate — is referenced, the skill reads it first, extracting total hours, phases, required roles, deliverables, and scope boundaries. It then compares the user's informal description of the engagement against the document's actual scope and flags any mismatch before touching the capacity math.

Next, the skill runs three parallel workload sweeps: a 30-day calendar scan to identify blocked weeks, travel, OOF periods, focus blocks, and recurring commitments; a review of the last two weeks of sent email for explicit promises ("I'll have this to you by Friday"); and a scan of recent Teams chats for open asks and in-progress threads likely to convert to real work.

From this data, the skill computes available hours per week, compares them against the engagement's requirements, and matches project phases to realistic windows. It concludes with one of three clear recommendations — take it on solo, take it on with a partner or role split, or decline and defer — accompanied by a confidence score. Anything below 75% confidence includes an explicit statement of what information is missing.

### How to Build It

Place the `SKILL.md` file at:

```
cowork/
  pre-commitment-capacity-check/
    SKILL.md
```

The front matter uses a multi-line `description` block listing all trigger phrases and exclusions. The `cowork` block sets `category: analysis` and specifies an icon.

### How to Use It

- *"Can I take on the Meridian SOW? Here's the proposal."*
- *"Should I commit to leading this engagement? Check my capacity."*
- *"Is this a good time to add another workstream?"*
- *"Bandwidth check — do I have room to sign this before end of month?"*
- *"Before I agree to this, review my next six weeks."*

### Example Output

```
Recommendation (confidence ~82): Take it on with a partner — capacity exists but 
June is constrained.

Scope reality check: You described this as a "strategy redesign." The SOW defines 
it as narrative refinement and explicitly excludes rebranding. Confirm scope before 
proceeding.

Engagement: 120h / $48,000 / ~6 weeks. Phases: Discovery (20h), Workshops (40h), 
Synthesis (40h), Final delivery (20h).

Current obligation load:
- Committed: Week of June 2 fully blocked (offsite); "I'll have the report by June 7" 
  sent to M. Allen on May 28.
- Likely incoming: Open ask from D. Kim re: budget narrative (Teams, May 30 — 
  unanswered).

High-capacity weeks: June 16–20, June 23–27.

Suggested split: Delegate Discovery phase to a junior analyst; you own Workshops 
and Synthesis in the June 16 window.
```

### Key Design Principles

- **Scope before capacity.** A framing mismatch between what the user thinks they're agreeing to and what the document actually says is surfaced first — capacity math on the wrong scope is meaningless.
- **Committed work is not just what's on the calendar.** Sent-email promises and open Teams asks are treated as real obligations, even when they don't appear as meetings.
- **Specificity is non-negotiable.** The recommendation names specific weeks, dates, and roles. Generic statements like "you seem busy but it could work" are explicitly prohibited.

---

## 3. Stakeholder Intelligence Brief

### What It Is

Walking into a meeting without context is a missed opportunity. The Stakeholder Intelligence Brief scans the last 90 days of a user's email and Teams history with a specific person and produces a structured, evidence-based snapshot in two minutes. It surfaces open commitments, unresolved threads, and observable communication patterns — so the user arrives informed, not scrambling.

### When to Use It

- Before a one-on-one with an executive or client you haven't spoken to in several weeks
- When preparing for a difficult conversation and needing to know what has been promised or left open
- When picking up a relationship that a colleague has been managing and you need a quick handoff brief
- Before a quarterly review with a key stakeholder to ensure no open items are missed
- When a stakeholder contacts you unexpectedly and you want to get up to speed before responding

### How It Works

The skill begins by resolving the person's identity against the directory, surfacing candidates if the name is ambiguous rather than guessing. It then runs four concurrent lookups across email (messages received from and sent to the person) and Teams (direct chat history and any channel mentions), covering the past 90 days.

From those results, it extracts three categories of signal: commitments the user made (things they said they would do, with dates and message citations); open or unresolved items (questions from the stakeholder with no visible reply, or promised deliverables with no follow-through); and communication patterns (cadence, response gaps, and any urgent or escalation language, quoted verbatim without interpretation).

If the history is thin — fewer than roughly five messages — the skill says so plainly and summarizes only what exists. It does not pad the output with speculation. The final briefing is delivered as inline markdown with four clearly labeled sections, each grounded in cited sources.

### How to Build It

Place the `SKILL.md` file at:

```
cowork/
  stakeholder-intelligence-brief/
    SKILL.md
```

The front matter uses a multi-line `description` block with trigger phrases. The `cowork` block sets `category: productivity` and specifies the `PersonInfo` icon.

### How to Use It

- *"Prep me for my meeting with Sarah Chen this afternoon."*
- *"Brief me on Marcus before our call — what's open between us?"*
- *"What have I committed to Director Wang in the last three months?"*
- *"Get me up to speed on my history with the Apex account lead."*
- *"Stakeholder brief on Jordan — we haven't spoken in a while and I need context."*

### Example Output

**Relationship Snapshot**
Sarah Chen — VP of Operations, Alliance Partners. Regular interaction over the past 90 days, averaging roughly two exchanges per week, with a notable gap in April.

**Commitments Made**
- "I'll have the updated timeline to you by Friday" — May 12 [msg_4]
- "We'll share the cost model before the board review" — April 28 [msg_11]

**Open or Unresolved Items**
- Sarah asked for confirmation on the revised scope on May 8 — no reply found [msg_7]
- Follow-up promised on Q2 resourcing (April 15) — no closing message found [msg_2]

**Communication Pattern Signals**
- Cadence: consistent weekly exchanges, except a three-week gap in April
- Escalation language present: "urgent" (May 8, [msg_7]); "please advise" (May 14, [chat_3])
- Two messages from Sarah currently unanswered

### Key Design Principles

- **Observation, not interpretation.** The skill reports what is visible in messages — it does not infer sentiment, relationship health, or intent beyond the written record.
- **Verbatim escalation signals.** Urgency language is quoted exactly as written. The skill does not characterize tone or make judgments about the relationship.
- **Honesty about data gaps.** If the history is sparse, the briefing says so — it does not fill space with generic observations.

---

# Copilot in SharePoint Skills

---

## 4. Content Expiration Sentinel

### What It Is

SharePoint environments accumulate content over time, and outdated policies, procedures, and reference documents create real risk when people rely on them. The Content Expiration Sentinel scans a SharePoint site or library and identifies content that is likely overdue for review — prioritized by impact and ownership status. It gives content managers and governance leads a clear starting point, rather than a manual audit.

### When to Use It

- When preparing for an annual content governance review and need to know where to focus first
- When a compliance team asks whether policy documents are current before a certification or audit
- When a site has grown organically and no one has a clear picture of what is stale
- When onboarding a new content owner and they need to understand the state of what they're inheriting
- When organizational changes (rebranding, restructuring, regulatory updates) require a targeted sweep of affected content

### How It Works

The skill scans every document and page in the specified site or library, evaluating each item against a set of observable signals: how long ago it was last modified, when it was last accessed (where that metadata is available), whether it has a named owner or author, and whether its title or content suggests it is authoritative material — such as a policy, procedure, or guideline.

Items without explicit review or expiration metadata are assessed comparatively — content that is significantly older than similar items in the same library is treated as a candidate for review. Where formal review metadata exists (such as a "Review Date" column), that takes precedence.

Each flagged item is classified into one of three priority tiers: High Priority for content that appears outdated and carries high organizational impact; Medium Priority for content that is possibly stale or has unclear ownership; and Low Priority for older content that appears lower risk. The output is a prioritized report with title, last modified date, owner, and the specific reason for the flag, followed by a summary of patterns — such as clusters of outdated content within a particular team's area or systemic ownership gaps.

The skill does not modify, move, or archive any content. It produces findings only.

### How to Build It

Place the `SKILL.md` file at:

```
sharepoint/
  content-expiration-sentinel/
    SKILL.md
```

The front matter requires `name` and `description`. Unlike Cowork skills, SharePoint skills do not use the `cowork` metadata block. The skill is activated by Copilot in SharePoint based on the description and user intent.

### How to Use It

- *"Which documents in this library haven't been updated in over a year?"*
- *"Run a content health check on this site — flag anything that looks outdated."*
- *"Which policies here are missing owners or review dates?"*
- *"Give me a prioritized list of content that needs attention before our audit."*
- *"What's stale in the HR policies library?"*

### Example Output

**Content Expiration Report — HR Policies Library**
*Scan date: May 17, 2026 | Items reviewed: 84 | Items flagged: 19*

**Summary Pattern:** 11 of 19 flagged items are in the Benefits & Compensation folder, with no updates since 2022. Six items lack any named owner.

| Priority | Title | Last Modified | Owner | Reason |
|----------|-------|--------------|-------|--------|
| 🔴 High | Remote Work Policy | Jan 2022 | None | No updates in 3+ years; no owner; policy content |
| 🔴 High | Data Retention Procedure | Mar 2021 | L. Morrison | Referenced in compliance review; not updated since |
| 🟡 Medium | Onboarding Checklist v2 | Aug 2023 | P. Reyes | Newer version (v3) found in same library |
| 🟢 Low | Office Supply Request Form | Sep 2022 | M. Grant | Infrequently used; low impact |

### Key Design Principles

- **Read-only operation.** The skill never modifies, moves, or deletes content under any circumstances — it outputs findings only.
- **Evidence-based classification.** Each flag is tied to a specific, observable signal (age, missing metadata, content type). The skill does not speculate about whether content is incorrect.
- **Patterns over individual items.** The summary section is designed to surface systemic issues — clusters, ownership gaps, structural problems — not just a long list of individual flags.

---

## 5. Onboarding Path Synthesizer

### What It Is

New hires and role transitions are expensive when onboarding is unstructured. The Onboarding Path Synthesizer reads a SharePoint site and assembles a structured, role-specific reading path from the content already there — organized into what a new person needs in their first week, what provides useful background, and what they'll consult on an ongoing basis. It removes the guesswork from onboarding design without requiring a content overhaul.

### When to Use It

- When a new hire is starting and a manager wants to give them a curated starting point rather than a folder full of links
- When someone moves into a new role and needs to get oriented quickly without reading everything
- When a team is scaling and onboarding needs to be consistent without being manually maintained
- When a new vendor, contractor, or partner needs to get up to speed on how the organization works
- When reviewing whether existing onboarding materials are sufficient before a hiring wave

### How It Works

The skill begins by asking for the role's description or key responsibilities if they haven't been provided. It then scans the SharePoint site for relevant content across all available content types — documents, pages, lists, guides, training materials, and policies — using the role description as a relevance filter.

Content is ranked by three factors: relevance to the stated role, recency (recently updated content is favored over older material), and the presence of a clear owner or official designation suggesting it is authoritative. From this ranked set, the skill constructs a three-tier onboarding path: First Week (essential reading, capped at seven items to avoid overwhelm), Background (helpful context for deeper understanding), and Reference (materials to consult when specific situations arise).

Each item in the path includes the document title with a link and a single sentence explaining why it is relevant to this specific role. If the site does not contain enough structured content to build a meaningful path, the skill states this clearly rather than padding the output with marginal material. No content is created or modified — the output is guidance only.

### How to Build It

Place the `SKILL.md` file at:

```
sharepoint/
  onboarding-path-synthesizer/
    SKILL.md
```

The front matter requires `name` and `description`. The skill is activated by Copilot in SharePoint when a user asks for onboarding guidance, training paths, or reading recommendations for a new hire.

### How to Use It

- *"Build an onboarding path for a new project manager joining next week."*
- *"What should a new HR Business Partner read in their first week?"*
- *"Create a reading list for our new data analyst — focus on what's most important first."*
- *"What training materials on this site are relevant for someone in a client-facing role?"*
- *"Give me a structured onboarding guide I can share with our new team lead."*

### Example Output

**Onboarding Path: Senior Business Analyst**
*Based on content available in the Strategy & Operations site*

---

**First Week** *(Essential — read before day 5)*

1. [How We Work: Operating Principles](link) — Establishes the decision-making norms and communication expectations you'll encounter immediately.
2. [Project Intake & Prioritization Process](link) — Explains how new work is initiated and approved; you'll need this in your first stakeholder meeting.
3. [Stakeholder Directory & Account Map](link) — Identifies key contacts across the business and their areas of accountability.
4. [Analytics Environment Overview](link) — Covers the tools, platforms, and data access procedures relevant to this role.
5. [Q2 Strategy Priorities](link) — Current organizational priorities that will shape your initial workload.

**Background** *(Read in weeks 2–4)*

- [Business Review Cadence & Templates](link) — Context for recurring reporting cycles you'll eventually own.
- [Historical Project Archive: Selected Cases](link) — Useful for understanding how similar problems have been approached in the past.

**Reference** *(Consult as needed)*

- [Data Governance Policy](link) — Required reading before accessing production data.
- [Finance Approval Thresholds](link) — Reference when a project requires budget or procurement involvement.

### Key Design Principles

- **Role-specificity over comprehensiveness.** The path is filtered by the stated role, not a dump of everything on the site. Seven items maximum in the First Week tier preserves focus.
- **Recency signals trustworthiness.** Older content that has not been updated is ranked lower, protecting new hires from acting on stale information.
- **Read-only output.** The skill does not create, update, or reorganize any content — it surfaces and structures what already exists.

---

## 6. Process Compliance First-Pass

### What It Is

Most organizations require that certain documents — policies, procedures, contracts, proposals — meet a defined standard before formal review. The Process Compliance First-Pass reads a document against the relevant checklist and identifies exactly what is present, what is missing, and what is ambiguous — so reviewers spend their time on substance rather than scavenger hunts. It is designed to reduce the back-and-forth cycle between authors and review committees.

### When to Use It

- Before submitting a policy document for legal or compliance sign-off, to catch gaps early
- When a project proposal must meet a defined gate criteria and the author wants to self-check before formal review
- When a procurement document requires specific clauses and a first-pass screen is needed before routing
- When a team is producing a new procedure and wants to validate it against the organizational template before publishing
- When a compliance team is managing a high volume of submissions and needs triage assistance to prioritize

### How It Works

The skill begins by identifying the document type, preferring metadata if it is present and falling back to title and content signals if not. It then retrieves the corresponding compliance checklist from the site's Compliance Requirements list or a configured reference source. If neither the document type nor the checklist can be determined, the skill stops and reports that clearly rather than proceeding on assumptions.

For each required element in the checklist, the skill evaluates the document and assigns one of three statuses: Present (clearly included and complete), Absent (missing entirely), or Unclear (partially addressed or lacking sufficient detail). Where the classification is not straightforward, the skill captures a brief excerpt or explanation to make the reasoning transparent.

The output is a structured report showing the document type, an overall summary status (Pass, Flag, or Needs Review), and a table of every required element with its status and supporting notes. Missing elements and ambiguous sections are highlighted. The skill does not rewrite, revise, or update the document — it produces a diagnostic only.

### How to Build It

Place the `SKILL.md` file at:

```
sharepoint/
  process-compliance-first-pass/
    SKILL.md
```

The front matter requires `name` and `description`. The skill depends on a configured Compliance Requirements list on the SharePoint site to retrieve the appropriate checklist for each document type.

### How to Use It

- *"Run a compliance first-pass on this policy draft before I send it for review."*
- *"Does this proposal meet all the required elements for the finance committee?"*
- *"Check this procedure against our standard template and flag anything missing."*
- *"Pre-screen this contract before it goes to legal — identify any gaps."*
- *"Give me a compliance readiness report on this submission."*

### Example Output

**Process Compliance First-Pass Report**

- **Document:** Data Retention Policy — Draft v2
- **Document Type:** Information Governance Policy
- **Overall Status:** 🟡 Flag — 2 required elements absent, 1 unclear

| Element | Status | Notes |
|---------|--------|-------|
| Purpose Statement | ✅ Present | Clearly stated in Section 1 |
| Scope Definition | ✅ Present | Covers all enterprise data types |
| Retention Schedule (by data class) | ❌ Absent | No schedule found; required per IG-POL-04 |
| Roles & Responsibilities | ⚠️ Unclear | "Data Owner" referenced but not defined in this document |
| Legal Hold Procedure | ❌ Absent | Required for all governance policies; not addressed |
| Review Cycle | ✅ Present | Annual review, effective date noted |
| Approval Authority | ✅ Present | Signed by CIO |

**Highlighted Gaps:** The Retention Schedule and Legal Hold Procedure are required elements that must be added before this document is eligible for formal sign-off.

### Key Design Principles

- **Checklist-driven, not interpretive.** The skill evaluates only against the elements defined in the relevant compliance checklist — it does not introduce subjective quality assessments.
- **Transparent reasoning.** Every "Absent" or "Unclear" classification includes a note explaining the basis, so authors know exactly what is needed, not just that something is wrong.
- **Read-only, always.** The skill never modifies or rewrites the document. Its role is diagnostic; remediation is the author's responsibility.

---

# Copilot Cowork vs SharePoint Skills

These two skill types serve different purposes, live in different environments, and operate under different governance models.

**Copilot Cowork skills** are personal, conversational, and user-controlled. A person builds a skill in Cowork to extend Copilot's behavior in their own context — analyzing their email, reviewing their workload, preparing for their meetings. These skills travel with the individual. They can be shared with specific colleagues or small teams, but they are not centrally managed. Cowork is where skills are created, tested, and refined in real working conditions before any broader rollout is considered.

**Copilot in SharePoint skills** are organizational and governed. They are attached to a site or library and are available to everyone who accesses that site. A SharePoint skill might screen every document submitted for compliance review, build onboarding paths for every new hire, or surface content health issues for a content governance team. These skills are designed for consistent, repeatable use across a group — not personalized to any individual. Because they operate at scale, they require more deliberate design and appropriate oversight before deployment.

The practical distinction is one of reach and accountability:

| | Cowork Skills | SharePoint Skills |
|---|---|---|
| **Scope** | Personal / individual | Organizational / site-wide |
| **Governance** | User-managed | IT or content owner managed |
| **Primary use** | Individual productivity | Operational and governance workflows |
| **Sharing** | Optional, person-to-person | Available to all site users |
| **Where to start** | Build and test here first | Deploy after Cowork validation |

---

# How Skills Scale in an Organization

Skills do not need to be built from scratch at the organizational level. The most effective pattern is a three-stage lifecycle that moves from individual experimentation to governed scale.

**Stage 1: Build and test in Copilot Cowork**
A practitioner — a consultant, analyst, operations lead, or anyone who works with Copilot regularly — identifies a repeated task where a custom skill would save time or improve consistency. They build it in Cowork and use it themselves. Because Cowork operates on real personal data (email, calendar, Teams), testing happens in genuine working conditions, not a sandbox. Problems surface quickly.

**Stage 2: Refine and share with individuals or teams**
Once the skill works reliably, the builder shares it with colleagues or a small team. This phase surfaces edge cases, naming issues, and workflow variations that a single user would never encounter alone. The skill is refined based on real feedback. At this stage, the skill is still informal — it's a shared tool, not a managed asset.

**Stage 3: Promote to SharePoint for governed reuse**
When a skill has proven its value across a group, it becomes a candidate for organizational deployment — typically via a SharePoint site where it can serve everyone who accesses that environment. At this stage, responsibility shifts: the skill needs a named owner, documentation, and alignment with any relevant compliance or data governance requirements. It becomes part of the organization's AI operating model rather than an individual's toolkit.

**Leadership implications**

For leaders and operating model designers, this lifecycle has two important implications. First, the Cowork layer is where organizational AI capability actually develops — through experimentation by practitioners close to the work. Creating space for that experimentation, and establishing a lightweight path from personal skill to governed deployment, is more valuable than top-down skill design. Second, skills that reach SharePoint represent institutional knowledge made actionable. When a compliance checklist or an onboarding framework is embedded in a skill, it stops being a document people might not read and becomes something Copilot actively applies. That shift — from passive artifact to active capability — is the real productivity gain at scale.
