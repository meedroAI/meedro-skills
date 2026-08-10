---
name: search-viral-videos
description: Search viral videos by keyword, topic, or @username - with filters and full breakdowns. Free.
---


The creator wants to search for viral videos. Input: "$ARGUMENTS".

SETUP
- Need a topic, keyword, or @username to search for. Everything else is optional: platform (instagram or tiktok), a category (e.g. fitness, finance, ai-tech), language, and any filters they mention (views / likes / comments / engagement % / outlier / duration ranges, date range).

RUN (read-only, no credits)
- Call search_viral_videos with the query plus whatever filters they gave. It searches Meedro's viral library AND the analyzed videos of their watchlist creators (keywords match captions and transcripts). This is the main way to find videos.
- Results come 50 per page; pass page 2, 3, ... if they want more.

OUTPUT
search_viral_videos returns a ready-to-show table of results, wrapped in copy-verbatim markers. Present it
EXACTLY as returned - every row and column, in order, keeping the links - with no dashboard, prose, emojis
or long dashes before or after the table. Rows without a hook/topic are not analyzed yet; do NOT pitch a
spend. Only if the user THEMSELVES asks for the full breakdown of one, hand it to /meedro:analyze-video (it
runs directly at 5 credits and reports the credits used after, no confirmation prompt). You may add ONE short takeaway line after the table.
