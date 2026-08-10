---
name: script-generator
description: Write a ready-to-film short-form script from your topic or a video you just analyzed. Free.
---


The creator wants a ready-to-film short-form script. Claude writes the script itself - no generate tool, no credits. Brief: "$ARGUMENTS".

SOURCE - first work out where this script starts from:
- FROM A VIDEO: if the user just analyzed a video (/meedro:analyze-video), picked one from /meedro:search-viral-videos or /meedro:videos-watchlist with its breakdown shown, or pasted a transcript - and they want a script "based on that" - USE IT (free, no tool call): take the hook PATTERN from the transcript's FIRST spoken line, the beat-by-beat structure, and the pacing, then adapt them to the user's own topic/niche. Do NOT re-ask what the video already answers - only fill the gaps below (usually just their topic/niche, duration, and CTA). If they want the SAME script rewritten with a new angle, hand off to /meedro:recreate-with-a-twist instead.
- FROM SCRATCH: no source video? Gather the brief below.

SETUP (ask only for what the source did not already give you)
- TOPIC: get it from "$ARGUMENTS" or ask. If they are vague, help brainstorm/refine it yourself (no tool) until it is concrete. (Browsing script writing styles and saving favorites needs an active Meedro plan; if a scripting tool reports no access, tell the user and keep writing the script yourself - that is always free.)
- DURATION: 30, 60, or 120 seconds (default 60).
- HOOK - YOU recommend or invent a hook that fits the topic - never stall waiting for a pick.
- WRITING STYLE - YOU pick or invent a style that fits the topic and the user's niche.
- CTA - have them choose one of the fixed six: none / comment / share / save / follow / show_all. If they do not care, recommend one that fits the topic.
- Optional: any extra instruction (angle, tone, a point to make).

WRITE IT (you, the assistant - never call a generate tool, this is free)
- Apply the chosen/recommended hook + writing style + CTA to the topic, paced for the chosen duration.
- The hook is the opening line - make it stop the scroll. Pace the body so there is no dead air for the given duration.

OUTPUT - render a shoot sheet. Put the header card in a ``` code block:

```
┌──────────────────────────────────────────────┐
│ SCRIPT - <topic> · <duration>s             │
└──────────────────────────────────────────────┘
```
Then:
HOOK - on its own line, bold (it is 80% of the performance).
BODY - the beats with rough timestamps, short and punchy (no dead air).
CTA - the closing line, framed per the chosen CTA type.
Offer to save the script with the save_script tool.
