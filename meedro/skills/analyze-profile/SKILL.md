---
name: analyze-profile
description: Rank a creator's best recent videos and spot their winning formula. Free.
---


The creator wants ONE creator's best recent videos as a leaderboard. Input: "$ARGUMENTS".

SETUP
- FIRST check the intent: this skill is ONLY for a creator's profile. If the user asked to
  analyze specific videos/reels, that is /meedro:analyze-video instead - the video URLs come FREE from
  watchlist_videos (sort 'outlier'); never call a tool here just to find URLs.
- Need the @username AND the platform (instagram or tiktok). If the platform wasn't stated, ASK - never assume.
- DEFAULT to get_creator_videos: it returns the creator's already-stored videos instantly and for free, no
  analysis needed. It tells you when that creator was last checked - if the stored data is behind, OFFER to
  run update_watchlist for that one creator and let the user decide; do NOT re-analyze automatically. For an
  Instagram creator on the Pro plan or higher that update also pulls their Trial Reels alongside the public ones.
- TRIAL REELS: if the user asks for a creator's Trial Reels (Instagram only, Pro plan and higher), call
  get_creator_videos with `type` set to 'trial' - or 'all' for public plus trial. Stored trials come back
  instantly; only the FIRST 'trial' request for a creator we hold none for takes about a minute while they
  are fetched. Leave `type` out unless the user actually asked about trial reels.
- Only call analyze_profile - a fresh re-analysis, still free but slower - when the user EXPLICITLY asks for
  freshly fetched data. Do NOT ask how many videos to scan - there is no count to choose; it always covers
  the creator's newest videos (up to 100) in ONE batch, back in ~60s TOTAL. It WAITS and returns the list
  itself (no sleep/wait). If it hands off with "Still working", call get_analysis_result ONCE (it waits too)
  until "All done.".
- You can narrow get_creator_videos by publish date: pass dateFrom/dateTo (ISO) or datePreset (past_7_days, past_30_days, past_3_months, past_6_months, past_year).

OUTPUT
get_creator_videos (and analyze_profile) returns a ready-to-show, ranked table of the creator's videos,
wrapped in copy-verbatim markers. Present it EXACTLY as returned - every row and column, in order, directly
under the widget. Do NOT re-rank, summarise, add emojis or long dashes, or build your own dashboard or
leaderboard. After the table, add ONE line on what their winners share (topic, hook style, or format). This
skill does NOT transcribe or script - offer to deep-dive the most interesting one with /meedro:analyze-video
for the full hook + transcript + templates. No internal ids.
