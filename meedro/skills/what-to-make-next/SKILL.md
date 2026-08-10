---
name: what-to-make-next
description: Get ranked ideas for your next video - from your watchlist + what is going viral in your niche. Free.
---


The creator wants to know WHAT TO MAKE NEXT. Build ranked, evidence-backed video ideas from THEIR corner of the platform - then offer to script the winner. All of this is free (read-only tools + you write the ideas). Input: "$ARGUMENTS".

SETUP
- Need their NICHE/topic (from "$ARGUMENTS", the conversation, or ask). If they track creators, that is a strong niche signal too.

GATHER (read-only, no credits - run what applies)
- watchlist_videos with sort 'outlier' (their tracked creators' over-performers right now). Skip silently if the watchlist is empty.
- search_viral_videos on their niche keyword(s) (the viral library + their watchlist's analyzed videos).

SYNTHESIZE (you, the assistant - never invent numbers)
- Cluster what you gathered into repeating winners: topics, hook patterns, formats.
- Build 3-5 concrete VIDEO IDEAS for THEIR niche. Each idea must trace back to at least one real gathered video as evidence.

OUTPUT - render a dashboard. Put the card in a ``` code block:

```
┌──────────────────────────────────────────────┐
│ WHAT TO MAKE NEXT - <niche>                │
│ ranked ideas · backed by real winners         │
└──────────────────────────────────────────────┘
```
Then the ranked ideas, best first:
  <the idea, one line>
     WHY NOW - the evidence video(s): @creator, <views> views, <outlier> (real numbers only)
     HOOK - a ready opening line you drafted for it
     FORMAT - one line: the beat structure to follow
  … (same shape)

End with: which one should I script? -> /meedro:script-generator (its FROM A VIDEO mode when the idea is based on one evidence video). Deep-dive the evidence with /meedro:analyze-video. If both gathers came back empty, say so and suggest tracking creators (add_to_watchlist) or a different keyword.
