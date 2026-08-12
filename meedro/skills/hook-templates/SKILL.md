---
name: hook-templates
description: Build a shareable Hook Templates dashboard as one self-contained HTML page from the Meedro viral library. MUST be used when the user asks for "hook templates", "a hook vault", "a hook library", "viral hooks", "hooks I can share", "a hook dashboard", or any single-page collection of proven hook templates for a niche their audience can copy. Every hook, view count, outlier score, and proof link is real. Nothing is invented.
---


# Meedro Hook Vault Skill

One page: viral hook templates for a niche, each verified against the real video transcript, each with a ready-to-use example in the user's own voice. Output is a single self-contained white-and-purple HTML file the user can host and share as a ManyChat link magnet or bio link.

The first rule above everything else: every hook, view count, outlier score, creator handle, and proof link comes from a real tool result. Nothing is invented, guessed, or padded.

---

## TOOLS (MeedroAI only - never substitute tools from other connectors)

| Tool | Cost | What it returns |
|---|---|---|
| my_info | Free | User's name, niche, connected handles, Brand Voice digest |
| get_brand_voice | Free | Full Brand Voice text. Call when a voice is saved and enabled |
| search_viral_videos | Free | Viral video summaries by keyword. Returns stats and metadata only, no transcript. Single keywords only. Use category, dateFrom, minOutlier |
| viral_hook_library | Free | Top hooks across the full library ranked by views, paginated 20 per page up to 100. Returns hook text, template, format, why it worked, views, and video link pre-filled. Filter by platform. Use as a third source when keyword searches are thin |
| get_video_analysis | Free if the user has already requested this video before. 5 credits first time on a library video | Full stored breakdown including transcript. Use this to verify hooks on library videos. Never call analyze_video on a library video |
| watchlist_videos filter='analyzed' | Free | User's already-analyzed watchlist videos. Full transcripts included inline |
| analyze_video | 5 credits per not-yet-analyzed video | Only called on unanalyzed watchlist videos, after explicit user yes |

---

## STEP 0 - LOAD NICHE AND VOICE

Call my_info first.

**Niche and Brand Voice both present:** confirm once: "I will build this for [niche] in your saved brand voice. Want a different niche?" Wait for confirmation before searching.

**Niche present, no voice:** ask: "Which niche, and how would you describe your voice in one line?"

**Nothing usable:** ask: "Which niche or category? And how would you describe your on-camera voice in one line?"

When a voice is saved and enabled, call get_brand_voice once for the full text.

Also ask: **how many hooks do you want on the final page?** Default is 20. The user can say fewer (for example 10) to reduce credit spend, or up to 30 if they want more. Wait for this answer before searching.

---

## STEP 1 - FIND FREE CANDIDATES FIRST

Pull candidates from three sources, free first. Do not narrate the searches.

**Source 1: Already-analyzed watchlist videos**
Call watchlist_videos with filter='analyzed'. Transcripts are included inline at zero cost. Use these before touching any source that needs a paid read.

**Source 2: Niche keyword search**
Call search_viral_videos at least twice, each with a different single keyword for the niche. Use dateFrom set to 6 months before today and minOutlier around 3. Prefer the last 6 months. If 6 months does not yield enough after quality checks, silently widen to 12 months. Only mention age if anything older than 12 months appears on the final page. Returns summaries only, no transcript. Each candidate from this source needs get_video_analysis to get the transcript.

**Source 3: Viral hook library (use when Sources 1 and 2 are thin)**
Call viral_hook_library if the first two sources do not yield enough candidates after quality checks, or to supplement with broader top-performing hooks. Returns up to 100 hooks paginated at 20 per page, pre-filled with hook text, template, and video link. Filter by platform if relevant. Hook autocorrect still applies: verify the first spoken transcript line via get_video_analysis before using any hook from this source.

From all three sources, note which candidates already have a free transcript and which need a paid read.

---

## STEP 2 - TELL THE USER THE CREDIT SITUATION BEFORE SPENDING ANYTHING

After collecting free candidates, say in plain chat:

Free sources (zero credits):
- Already-analyzed watchlist videos: [N] candidates with transcripts included
- Library videos the user has already requested before (get_video_analysis already called): [N] candidates

Paid reads needed to reach the target (5 credits each, first time only):
- Library videos not yet requested: [N] candidates needed, [N x 5] credits total
- Accounting for roughly 30 to 40 percent discard rate on quality checks, you may need more candidates than the target number

Your current credit balance: [balance]
Estimated credits to reach your target of [N] hooks: [total]

Then give three options:
1. Say yes to proceed with the paid reads needed to reach the target
2. Give a smaller target number that fits within the free candidates
3. Say "free only" to build with zero credits using only already-analyzed videos

Wait for the answer. Never spend any credits before an explicit yes.

---

## STEP 3 - AUDIT EVERY CANDIDATE (quality floor, non-negotiable)

For each candidate where you have a transcript, run all five checks:

**1. Hook autocorrect (silent)**
Use the stored hook field if it reads as a real spoken opening line. If it looks like a caption, a CTA, a hashtag line, or does not read as something said out loud at the start of a video, silently verify against the transcript and replace it with the first spoken line. Never mention this on the page.

**2. Template validity (all four must pass)**
A: It is a spoken verbal opening, not a silent visual or title card.
B: It is writable as a fill-in-the-blank with [brackets], not a production instruction.
C: The template works in more than one niche.
D: The template is under 20 words. Bracket variables count as one word each.

**3. Real URL and numeric outlier**
Must have a real Instagram or TikTok link AND a numeric outlier score. If the URL is missing or the outlier is empty, zero, or "N/A", discard.

**4. No duplicate patterns**
If two candidates share nearly the same hook structure, keep only the higher-view one. All final hooks must be structurally distinct.

**5. Discard cleanly**
If a candidate fails any check, discard it and move to the next one. Never pad the count with a failed video.

Rank survivors by raw views. Take the top [target number]. If still short after all sources, tell the user the real count and offer to try another keyword.

---

## STEP 4 - WRITE EACH CARD

For every confirmed hook, write:

**Template:** the first-spoken-line hook rewritten as fill-in-the-blank with [brackets]. Keep original punctuation and grammar. Under 20 words. No em dashes (use a comma or colon instead).

**Example:** the template filled in for this user, in their niche and brand voice. Follow the template structure exactly. Zero brackets left over. Under 25 words. Matches the user's pacing and energy. Use only round, believable numbers. Never fabricate precise stats about the user's real results. If no brand voice is available, write in a clean confident neutral voice for the niche.

**How it was used:** 2 to 3 plain sentences on what actually happened in the video, grounded in the transcript. No filler phrases. No bullets. No em dashes.

**Tags:** 1 to 2 tags from this fixed list only: urgency, curiosity, reveal, story, tool, challenge. Base tags on the hook text, not the topic.

---

## STEP 5 - SELF-CHECK BEFORE BUILDING

Confirm all of these before writing any HTML:
- All hooks have a real proof URL, a real numeric outlier, a first-spoken-line hook, and passed all four validity checks
- All examples are filled in with zero leftover brackets
- Zero em dashes anywhere
- View counts are formatted (3.7M, 941K, not raw numbers)
- No duplicate hook structures
- Tags assigned to all hooks
- All proof URLs are unique and real

---

## STEP 6 - BUILD THE HTML

One self-contained file. No external JS or CSS. One Google Fonts import (Inter 400 to 900) allowed.

**Design tokens (in :root):**
--purple:#6D28D9, --purple-light:#7C3AED, --purple-pale:#F5F3FF, --purple-border:#DDD6FE, --white:#FFFFFF, --gray-50:#F9F9F9, --gray-100:#F2F2F2, --gray-200:#E5E5E5, --gray-400:#AAAAAA, --gray-600:#666666, --gray-800:#1A1A1A, --radius:12px.

**Header (sticky):** Logo: 32px purple rounded square with bold white "M", no icon. Wordmark: "Meedro" in #1A1A1A. Center: search input with magnifier icon, placeholder "Search hooks, creators, topics...".

**Hero:** Purple gradient (#6D28D9 to #7C3AED). Eyebrow pill "[Niche] Hook Library". H1 "Top [N] Viral Hooks That Actually Work" (clamp 28 to 44px, weight 900, white). Subtitle. Three stats: "[N] Hook Templates", "[combined views]+ Combined Views", "100% Transcript Verified".

**Filter bar (sticky, white):** All Hooks, Urgency, Curiosity, Reveal, Story, Tool Tips, Challenge. Active filter: purple fill white text. Inactive: white fill gray border. Horizontally scrollable on mobile.

**Grid:** max-width 1280px, auto-fill columns min 340px, gap 20px. Live "[N] hook templates" count above.

**Each card:**
- White background, 1.5px --gray-200 border, --radius corners. Hover: lifts 3px, stronger shadow, --purple-border
- Top row: rank badge in --purple-pale left, views pill in --purple-pale with purple border right
- "HOOK TEMPLATE" label (purple uppercase 10px) then the template in 15px bold
- "HOW IT WAS USED" label (gray uppercase 10px) then the explanation with a left purple-border rule
- Example box: --purple-pale background, 1px --purple-border, --radius 8px, padding 11px 12px. Left: small purple uppercase label with lightbulb icon "Ready to use, your voice". Right: small "Copy" button. Below: the example hook in 13.5px bold dark
- Meta row: creator handle as clickable purple bold link (opens profile in new tab), dot separator, green outlier badge
- Footer: "Copy Hook" button (--purple-pale, copies the blank template) plus external-link icon button opening the real video URL in a new tab

**JavaScript:** Store all hook objects in a const hooks array. Each object has: rank, hook, example, howUsed, views, rawViews, creator, outlier, url, profileUrl, tags. Derive profileUrl from the real handle and platform of the video URL only. Never guess it.

**Copy functions:**
- copyHook(btn, idx): copies the blank template using navigator.clipboard with an execCommand textarea fallback for older browsers. Shows a checkmark for 2 seconds.
- copyExample(btn, idx): copies the ready-to-use example line. Same clipboard logic. Same checkmark feedback.

**Search and filter:**
- Search bar filters cards live by hook text, creator handle, and topic
- Tag filter buttons show only cards matching that tag
- Both work together simultaneously
- setFilter(tag, el) and filterCards() functions handle this

**Page footer:** White, top border, centered "Powered by Meedro viral library".

---

## STEP 7 - FINAL SCAN AND DELIVER

Before delivering: confirm zero U+2014 characters anywhere, all copy buttons are wired, the file is fully self-contained, and all proof URLs appear exactly as the tool returned them.

Present the HTML file. Then write exactly three short lines, no headers or bullets:
1. How many hooks and which niche.
2. How to share it (host on any static host, use the URL as a ManyChat button link).
3. What is next (re-run for another niche, or add more hooks in this one).

Write nothing after those three lines.

---

## ERROR HANDLING

**Under 20 usable videos after two searches:** run a third keyword search. Still under: tell the user the real count and offer another keyword. Build with what passed if they decline.

**Video with no transcript or no URL:** skip it, never reconstruct.

**User changes niche after searching:** start over from Step 1.

**6-month window is thin:** widen to 12 months silently. Mention age only if anything older than 12 months appears on the final page.
