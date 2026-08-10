---
name: analyze-video
description: Use whenever the user asks to analyze, break down, or explain a video or reel - even without the slash command, and even if they only gave a link or named a creator. Full breakdown: hook, structure, full transcript & copy-ready templates. 5 credits per video.
---


The creator pasted one or more videos and wants to know exactly why they work. Input: "$ARGUMENTS".

SETUP
- Collect the video URL(s); all the same platform (Instagram OR TikTok). If the user named a creator or a
  watchlist instead of giving URLs: do NOT switch to analyze-profile and do NOT ask the user for links -
  fetch the URLs yourself, FREE, with watchlist_videos (a whole watchlist; sort 'outlier' ranks by viral),
  then run analyze_video on those URLs. Every reel it lists carries its URL. /meedro:analyze-profile is ONLY
  for scanning/ranking a profile, never a substitute for analyzing specific videos.
- IF the video came from a /meedro:search-viral-videos result WITH its breakdown shown, it is ALREADY
  analyzed - do NOT call analyze_video; just present that breakdown (free). analyze_video is only for a NEW
  link not already in the search results.
- A reel that is not analyzed yet (from search or the watchlist) goes through THIS skill: it needs a full
  analyze_video run on its URL, after which it can be saved with save_video. Never re-analyze a reel that is
  already analyzed - its breakdown is already shown, free.
- COST, NO CONFIRMATION: analyze_video costs a flat 5 credits PER video (expired or fresh, always 5; a
  reel the user already analyzed anywhere is free). Do NOT ask the user to confirm the cost first - them
  asking to analyze IS the go-ahead, so run analyze_video straight away with no "this costs 5 credits,
  proceed?" prompt. AFTER it finishes, tell them the credits used in one short line ("5 credits used", or
  "3 videos, 15 credits used"); if a video came back already-analyzed it was free, so say "already analyzed,
  no credits used" instead - never claim credits were spent when they were not. Run check_credits if unsure
  of the balance.
- Call analyze_video and let it run - it WAITS and streams results itself (no sleep/wait command, no pausing
  to ask). If it hands off with "Still working", call get_analysis_result ONCE (it waits too) and repeat only
  if it hands off again, until you see "All done.". Results stream a few at a time.

SEE THE COVER FRAME TOO (free, no extra credits)
- After analyze_video finishes, call get_video_thumbnail on the SAME url. It is free, needs no analysis, and
  returns the real cover image so you can SEE the video instead of guessing from text. Do this for a single
  video always, and for a batch on request (one image per video is a lot of reply).
- Why it matters: the analysis is TEXT. It cannot tell you what the frame looks like or what words are burned
  onto it. Only the image can, and the Three Hook Types below need it.

OUTPUT
analyze_video returns a complete, ready-to-show Video Insight for each video - a Performance table, then
Topic, Caption, Hook, Why It Worked, Core Concept, Story Beats, Script & Structure, Visual Breakdown and the
FULL TRANSCRIPT - wrapped in copy-verbatim markers. Present it EXACTLY as returned, directly under the video
card, in the SAME reply. Do NOT summarise, paraphrase, re-order, add emojis or long dashes, or build your own
virality snapshot / ASCII chart / score bars - show only what the tool produced. For a batch, present EVERY
video's full insight in order, separated by a divider - never keep only the "top" ones and never collapse the
batch into a summary. Never show internal ids.

THREE HOOK TYPES - add this section after the tool's insight, before the transcript offer
Every video hooks the viewer in three separate places, and they come from two different sources. Add a
"Three Hook Types" section with all three, in this order, ALWAYS all three even when one is empty:
1. VERBAL HOOK (what is said out loud) - from the transcript / the insight's Hook section. Quote it exactly.
2. VISUAL HOOK (what is SEEN in the opening frame) - from the cover image you fetched: the subject, framing,
   setting, colours, what makes the eye stop.
3. TEXT-OVERLAY HOOK (words burned ONTO the frame) - read verbatim off the cover image, in quotes.
For each one give: the hook itself, a one-line "Why it works", and a reusable Template with the variable parts
in [square brackets] - the sentence's own wording with blanks, never a description of it.
IF A HOOK TYPE DOES NOT EXIST OR YOU CANNOT SEE IT, WRITE "-" AND SAY WHY IN A FEW WORDS (e.g. "- (no text on
the cover frame)" or "- (thumbnail unavailable)"). NEVER invent a visual or text-overlay hook from the
transcript, the caption or the topic - if you did not see the frame, you do not know what is on it, and a
confident guess reads to the user as fact. A "-" is the correct, honest answer.
Close with a short "How they work together" line - how the three combine in the first seconds.
MANDATORY - ALWAYS show the full transcript: every video's insight MUST include its complete "Full Transcript"
section, reproduced word for word, no matter how long it runs or how many videos there are. A breakdown shown
without its transcript is INCOMPLETE - never drop, shorten, excerpt or truncate the transcript, and never point
the user to a card or elsewhere for it instead of showing it in the reply. If you feel the reply is getting
long, that is expected: still show every transcript in full rather than condensing.
Offer next: /meedro:script-generator to draft an adaptation, or the save_video tool to keep it.
