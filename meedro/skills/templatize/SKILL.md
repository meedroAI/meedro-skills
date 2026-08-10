---
name: templatize
description: Turn a script or a hook into a reusable fill-in-the-blank template. Free.
---


The user wants you to TEMPLATIZE something - turn a SCRIPT or a single HOOK into a reusable fill-in-the-blank template. You do this YOURSELF - do NOT call any Meedro tool to build it. Input: "$ARGUMENTS".

SETUP
- Work out WHAT they are templatizing from "$ARGUMENTS" (or the most recently analyzed video's transcript, or a hook from earlier in the chat). If you have nothing, ask for the script or hook.

FOR A SCRIPT (you, the assistant - never send a request to Meedro for this)
- Convert it line-for-line into a reusable template: replace the specific topic, names, numbers and examples with clear [PLACEHOLDERS] (e.g. [HOOK], [PROBLEM], [PROOF], [PAYOFF], [CTA]).
- Keep the structure, pacing, and hook pattern intact so any topic can be dropped in.
- OUTPUT - render a template sheet. Put the header card in a ``` code block:

```
┌──────────────────────────────────────────────┐
│ SCRIPT TEMPLATE                            │
└──────────────────────────────────────────────┘
```
Then, in order:
- TEMPLATE: the script as clean, copyable lines with [PLACEHOLDERS].
- ️ PLACEHOLDERS: a short legend - one line per placeholder explaining what to drop in.
- ▶️ EXAMPLE: the same template filled in once for a sample topic, so the user sees it in action.
Offer to draft a fresh script from it with /meedro:script-generator.

FOR A HOOK
- Strip the specifics into placeholders while keeping the pattern, rhythm and emotional trigger that stop the scroll (e.g. "I paid $500 for this fitness mistake" -> "I paid [PRICE] for this [TOPIC] mistake").
- OUTPUT: the templatized hook bold on its own line, a one-line legend of its placeholders, and the same hook filled in once for the user's niche.
