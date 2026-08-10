---
name: viral-hook-library-display
description: Display the Meedro viral hook library tool result as a complete markdown table directly below the iframe on the FIRST response. Use when the tool `viral_hook_library` is invoked.
---


# Viral Hook Library Display

When the `viral_hook_library` MCP tool returns a result, the response has two parts: a video-card iframe (rendered by the host) and a markdown table (in the tool's text content). The table is already complete and ready to relay. Your job is to put it on screen on the FIRST message - not summarize it, not reformat it, not ask the user to confirm.

## Rule: show the table immediately

After the tool returns, your response must contain the full markdown table the tool produced, copied verbatim, in the same turn. No "here's the data:", no "the top 5 hooks are:", no "let me know if you want this in a table." The table is the answer.

The 9 columns, in this exact order:

| ID | Creator | Hook | Hook Format | Hook Template | Why It Went Viral | Views | Video Link | Niche |

## Rule: no surrounding prose

Do not add an H1 header, a "Top N hooks of the month" intro, a "Want the full breakdown?" CTA, a credits line, a refresh-cadence line, a month name, or an ORDER_NOTE. None of these are in the tool text - keep your response the same shape: just the table.

A one-line acknowledgement before the table is OK if the user asked a question (e.g. "Here are the top hooks:"), but the table must be the dominant content of your message.

## Rule: missing fields stay as the tool rendered them

If a row shows em-dash (`-`) for any field, that is the source-of-truth value. Do not invent likes, comments, engagement, or outlier scores. Do not call additional tools to "fill in" missing stats. Relay the dashes as-is.

If the tool returned an empty hooks array, the response is the table header plus whatever the tool emitted (typically `_No hooks available._`). Do not invent example rows. Do not call `search_viral_videos` to populate it.

## Rule: never strip the iframe

The video cards render in the host's UI above your text. Do not describe them in prose ("there are 5 cards above"), do not list them as numbered items, do not duplicate their content. Just add the markdown table directly below.

## Rule: no business-logic prose

Never say anything like:
- "This list refreshes monthly"
- "It's the same for everyone"
- "This is free, no credits spent"
- "Want the full breakdown? (5 credits)"
- Month names (July, August, …) as headings

Those are internal business facts. The tool does not emit them. You must not either.

## What to do when the user asks a follow-up

- **"Show me the table"** → the table is already in your previous response; reference it, do not re-call the tool unless the user explicitly asks for a refresh or filter.
- **"Filter to Instagram only"** → re-call `viral_hook_library` with `platform: "instagram"`.
- **"More about hook X"** → use `get_video_analysis` with the video's link (the row's Video Link column is the link).
- **"Top hooks on a specific topic"** → use `search_viral_videos` with `return: "hooks_only"`, not this tool.
- **"Why is column Y missing?"** → answer from the tool's empty/missing semantics; do not invent data.

## Anti-patterns to avoid

- Summarising the table into prose ("Hook #1 uses a Question format and got 120K views…")
- Adding an H1 like "# Viral Hook Library" before the table
- Reformatting columns (e.g. mashing "Views/Niche" into one cell)
- Adding a footer like "_Want to dig into any hook? Ask me._"
- Calling another tool to "enrich" missing stats
- Asking "Want to see the full list as a table?" - the table is already there
