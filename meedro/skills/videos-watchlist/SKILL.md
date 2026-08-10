---
name: videos-watchlist
description: See the top recent videos from the creators you track. Free.
---


The creator wants the top recent videos across the creators they track. Filter/context: "$ARGUMENTS".

SETUP
- ASK: all videos, or just Trial Reels (Instagram Trial Reels - shown only to non-followers)? Map the answer to `type` ('all' or 'trial'; default 'public' if they clearly mean normal videos).
- Optional, only if the user cares: how to order - latest (default), most-viewed, most-engaging, or biggest-outlier (`sort`: recent/views/er/outlier). Optional: narrow to only viral or over-performing videos (`filter`: viral/hot/above/below; default 'all'). Optional: narrow to only some of the tracked creators (`creators`, by @username) - it still comes back as ONE combined list and ONE widget.

RUN (read-only, no credits)
- Call watchlist_videos with `type` (and `sort`/`filter`/`creators` if the user asked for them) to pool the watchlist creators' best recent videos into ONE combined list. Shows up to 50 per page by default - if they want more, call again with `offset` set to the previous limit to page further.
- You can narrow watchlist_videos by publish date: pass dateFrom/dateTo (ISO) or datePreset (past_7_days, past_30_days, past_3_months, past_6_months, past_year).
- ROUTING: this tool always pools into ONE widget, whether it is the whole watchlist or the `creators` subset. If the user wants each creator shown SEPARATELY, one widget per creator, use /meedro:analyze-profile once per creator instead.

OUTPUT
watchlist_videos returns a ready-to-show table of the tracked creators' top recent videos, wrapped in
copy-verbatim markers. Present it EXACTLY as returned - every row and column, in order, directly under the
widget - no dashboard, leaderboard, emojis or long dashes. You may add ONE short takeaway line after the
table. Next: /meedro:analyze-video to break one down, or /meedro:what-to-make-next to turn the trend into an
idea. If the watchlist is empty, say so and offer to start tracking creators (add_to_watchlist - ask for the
@username and platform). No internal ids.
