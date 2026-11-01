---
name: template-selection
description: Use when a SoWhatify analysis is wanted but no template was named — "analyze this with SoWhatify", "what does this mean for me", "find the right SoWhatify analysis for this". Picks a template from the marketplace by task fit rather than asking the user to browse it. Not needed when the user already named a template or workflow.
---

# Choosing a SoWhatify template

The user should not have to know what is in the marketplace. Infer the job, search
for it, pick one, run it. Asking "which template would you like?" is the failure
mode this skill exists to prevent.

## How to choose

1. **Name the job in one sentence**, from the content and the conversation. Not
   "analyze this article" — something like "decide whether a competitor's launch
   threatens our product" or "work out what this regulation obliges us to change".
2. **Search with that sentence.** `search_marketplace_templates` scores by how many
   query terms a record matches and returns partial matches ranked, so a full
   sentence works better than one keyword. Add `list_templates` if the user is
   likely to have their own.
3. **Judge from the summaries, not the order.** Each hit carries
   `outputSections` — the actual section names the template produces. That is the
   strongest fit signal available without a second call: a template emitting
   *Threat / Opportunity / Recommended response* is a competitive tool whatever its
   title says. `get_template` only when two candidates are genuinely close.
4. **Prefer specific over generic.** A template built for the exact job beats a
   general "summarize and give implications" one, even with fewer installs.
   `installCount` is a tiebreak between close fits, never a reason to pick.
5. **Run it.** Don't narrate the search. "Running Competitive Impact" is enough.

## When to offer a choice

Only when two candidates would produce **meaningfully different analyses** and you
cannot tell which the user wants — a regulatory template and a competitive one for
an article that is both. Then name the two in one line, say what each would
answer, and pick a default so the user can just say "yes".

Never present a list of five. Never ask the user to go and browse.

## When nothing fits

If the best score is weak and the summaries look unrelated, say so and analyze the
content directly without a template. A badly-fitting template is worse than none:
it produces confidently-shaped output answering a question nobody asked.

Don't invent a template id, and don't run a template you have not seen in a search
result or a `get_template` call.

## Worth knowing

- `profileReadAccess: ['none']` means the template ignores the profile entirely.
  Fine for a general explainer, wrong for "what does this mean for *me*".
- The user's own private templates are usually the better answer when one matches —
  they built it for a reason.
- Perspectives are separate: `search_marketplace_perspectives` finds a thinking
  style ("SaaS founder") to layer on top of whichever template you picked.
