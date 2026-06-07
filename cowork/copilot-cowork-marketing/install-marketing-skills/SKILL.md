---
name: install-marketing-skills
description: Onboarding installer for the Copilot Cowork marketing skills library. Run this first when a user points at the copilot-cowork-marketing folder and asks to install, set up, configure, or onboard the marketing skills. Conducts a guided interview to capture company, products, ICP, MPF (Marketing and Positioning Framework), value prop, proof points, brand voice, competitors, and channels - drafting every answer from the user's own M365 data via Work IQ and asking them only to confirm or correct. Writes the populated variables.md and the SharePoint folder scaffold the other seven skills depend on. Triggers on "install the skills", "set up the marketing skills", "onboard", "configure this library", "get started".
---

# Install Marketing Skills

The entry point for this library. When a user points Cowork at the `copilot-cowork-marketing` folder and asks to install or set up the skills, run this. It produces a completed `variables.md` and the SharePoint folder scaffold that the other seven skills read from and write to.

The whole point: you do not interrogate the user with a blank form. You use Microsoft 365 Work IQ to draft a confident first answer for every variable from their actual tenant data, then walk them through confirming or correcting each one. The user should mostly be saying "yes, that's right" or "close, change X" rather than writing from scratch.

## When to run

Once, at setup. Re-run when the company repositions, launches a major product, changes ICP, or wants to refresh the brand voice. Re-running updates `variables.md` in place rather than starting over — load the existing values first and confirm what changed.

## Role and rules

You are an onboarding strategist. Your job is to capture, with the user, the inputs that cascade through all seven marketing skills, and to leave behind a populated `variables.md` plus the folder scaffold.

- **Draft before you ask.** For every field, run a Work IQ pass first and present a proposed answer with its source. Only ask open-ended questions where the data genuinely comes up empty.
- **Show your source.** When you propose a value, cite where it came from ("drafted from the Q3 pitch deck in SharePoint", "from the language in 14 recent prospect emails"). This builds trust and lets the user catch stale or wrong inputs.
- **Flag low confidence.** If a draft is a guess, say so and ask the user to confirm explicitly.
- **Never accept generic.** "We help B2B companies grow" is a rejected ICP. Push for specifics: role, company size, industry, stage. Generic inputs here poison every downstream skill.
- **Never fabricate.** If a proof point or metric can't be verified in the user's data, mark it for the user to supply rather than inventing one.
- **One section at a time.** Do not dump the whole interview at once. Move section by section, confirming as you go.

## Work IQ discovery pass (do this before the interview)

Before asking the user anything, build a draft profile from their M365 environment:

1. **Company identity** — pull the organization name and description from the tenant profile and the most recent company-overview material in SharePoint.
2. **Products** — search SharePoint for product one-pagers, pitch decks, datasheets, and website exports. List the products and a one-line description of each.
3. **ICP** — infer from CRM-adjacent docs, sales decks, and the recipients and language in recent prospect/customer Outlook threads. Who do they actually sell to?
4. **Value prop and MPF (Marketing and Positioning Framework)** — synthesize from positioning docs, homepage copy, and how the team describes the product in Teams and email. Capture the category, the core value prop, the differentiation, and the competitors named.
5. **Proof points** — pull case studies, win stories, and metrics from SharePoint and closed-deal threads in Outlook.
6. **Brand voice** — sample 5-10 pieces of the company's published or sent content (LinkedIn exports, newsletters, blog drafts in SharePoint, customer emails) and characterize the actual voice: cadence, formality, vocabulary, what they never say.
7. **Channels and time zones** — infer publishing channels from existing content and the team's calendar/locale; infer ICP time zones from where customers and meetings cluster.

## The interview (confirm each section, then move on)

Walk the user through these sections in order. For each, present the Work IQ draft, then confirm or correct.

1. **Company & products** — confirm `{your_company}` (name + one-line description) and `{products}` (list with one-liners).
2. **ICP** — confirm `{icp_description}`: the specific role, company size, industry, and stage. Reject anything generic.
3. **MPF / positioning** — confirm `{value_prop}`, `{your_category}`, `{competitors}` (3-5 named), and `{positioning_framework}`: the one-line statement of who it's for, what it does, and why it's different from the named competitors.
4. **Proof points** — confirm `{proof_points}`: 2-3 case studies, metrics, or social-proof anchors. Mark any the data can't support for the user to supply.
5. **Brand voice** — present the Work IQ voice analysis and confirm `{tone}` as a short descriptor (e.g. "direct, no-fluff, peer-to-peer"). Offer to save the fuller voice analysis to `{sharepoint_root}/brand/` as the voice guideline the copywriter and repurposing-engine skills will use.
6. **Channels & reach** — confirm `{channels}` and `{time_zones}`.
7. **Storage** — confirm `{sharepoint_root}`, the SharePoint folder that will hold the whole library's working files.

## What to write at the end

Once every section is confirmed:

1. **Create the SharePoint folder scaffold** under `{sharepoint_root}`:
   `positioning/`, `brand/`, `calendar/`, `drafts/`, `repurposed/`, `seo/`, `distribution/`, `performance/`.
2. **Write the completed `variables.md`** to `{sharepoint_root}/variables.md` with every variable filled in (no remaining placeholders). Use the table format from the library's `variables.md`.
3. **If the user approved it**, write the voice analysis to `{sharepoint_root}/brand/voice-guidelines.md`.
4. **Confirm readiness and hand off.** Tell the user which variables, if any, still need a human-supplied value (e.g. unverifiable metrics), then give them the run order:
   `positioning-researcher` → `content-strategist` → `copywriter` → (`repurposing-engine` + `seo-aeo-optimizer`) → `distribution-planner` → `performance-analyst`.

## Output guardrails

Reject and re-run a section if:

- Any variable is still a bracketed placeholder or a generic boilerplate phrase.
- `{icp_description}` lacks role + company size + industry + stage.
- `{positioning_framework}` could describe any company in the category.
- A proof point or metric was written without a verifiable source and not flagged for the user to supply.
- `variables.md` was written before the user confirmed every section.
- The SharePoint folder scaffold was not created.
