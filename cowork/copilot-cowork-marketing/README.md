# Marketing Skills Library for Copilot Cowork (M365)

A chained set of seven marketing skills for Copilot Cowork, grounded in your Microsoft 365 environment. Together they take you from positioning research through content production, repurposing, SEO/AEO, distribution, and performance analysis as a single closed loop.

Each skill is a folder containing a `SKILL.md` (name + description frontmatter, instructions, the user-prompt template it expects, M365 data grounding, and guardrails). Drop the whole `copilot-cowork-marketing` folder into Cowork to ingest the installer plus all seven working skills.

## Quick start

Point Cowork at this folder and say **"install the marketing skills."** That runs the **`install-marketing-skills`** skill, which interviews you to capture your company, products, ICP, MPF (market positioning framework), proof points, brand voice, competitors, and channels — drafting every answer from your own M365 data via Work IQ so you mostly confirm rather than type. It then writes the completed `variables.md` and the SharePoint folder scaffold the other seven skills depend on. Run it first.

## What's inside

- **`install-marketing-skills`** — the onboarding installer. Run first. Interviews you (Work IQ-augmented) and writes `variables.md` + the SharePoint scaffold.
- **`positioning-researcher`** — analyzes your ICP, competitive landscape, and market gaps so your messaging hits a real nerve instead of sounding like everyone else.
- **`content-strategist`** — pulls search demand, audience pain points, and competitor content gaps to build an editorial calendar grounded in data.
- **`copywriter`** — drafts LinkedIn posts, blog intros, newsletters, email sequences, and landing page copy in your voice.
- **`repurposing-engine`** — takes one long-form piece and turns it into 8-10 assets across LinkedIn, X, email, blog, and short-form video scripts.
- **`seo-aeo-optimizer`** — handles keyword mapping, metadata, heading structure, and the citation signals that get your content surfaced by AI search engines.
- **`distribution-planner`** — maps every piece to the right channel, format, and posting window so nothing sits in a doc collecting dust.
- **`performance-analyst`** — tracks what's driving pipeline, flags what to cut, and recommends where to double down.

## How the skills chain

- `positioning-researcher` output feeds `content-strategist` and `copywriter`.
- `content-strategist`'s editorial calendar drives `copywriter`'s writing queue.
- `copywriter` output feeds `repurposing-engine` and `seo-aeo-optimizer`.
- `distribution-planner` takes the full content package and schedules distribution.
- `performance-analyst` closes the loop by feeding performance data back into `content-strategist`.

## How M365 grounding works

Unlike a stand-alone prompt library, these skills are wired to read from and write to your Microsoft 365 environment:

- **SharePoint / OneDrive** — the source of truth for your positioning dossier, brand and voice guidelines, editorial calendar, content drafts, and performance reports. Each skill reads its upstream inputs from SharePoint and writes its outputs back so the next skill in the chain can pick them up.
- **Outlook** — mined for voice-of-customer signals (prospect and customer email language), and used by the distribution planner to schedule and the performance analyst to pull reply data.
- **Teams chat** — mined for internal context, customer-call notes, and recurring questions the sales and CS teams hear.

Store your shared variables (see `variables.md`) once in a known SharePoint location. Every skill reads them from there so you define them a single time.

## Variables to define once

Define these in `variables.md` and save it to a known SharePoint location (e.g. `/Marketing/Cowork/variables.md`). They cascade through every skill.

- `{your_company}` — company name + one-line description
- `{icp_description}` — who you sell to (role, company size, industry, stage)
- `{value_prop}` — the specific outcome you deliver, in 1-2 sentences
- `{proof_points}` — 2-3 case studies, metrics, or social-proof anchors
- `{tone}` — voice descriptor (e.g. "direct, no-fluff, peer-to-peer")
- `{your_category}` — your product category
- `{channels}` — where you publish
- `{competitors}` — 3-5 direct competitors by name
- `{sharepoint_root}` — the SharePoint folder that holds these assets (e.g. `/Marketing/Cowork`)
- `{time_zones}` — primary time zones of your ICP

## Setup checklist

1. Ingest the `copilot-cowork-marketing` folder into Cowork.
2. Run `install-marketing-skills` ("install the marketing skills"). It interviews you with Work IQ-drafted answers and writes a completed `variables.md` + the SharePoint scaffold. This replaces filling in `variables.md` by hand.
3. Run `positioning-researcher` on your company + 3 competitors. Confirm the positioning gaps make sense. It writes the dossier to SharePoint.
4. Run `content-strategist` using that dossier. Review the editorial calendar for 2 weeks.
5. Run `copywriter` on your first 5 briefs. Edit for voice, then publish.
6. Activate `repurposing-engine`, `seo-aeo-optimizer`, `distribution-planner`, and `performance-analyst` once you have a rhythm going.

## The chain in action

**Week 1 — Foundation:** Run `positioning-researcher`, then `content-strategist`, then `copywriter` on the first 5 briefs.

**Week 2 — Scale:** Run `repurposing-engine` on everything from Week 1, `seo-aeo-optimizer` on all blog content before it goes live, and `distribution-planner` to map the schedule.

**Week 3 — Optimize:** Run `performance-analyst` on your first two weeks of data and feed its output back into `content-strategist`.

**Week 4+ — Compound:** The loop tightens each cycle. `performance-analyst` feeds `content-strategist`, which feeds `copywriter`, which `repurposing-engine` multiplies and `distribution-planner` ships.

## Where teams hit the wall

- **No positioning clarity.** If you feed `positioning-researcher` generic inputs ("we help B2B companies grow"), every downstream skill produces generic output. Spend the time on `variables.md`.
- **Content without distribution is invisible.** `distribution-planner` maps the plan, but execution still requires showing up — posting, commenting, engaging.
