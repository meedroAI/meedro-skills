---
name: manage-projects
description: Use whenever the user works with My Projects - listing projects, browsing saved videos or scripts and their notes, or asking for the FULL insights/breakdown/transcript of saved videos. Free (a saved video replays its stored breakdown at no charge).
---


The user is working in My Projects - projects plus the videos and scripts they saved into them. Input: "$ARGUMENTS".

BROWSE
- Projects: list_projects. A project's saved videos: list_saved_videos (the project name is REQUIRED - ask which project if not given; list_projects shows the names). Saved scripts: list_saved_scripts.
- list_saved_videos returns a compact TABLE (Creator, Caption, Views, Outlier, Engagement, Link) alongside the card grid - a browse view, not the full breakdown. Present that table verbatim under the cards.
- You can narrow list_saved_videos by publish date: pass dateFrom/dateTo (ISO) or datePreset (past_7_days, past_30_days, past_3_months, past_6_months, past_year).

FULL INSIGHTS OF SAVED VIDEOS (this is the important part)
- When the user wants the full insights / breakdown / transcript of saved videos, do NOT stop at the table. Take the video Link(s) from list_saved_videos and run analyze_video on them. Saved videos are already analyzed, so this is a FREE replay - no credits, no confirmation - that returns each video's complete Video Insight.
- Present each Video Insight EXACTLY as analyze_video returns it, following the /meedro:analyze-video OUTPUT rules: every section INCLUDING the complete "Full Transcript", for EVERY video, in the same reply, in order, never summarised, shortened or re-ordered.
- MANDATORY - always show the full transcript: a breakdown shown without its complete "Full Transcript" section is INCOMPLETE. Reproduce every transcript word for word, no matter how long it runs or how many videos there are, and never point the user elsewhere for it instead of showing it.

MANAGE (destructive actions = confirm first)
- Save a video/script to a project: save_video / save_script (ask which project by name). Notes: add_note_to_saved_video / add_note_to_saved_script. Edit a script: edit_script.
- Rename or delete a project (edit_project / delete_project), or unsave a video/script (unsave_video / unsave_script): show the exact target and get the user's explicit confirmation BEFORE calling - these remove data.

Never show internal ids. Refer to everything by its project / video / script name.
