---
name: meedro-content-audit
description: Build a full agency-grade content audit of the user's own connected Meedro account as one polished, tabbed HTML report. MUST be used when the user asks for a "full audit", "complete audit", "content audit", "audit my account", "agency report", "the full report on my account", "analyze everything about my content", or any single deliverable that combines their performance, pillars, brand feel, playbook, growth plan, strategy, craft diagnostic, and scripts into one report. Pulls every number live from the Meedro MCP tools and renders an eight-tab dashboard (Performance, Content Pillars, Brand Clarity, Playbook, Growth Plan, Strategy, Weekly Diagnostic, Scripts and Calendar). Every stat, hook, thumbnail, and recommendation is real. Nothing is invented. For a single-section ask (just a weekly plan, just competitor mapping, just one script), a lighter dashboard is enough; use this when the user wants the whole picture in one file.
---


Meedro Content Audit
One command, one premium report. This skill produces a complete agency-grade content audit of the user's own connected account, rendered as a single self-contained HTML file with eight left-tab sections. Every number is computed live from real Meedro data. Nothing is guessed.

The eight tabs, in this exact order:

Performance
Content Pillars
Brand Clarity
Playbook
Growth Plan
Strategy
Weekly Diagnostic
Scripts and Calendar
The run flow
Identify the user. Call my_info (free). It returns their full name, niche, connected Instagram and TikTok usernames, and (when saved and enabled) their Brand Voice digest. Never ask for what my_info already answers. If both Instagram and TikTok are connected, my_reels will ask which platform; relay that question once, then proceed with their answer.

Pull the account data. Call my_reels with sort='outlier' (free). This returns the user's analyzed videos with the full breakdown per video: views, likes, comments, engagementRate, outlierScore, durationSec, publishedAt, topic, hook, hookFormat, transcript, storyBeats, visualHook, scriptTemplate. Compute across the FULL set, never a sample. If newUnanalyzedCount is above zero, note once, plainly, that the report covers the analyzed set (there is no re-analyze action; never tell the user to re-run it). If there are fewer than about 8 analyzed reels, say the patterns are a first pass that will firm up as they analyze more.

Pull competitor and niche data (last 6 months only). For the Content Pillars competitor section and the Brand Clarity niche-neighbor section, call search_viral_videos. Use query (a topic, keyword, or @handle), plus dateFrom set to six months before today and minOutlier around 3. You can also pass a category from its fixed list (for example content-marketing, ai-tech, make-money-online) and narrow with searchIn (hook, topic, caption, or username). Keep queries focused; if a broad phrase returns little, retry with a tighter keyword. Note that minEngagement/maxEngagement are PERCENT values (5 = 5%). If the user already tracks competitors in a watchlist, watchlist_videos also works; analyze_profile requires the creator to already be in a watchlist and needs an explicit platform. Keep only videos published in the last 6 months; discard older ones even if they went viral.

Compute every section from the real data per the section specs below. Silently re-read each hook from its transcript first line and correct the stored hook field where they disagree (backend only, never mentioned in the report).

Render one self-contained HTML file per the layout spec below, write it to /mnt/user-data/outputs/, and present it. Verify the hard rules before delivering (zero em/en dashes, real links only, balanced markup, closes </html>).

Offer to persist a Brand Voice. At the end, offer to distil the findings into a Brand Voice and save it via save_brand_voice. First check my_info (or get_brand_voice) for an existing one. Show the user the FULL exact voice text and save it ONLY after they explicitly approve it in this conversation, never automatically. Also offer to write more scripts or run a deeper competitor comparison.

Adapt to the user
User instructions override defaults: a requested color theme, an added section, a different language, a specific competitor, or a focus area all get honored, as long as no engine rule breaks (no fake data, no padded items, no missing sources).
Extra data the user provides (analytics screenshots, their own notes) is woven into the relevant section and labeled as their data.
The layout below is the proven quality baseline. You may adjust colors, spacing, or section styling when the user's brand or the data calls for it, as long as the result stays clean and editorial and every hard rule holds.
Error handling (never fail silently)
Auth or permission error: tell the user to reconnect the Meedro connector, then retry once.
Platform unknown and both connected: relay the my_reels platform question once. Never assume.
Long job interrupted: results persist server-side; resume with get_analysis_result. Never restart a batch. Re-running an analyzed URL is free.
Empty or off-niche competitor results: retry with a tighter query, a category, or a searchIn field; if still thin, show the honest shortfall rather than padding it, and note the scan caveat.
Very few analyzed videos: build what the data supports and say plainly which sections are a first pass.
Rules for the whole report (apply to every tab)
These apply to every tab. Read them before building anything.

Data honesty
Every number, ranking, hook, and recommendation is derived from the user's real Meedro data. Never invent a statistic, never fill a gap with a plausible guess, never present a pattern you did not actually compute.
If the data does not support a section, say so plainly rather than fabricating it.
Rank by the MEDIAN, never by count or raw total. The average is inflated by a single big outlier and describes almost none of the catalogue.
Patterns with a small sample (fewer than about 4 videos) are labelled directional, not proven.
Every video reference is a real link, never a placeholder. Cross-check each own-account link against the returned data. Competitor links must be from the last 6 months.
Three backend rules that NEVER appear in the report copy
Hook verification. Silently re-read every hook from the first spoken line of its transcript and correct the stored hook field where they disagree. Never write "verified against transcripts" or "auto-corrected" anywhere the user sees. Just use the correct hook.
No credits talk. Never mention credits, credit cost, or "0 credits spent" anywhere in the report.
No pinned-post claims. Pinned posts are excluded when videos are pulled, so isPinned is unreliable. Never say the user has zero pinned posts, never recommend pinning, never reference it. In the executive summary, the SWOT, and the weakness fixes, the lead fix is a framing or content change, never pinning.
Recency
Every recommendation and every competitor example must be from the last 6 months. Check the publish date on every competitor video before using it. Discard older ones even if they went viral, because the user needs current openings, not trends that already peaked.

Language and formatting
No em dashes or en dashes anywhere. Use commas and periods. Verify the count is zero before delivering.
No italics for emphasis. Keep body text regular weight.
Section headings are LARGER than the body text and BOLD.
Plain, short language. Explain every metric in everyday words the first time it appears. Never assume the user knows outlier, median, TOFU, or engagement rate; say what it means.
Shorten every explanation. Cut a dark callout box whenever its point is already in the heading or intro. Do not overwhelm the reader.
Labels: write "reels=8" not "n=8". Every chart axis needs a plain label and every color needs a key.
Charts and interactivity
Build every chart as hand-written inline SVG. No external chart libraries.
The trend chart dots are interactive: hovering shows the full video topic and its stats, clicking opens the real video in a new tab.
The scorecard frameworks (Brand Clarity, Weekly Diagnostic) each get an info popup explaining the framework in plain language.
Thumbnails
Prefer CloudFront URLs (d3c1ms5t889vei.cloudfront.net). Treat Instagram CDN links (fbcdn.net, cdninstagram.com) as short-lived and always provide a labelled fallback via onerror.

Tools
Use only MeedroAI tools (MeedroAI:*). Never substitute similarly named tools from other connectors. The tools this report uses:

my_info (free): the user's name, niche, connected Instagram and TikTok usernames, and Brand Voice digest when saved and enabled. Call first.
my_reels with sort='outlier' (free): the user's own analyzed videos with full breakdowns, up to about 50. The backbone of the report. Pass username or platform to choose among connected accounts; it asks which when ambiguous, so relay that once. It can also be narrowed by publish date with dateFrom/dateTo (ISO) or datePreset (past_7_days, past_30_days, past_3_months, past_6_months, past_year).
search_viral_videos: niche and competitor search across Meedro's library and all analyzed creator videos. Use query, dateFrom for the 6-month window, minOutlier, category (fixed enum), and searchIn to target a field. minEngagement/maxEngagement are percents. return='hooks_only' for compact hook lists.
search_account: find a creator by @handle, name, or niche keyword. Requires platform (ask if not given).
analyze_profile (free, requires platform, the creator must already be in a watchlist): scans a competitor's recent videos and returns them ranked. Pass sort='outlier' and filter (viral/hot/above/below) to focus. It is a fuller scan, so prefer watchlist_videos or search_viral_videos for quick reads.
watchlist_videos: recent top videos across tracked creators.
save_brand_voice: persist a Brand Voice (plain text, 50 to 10,000 chars). Show the full text and save only after explicit user approval. get_brand_voice reads the current saved voice; set_brand_voice_enabled toggles whether the MCP may use it (only when the user explicitly asks).
get_video_analysis, get_creator_videos (type 'trial'), analyze_video: read a stored breakdown, pull trial reels, or analyze a specific new video when needed (analyze_video costs 5 credits per new video; confirm the total first).
What each tab contains and how to compute it
Every section states its PURPOSE (why the user cares, write this into the intro in plain words) and its BUILD (how to compute it from the real data). Follow the tab order exactly. The trend chart colors dots by outlier band only: pink for viral (3x or more), green for above average (1.5x to 3x), grey for on pace or below. Never color by hook format.

Tab 01: Performance
ORDER within this tab: executive summary, honest numbers, top videos, trend over time, monthly views, video length, timing and cadence, then hook format performance last. Length and timing come before hooks because they are simpler production decisions. In the trend chart color dots by result using only three colors: pink for viral (3x or more), green for above average (1.5x to 3x), grey for on pace or below. Do not color by hook format.

1a. Executive summary (top of the report)
PURPOSE: give the creator the whole verdict on screen one, in plain words, so a busy reader knows what works, what is holding them back, and the one move that matters most, even if they read nothing else. BUILD: synthesise from the finished analysis, do not guess. One plain verdict line, framed as a simple contrast the creator can act on (for example, you win when you show something real and lose when you only talk about it). Then three cells: what you are best at (the highest performing pattern, with real numbers), what is holding you back (the clearest gap with evidence, but NEVER pinned posts), and the one move that matters most (the single action with the best reach for the least effort, explained simply, with a short why-this-one). Write this last, after every other section is computed.

1b. The honest numbers
PURPOSE: give the creator a truthful baseline that one viral video cannot distort, so every later comparison has a fair reference point. BUILD: open with a small snapshot card row (average views per reel with median noted beneath, average engagement rate with the top reel noted, how many of the videos are at or above the median line, and the single best outlier score). These are the impressive-but-skewed averages. Then, directly below, the median row (median views, median engagement, median outlier, median length) framed as the creator's true normal. Make the gap between the inflated average and the median the point: the average is pulled up by a few hits, the median is what a typical post really does.

1c. Best duration, best day, cadence mini-cards
PURPOSE: three fast production defaults the creator can apply to the next post. BUILD: best duration = the duration bucket with the highest median outlier. Best day = the weekday with the highest median outlier from publishedAt; label it directional if reels for that day are few. Cadence = posts per month and typical publish hour. (These can also live inside the timing section below.)

1d. Top videos by outlier score
PURPOSE: show the creator their strongest videos and the real performance gap. BUILD: a bar per video, outlierScore descending, top ~6 shown with FULL topic names (never truncated), each bar linking to the real video. Rank by outlier not raw views so one giant video does not hide the pattern. Keep the intro to one short sentence.

1e. Views and outlier trend over time (interactive)
PURPOSE: answer the question every creator worries about, am I growing or declining, by showing the real shape over time. BUILD: plot every video chronologically by publishedAt, y = outlierScore on a log axis if there is a large outlier, with the median as a reference line and proper axis labels. Color dots pink/green/grey by outlier band only, with a legend. Make each dot interactive: hovering shows the FULL video topic plus its outlier and views, clicking opens the real video in a new tab. Read the shape honestly in one line: occasional spikes versus steady climb versus decline. Do NOT restate the color meanings in the intro, the legend already shows them.

1f. Monthly median views
PURPOSE: separate a healthy stable baseline from real decline. BUILD: median views per publish month as a labeled bar chart. Flag small-sample months. If recent months look low only because early months were single breakouts, say so.

1g. Video length vs performance
PURPOSE: give a concrete length target backed by the creator's own results. BUILD: median outlier and median views for each duration bucket, three cards. Place this BEFORE the hook section.

1h. Timing and cadence
PURPOSE: give a testable posting-day recommendation from real timestamps. BUILD: median outlier by weekday as a labeled bar chart, all directional, flag small samples. Add cards for typical posting time and monthly cadence. Place this BEFORE the hook section.

1i. Hook format performance
PURPOSE: give the creator a reusable library of their own proven openers, ranked, so they reach for a proven style and copy the exact wording that worked instead of guessing. BUILD: this is the single hook section (there is no separate bar chart and no separate pattern bank anymore). For each hook pattern show reels count, median outlier, and one real example taken from the corrected first spoken line of the best performer in that pattern, linked to the real video, plus its reach. Rank by median outlier. Close with which pattern is the most consistently high- returning (highest median at healthy sample), not just the one holding the single biggest outlier.

Do NOT include a "hidden signal" comment-ratio card. It was removed.

Tab 02: Content Pillars
2a. Your pillars (list every video as proof)
PURPOSE: show the creator what their account is actually about and which themes reward them most per post. BUILD: group every video's topic into 4-7 pillars. Per pillar compute count, median outlier, median views, and the best video as linked proof. Rank by median outlier. Tag each pillar with the buyer-journey stage it serves (Know / Like / Trust). Then list EVERY analyzed video under its pillar, sorted by outlier, each linked, so the ranking is fully backed by clickable proof. Close with the real spread between top and bottom pillar in one short line.

2b. Discoverable versus community content
PURPOSE: show whether content is built to reach strangers or deepen the existing audience, and whether that mix serves them. BUILD: classify every video into discoverable (searchable how-tos, tutorials, resources, comparisons) or community (personality, mission, behind the scenes). Compute the split percentage and median outlier and median views per type. State the ratio, say which performs better, and note if strong discoverable content still only reaches existing followers because it sits in saturated pillars. Keep any callout short.

2c. Competitor openings (pillars they own that you have not started)
PURPOSE: hand the creator proven, high-reach pillars where demand is already established in their niche and they have zero presence. BUILD: from the live niche scan, identify 2-3 recurring high-reach pillars the creator has not made, using ONLY competitor videos from the last 6 months. Check each publish date and discard anything older, even if it went viral. For each pillar give real competitor examples with real hooks and view counts, all linked, plus one concrete starter topic adapting the pillar to the creator's proven format. Note that view counts came from the niche scan and are worth a quick check before building on them.

Tab 03: Brand Clarity
This tab reads the FEEL and framing of the brand, not the raw numbers. Each scorecard framework gets a small "i" info button that opens a plain-language explanation of what the framework means. Keep section copy short. Do NOT put a long dark callout box under each section; if the insight is already in the sub-heading, do not repeat it.

3a. AAA scorecard (Appealing, Effective, Authentic)
PURPOSE: grade the brand on attention, emotional connection, and credibility. BUILD: three rows, each with a short read from the real videos and a one-word verdict chip (strong / mixed / weak). Appealing = visual and audio attention (is the look fresh or plateaued). Effective = does it make people feel something (use real engagement and the share of videos above the median). Authentic = does personal, first-hand proof show up in the higher performers. Info popup text: the AAA Rule ensures content has viral potential by hitting three markers. Appealing is grabbing attention visually and auditorially with strong visuals, purposeful lighting, dynamic movement, and crisp clean audio. Effective is whether the viewer feels an emotion (joy, pain, curiosity, nostalgia) through facial expressions, tone, and body language. Authentic is feeling real and unique, achieved by speaking from personal experience and not trend hopping or using fake-guru vibes.

3b. Triple C scorecard (Colors, Cinema, Consciousness)
PURPOSE: grade the brand on visual identity and depth. BUILD: three rows with short reads and verdict chips. Colors = is the palette consistent and recognisable. Cinema = are videos directed (shots, angles, cuts) or just recorded static. Consciousness = is there a real point of view or a repeated scripted CTA acting as filler. Info popup text: the Triple C Rule makes a personal brand feel unique and respectable. Colors form the visual identity, a consistent two-to-four color palette for instant recognition. Cinema is visual storytelling through shots, angles, cuts and pacing, treating videos like movies with intentional movement rather than a static face. Consciousness is purpose and soul, sharing real stories and values and speaking from the heart rather than repeating a script or empty motivation.

3c. Are you teaching or connecting? (story vs lesson)
PURPOSE: show whether the creator teaches AT people or connects with them. The best creators run roughly 80% story to 20% lesson. BUILD: classify every video as pure instruction or story/personal, from the transcript, and show the ratio as two bars. List the real pains and dreams the audience shows (drawn from the creator's own topics, comments, and captions). Do not add a dark callout box; the heading and bars carry the point.

3d. Story framing beats plain teaching (conversion split)
PURPOSE: show that the same idea performs far better told through the creator's own story than as a plain lesson. BUILD: this is based on how each video is FRAMED, read from the transcript, not just the topic and not the hookFormat field. Say so plainly in the intro. Show a linked bar per video: personal/story-framed winners near the top, straight- educational versions near the floor, each with its real outlier. The takeaway, stated once and briefly: they do not need new topics, they need to frame the ones they have through their own experience. No dark callout box.

3e. Niche neighbor intelligence
PURPOSE: list the current patterns worth borrowing from top performers next to them in the niche. BUILD: from the live niche scan, last 6 months only, give 2-3 patterns to steal, each with a short read and a real recent proof point (handle, views, outlier). Note the scan caveat once.

Tab 04: Playbook
PURPOSE: turn the whole analysis into a simple green-light / red-light list the creator checks every future idea against. BUILD: split winners from losers at the natural performance break. For topics, formats, and hooks, give at least 5 "do more of this" and 5 "stop doing this" entries. Every entry cites one real video, its real stat, and links to it. Use the corrected first-line hook for any hook example. Keep the intro to one line.

Tab 05: Growth Plan
5a. Your funnel, filled in with all your videos (put this FIRST)
PURPOSE: show where content sits in the customer journey and, most importantly, which stage to prioritise next. The funnel comes before topics because which KIND of content to make is the bigger decision. BUILD: use the creator's own funnel definition if they have a video on it. Classify every video into their stages, top first. Per stage compute count, median outlier, median views, best performer linked. Then a clear focus recommendation box: name the single stage to prioritise next and why in plain terms. If a lower stage outperforms an upper stage, explain what that means (they convert well but do not reach enough new people, so fix top of funnel). Give a short priority list: what to add, what to keep steady, what not to over- invest in. Then per-video bars grouped by stage, each linked.

5b. What to film next, and why it works now
PURPOSE: give specific next videos with the reasoning and proof behind each. BUILD: 5 specific topics (not vague categories). Each carries a why-it-works line, then a "Why now:" line ON ITS OWN NEW LINE, tied to real evidence: a gap in the strongest pillar, an adjacent topic sharing a proven format, a live niche proof point from the last 6 months with real views, or a demand signal in the creator's own comments. Link every proof point. Never use competitor videos older than 6 months.

Tab 06: Strategy
6a. SWOT (four boxes)
PURPOSE: a one-screen executive summary of the whole audit. BUILD: render as four clear boxes with a colored accent and a short label chip each (for example WIN, FIX, GROW, WATCH) and a readable heading. Strengths and weaknesses are the highest and lowest performing real format and pillar combinations, cited with numbers. Opportunities are proven demand not yet captured (the competitor pillars, the missing funnel stage, unanswered comment demand). Threats are patterns that will cap growth if unchanged (share of below- median output, reach ceiling, repetition). Every cell cites real data. Do NOT reference pinned posts anywhere.

6b. Improve your weakness (ranked fixes)
PURPOSE: a ranked, do-this-first fix list, biggest return for least effort. BUILD: rank fixes by leverage over effort. Lead with the fastest high-impact fix, which should be a low-effort framing or content change (for example, lead with a short personal story before teaching), NEVER pinning posts. Each fix names what is failing with evidence, what proven pattern to borrow, and one concrete test video.

Tab 07: Weekly Diagnostic
This tab reads the CRAFT inside the videos, the visual, verbal, and audio choices. Each framework gets a small "i" info button with a plain explanation. Keep copy short.

7a. VVA framework (Visual, Verbal, Auditory)
PURPOSE: check the video works across all three ways a person takes it in. BUILD: three rows with short reads and verdict chips. Visual = set, framing, props, novelty. Verbal = does the opening line carry a stake or a number. Auditory = clean audio and a spoken hook in the first second. Info popup: VVA checks a video works across sight, words, and sound. Visual is what the viewer sees. Verbal is the words, especially the opening line. Auditory is clean audio plus a spoken hook so the video lands even when someone is not looking directly at the screen.

7b. Hook layering (visual + text + audio in first 3 seconds)
PURPOSE: show whether the opening hits all three channels at once. BUILD: check the last several videos. Mark each with a check or cross for whether visual, text, and audio hooks fire together in the first 3 seconds, with its real views. Note that most leading on one channel only leaves reach on the table.

7c. Fluff diagnostic
PURPOSE: name what to cut so people keep watching. BUILD: list the specific weak openings, slow middles, and filler lines from real videos, each with a short "cut this" instruction.

7d. Next session checklist
PURPOSE: a short, tickable list of what to change before the next shoot. BUILD: five concrete items drawn from the diagnostics above (bring a prop, open with a number, layer the hook, add one camera move, move the generic CTA out of the opening). Render the checkbox as a clean drawn box, not a raw text character.

Tab 08: Scripts and Calendar
8a. Full scripts
PURPOSE: ready-to-film scripts that are safe bets because they reuse the exact mechanic of a video that already worked for the creator. BUILD: pick 2-3 source videos from the creator's real winners. For each, write a new script that PRESERVES the source's mechanic exactly: same structure, beat sequence, pacing, and CTA style. Change ONLY the topic, adapting it to a gap from the Growth Plan, in the creator's real voice from their transcripts. Show the linked source and label each beat with which source beat it mirrors. Include the hook (a proven pattern), the full body, a CTA in their proven style, and on-screen text suggestions.

8b. Weekly plan with per-day strategy
PURPOSE: a concrete, shoot-ready posting week, sequenced so a new viewer is carried from discovery to conversion across the week. BUILD: five day cards (not a bare table). Each names the day, the topic, the pillar, and the funnel stage, and explains in plain words the content strategy: what job that post does (reach new people, warm them up, build trust, convert, connect), why it sits on that day, and how to shoot it. Put the biggest reach bet on the creator's strongest posting day. Every topic traces to a real finding, and the scripts from 8a cover the highest-priority days. Do NOT add a dark summary callout box at the bottom.

Output format and layout (the premium dashboard)
Produce ONE self-contained HTML file. No build step, no external JS libraries, no frameworks. Everything (markup, CSS, a little vanilla JavaScript) lives in that single file so the creator can open it in any browser or hand it to a client. The goal is a report that looks like a premium agency deliverable, not a data dump. The tokens, fonts, and structure below are the proven baseline from the shipped reports. Follow them for quality, but you MAY adjust colors, spacing, or section styling when the creator's brand or the data calls for it, as long as the result stays clean, editorial, and consistent.

--- Overall shape --- A two-column app: a fixed LEFT RAIL with clickable tab navigation, and a wide CONTENT PAGE on the right. The page opens with a dark COVER banner, then shows exactly one tab PANEL at a time. Clicking a rail tab swaps the visible panel.

--- Design tokens (put these in :root) --- --ink:#0F1210; dark near-black, used for cover, rail, callouts, body bg --paper:#FAF7F0; warm off-white, the main page background --paper-dim:#F1ECE0; slightly darker paper, for chips and list rows --signal:#B8FF3C; acid green, the one accent, for the active tab and hero --signal-deep:#4A6B0E;deep green, for links, stats, and small accents on paper --gray:#6B6459; muted text, labels, secondary copy --line:#E4DFD3; hairline borders --white:#FFFFFF; card backgrounds that sit on paper --do-bg:#E7F5CE; --do-text:#3F6B0E; green pair for "do this" / positive --dont-bg:#F3E3DD; --dont-text:#8C3E22; red pair for "stop this" / negative --alert-bg:#FBEFD2; --alert-text:#7A5A0A; amber pair for cautions --blue:#4A6B8A; --tan:#8B8567; two supporting accents The acid green is used sparingly: the active tab, the hero name, small accents. Never flood a section with it.

--- Fonts (Google Fonts) --- Fraunces (serif) for display: the cover H1, section headings, big stat numbers. Inter (sans) for body copy and tab labels. IBM Plex Mono for data labels, stat captions, eyebrows, and axis text. Load: Fraunces 400/500/600, Inter 400/500/600, IBM Plex Mono 400/500. Do NOT use italics for emphasis. Keep body text regular weight.

--- The shell (structure to reproduce) --- body: background var(--ink), Inter, color var(--ink). .layout: max-width ~1220px, centered, CSS grid, two columns 250px + 1fr, background var(--paper), min-height 100vh. .rail: the left nav. Sticky, full height, own scroll, right hairline border, dark background. Contains, top to bottom: the brand word "Meedro" (Fraunces, light on dark), the creator handle beneath it, a small "Sections" label, then the tab buttons, then a small footer line ("N analyzed videos / Prepared <date>"). .tab-btn: full-width, left-aligned, no border, pointer cursor, a small two-digit number span then the UPPERCASE tab name. The active one gets background var(--signal) and dark text. Inactive are light text on the dark rail. .page: the right column (min-width:0 so charts can shrink). .cover: dark banner, generous padding. Contains a mono eyebrow ("Meedro content audit / confidential"), an H1 in Fraunces ("The complete audit of <creator>", the handle in acid green), a one-line plain-language summary of what the report is, and a small meta row (Account, Niche, Videos analyzed). .panel: one per tab, display:none by default, .active shows it with a quick fade. Padding roughly 3rem 3.5rem. Each panel opens with a mono .panel-index ("01 / PERFORMANCE") then the section H2 in Fraunces.

--- Tab switching (the only required JavaScript for nav) --- Give each tab button a data-tab that matches a panel id. One tiny script: collect the buttons, on click toggle .active on the matching button and panel, and scroll to top. Keep it dependency-free. Because it is id-based, panels do not need to sit in visual order in the markup, but the rail buttons must be in the intended reading order with correct numbering.

--- Section headings and copy --- Section headings (the subsection labels inside a panel) are LARGER than the body text and BOLD, in Fraunces (around 19px, weight 600), with a hairline underline. Body copy is short and plain. A section gets a one or two line intro that states its purpose, then the content. Do NOT stack long paragraphs. Cut a dark callout box whenever its point is already in the heading or intro.

--- Cards, tables, callouts (reusable pieces) --- .chart-frame: white card with hairline border and rounded corners, wraps every chart. Stat cards: white card, a big Fraunces number, a mono caption, and an optional small colored note chip (green for good, red for a warning). .data table: full width, small font, hairline row borders, mono for numeric cells, a colored "outlier pill" for the outlier value. Every video row links. .callout: dark rounded box for a single important takeaway, used sparingly. "do / stop" blocks: two columns, green card vs red card, each entry linked. Verdict chips: small mono pills (strong = green pair, mixed = amber, weak = red) used in the scorecard rows.

--- Charts (render as inline SVG, no libraries) --- Build every chart as hand-written SVG sized to a viewBox, width:100%. 1. Top videos bar chart: horizontal bars, one per top video, outlier descending, FULL topic label (never truncated, give the label column enough width), the bar, and the outlier value. Each row is a link to the real video. 2. Trend over time (interactive): plot every video chronologically, x = time with month labels, y = outlier score on a LOG axis when there is a big outlier, with gridlines, axis labels, and a dashed median reference line. Color each dot by band ONLY: pink (#E84393) viral 3x or more, green (#2ECC71) above average 1.5x to 3x, grey (#9A968A) on pace or below. Add a three-item legend. Make dots interactive (see below). 3. Monthly median views and Timing: vertical bar charts with real x and y axes, plain axis labels, the value above each bar, and the sample size ("reels=N") beneath. Do not leave a bar chart unlabelled. Give each chart a plain axis label and, where colors carry meaning, a legend.

--- Interactive functions (vanilla JS, in the same file) --- a) Trend dots: give each dot data-url, data-topic, data-stat. On hover, show a small dark tooltip near the cursor with the FULL topic, the stat line, and a "Click to open video" hint; the tooltip flips side near edges so it never overflows. On click, window.open the real video in a new tab. Do NOT use raw SVG <title> tooltips (they truncate and lag) or SVG wrappers (unreliable clicks); use a positioned HTML tooltip div and JS listeners. b) Framework info popups (Brand Clarity and Weekly Diagnostic): each scorecard heading gets a small round "i" button with a data-modal key. Clicking it opens a centered modal overlay with the plain-language explanation of that framework. Close on the X, on overlay click, and on Escape. One overlay, swap which modal is shown by key. c) Checklist boxes: render the checkbox as a small drawn CSS box (a bordered square), never a raw unicode character that may not render.

--- Quality bar and hard rules for the file --- - No em dashes or en dashes anywhere. Use commas and periods. (Verify before delivering; the count must be zero.) - Every video reference is a real link, never href="#". - Balanced markup, valid single file, closes </html>. - No italics for emphasis. - The left rail order and numbering match the eight tabs exactly. - It should look finished enough to sit in a paid client deliverable.

You may extend this system (extra card types, an added chart, a tweaked accent) when the data or the creator's brand justifies it, as long as you keep the editorial feel, the token discipline, and every hard rule above.
