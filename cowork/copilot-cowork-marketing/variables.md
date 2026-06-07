# Shared Variables

The easiest way to fill this in is to run the **`install-marketing-skills`** skill. Point Cowork at this folder and ask it to install the skills — it drafts every value below from your M365 data via Work IQ, walks you through confirming each one, and writes the completed file to `{sharepoint_root}/variables.md` for you.

To fill it in by hand instead: replace every bracketed placeholder with your real values and save this file to your SharePoint marketing folder (e.g. `/Marketing/Cowork/variables.md`). Every skill in this library reads its variables from here, so you only define them in one place. When a skill needs a value, it searches SharePoint for this file and substitutes the value into its prompt.

Do not leave any value as generic boilerplate.

| Variable | Value |
| --- | --- |
| `{your_company}` | _Company name + one-line description_ |
| `{products}` | _Your products, each with a one-line description_ |
| `{icp_description}` | _Who you sell to: role, company size, industry, stage_ |
| `{value_prop}` | _The specific outcome you deliver, in 1-2 sentences_ |
| `{positioning_framework}` | _MPF: one-line statement of who it's for, what it does, and why it's different from the named competitors_ |
| `{your_category}` | _Your product category, e.g. "sales engagement"_ |
| `{competitors}` | _3-5 direct competitors by name_ |
| `{proof_points}` | _2-3 case studies, metrics, or social-proof anchors_ |
| `{tone}` | _Voice descriptor, e.g. "direct, no-fluff, peer-to-peer"_ |
| `{channels}` | _Where you publish, e.g. "LinkedIn, X, blog, newsletter, YouTube"_ |
| `{time_zones}` | _Primary time zones of your ICP, e.g. "US Eastern, US Pacific"_ |
| `{sharepoint_root}` | _SharePoint folder holding these assets, e.g. "/Marketing/Cowork"_ |

## SharePoint layout the skills expect

These skills read upstream inputs and write outputs to predictable locations under `{sharepoint_root}`. Create these folders so the chain can hand off automatically:

- `{sharepoint_root}/variables.md` — this file
- `{sharepoint_root}/positioning/` — positioning dossier (output of positioning-researcher)
- `{sharepoint_root}/brand/` — brand and voice guidelines (input to copywriter and repurposing-engine)
- `{sharepoint_root}/calendar/` — editorial calendar (output of content-strategist)
- `{sharepoint_root}/drafts/` — content drafts (output of copywriter)
- `{sharepoint_root}/repurposed/` — repurposed asset packages (output of repurposing-engine)
- `{sharepoint_root}/seo/` — SEO/AEO recommendations (output of seo-aeo-optimizer)
- `{sharepoint_root}/distribution/` — distribution plans (output of distribution-planner)
- `{sharepoint_root}/performance/` — weekly performance reports (output of performance-analyst)
