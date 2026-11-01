---
description: Analyze a URL or pasted text with a SoWhatify template or workflow, tailored to your profile
---

Analyze this with SoWhatify: $ARGUMENTS

If no template or workflow name was given, ask the user which one to use, or call
`search_marketplace_templates` / `list_templates` to suggest one based on the
content. Then follow the standard SoWhatify flow: `run_template` or `run_workflow`
with the text as `seedText` — for a URL, fetch the page yourself first and
pass it along with `seedUrl`, since the server does not fetch — produce the
analysis yourself from the returned brief, and finish by calling
`record_analysis_result` with the returned `historyId` so the result is saved
to the user's history.
