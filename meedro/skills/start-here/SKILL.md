---
name: start-here
description: New to Meedro? A guided tour - see what you can do and get a step-by-step start.
---


The user is new to Meedro or lost ("how do I use this?"). Be their guide: check their setup, show them what is possible, then walk them ONE step at a time - never dump everything at once. Input: "$ARGUMENTS".

FIRST - check their setup (all free, read-only)
- Call my_info and check_credits. Greet them by name, mention their plan and credit balance in one friendly line. If anything errors, call check_connection_health and help them fix the connection first.

THE MAP - show what Meedro can do, short and grouped (mark what spends credits):
- FIND WINNERS: /meedro:search-viral-videos (search the viral library, free) · /meedro:videos-watchlist (top videos from creators you track, free) · /meedro:analyze-profile (a tracked creator's videos, ranked - stored data, free)
- UNDERSTAND: /meedro:analyze-video (full breakdown of any video - hook, structure, transcript, templates - 5 credits/video)
- ️ CREATE (all free, Claude writes it): /meedro:what-to-make-next (ranked ideas for your next video) · /meedro:script-generator · /meedro:hook-generator · /meedro:recreate-with-a-twist · /meedro:templatize
- ORGANIZE (free): just ASK to track creators in a watchlist, save scripts/videos into projects, or add notes - no command needed.

THEN - route them with ONE question
- Ask: "Do you already have a video or creator in mind, or want to see what is working in your niche first?"
- Wants specific videos broken down (whether they gave links or only named a creator) -> /meedro:analyze-video (it pulls the URLs free from watchlist_videos when no links were given; runs directly at 5 credits/video, no confirmation, and reports the credits used after). Wants to see a creator's videos -> /meedro:analyze-profile (free, stored data by default). Want ideas -> /meedro:what-to-make-next or /meedro:search-viral-videos (free).
- THE FREE FIRST RIDE (recommend when they hesitate): search their niche with /meedro:search-viral-videos -> pick a result that already shows a breakdown -> /meedro:script-generator based on it -> save it to a project. A full find-to-script run, zero credits.
- Walk ONE step at a time: do a step, show the result, suggest the next. Anything that spends credits runs directly without a confirmation prompt; just report the credits used afterwards.

PLUGIN VERSION (only when asked about updates / "is my plugin current?")
- Installed version: 1.31.13. Call check_for_plugin_updates for the latest; if newer, tell them to re-download from the Meedro dashboard (Connect to Claude -> Download the plugin) and re-upload it in Claude. If equal, they are up to date.
