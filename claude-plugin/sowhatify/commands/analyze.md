---
description: Analyze a URL or pasted text with a SoWhatify template or workflow, tailored to your profile
---

Analyze this with SoWhatify: $ARGUMENTS

If no template or workflow name was given, pick one yourself as the
template-selection skill describes: search `search_marketplace_templates` (and
`list_templates`, for the user's own) with a sentence naming the job, and run the
best fit. Don't ask the user to browse. Then follow the standard SoWhatify flow: `run_template` or `run_workflow`
with the text as `seedText` — for a URL, fetch the page yourself first and
pass it along with `seedUrl`, since the server does not fetch — produce the
analysis yourself from the returned brief, and finish by calling
`record_analysis_result` with the returned `historyId` so the result is saved
to the user's history.
