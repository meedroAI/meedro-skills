---
name: meedro-content-audit
description: Build a full agency-grade content audit of the user's own connected Meedro account as one polished, tabbed HTML report. MUST be used when the user asks for a "full audit", "complete audit", "content audit", "audit my account", "agency report", "the full report on my account", or any single deliverable combining performance, pillars, brand feel, playbook, growth plan, strategy, craft diagnostic, and scripts. Pulls every number live from the Meedro MCP tools. Every stat, hook, and recommendation is real. Nothing is invented.
---


# Meedro Content Audit Skill

One command, one premium report. A complete agency-grade content audit of the user's own account, delivered as a single self-contained HTML file with eight left-rail tabs. Every number comes from live Meedro data. Nothing is guessed or padded.

---

## TOOLS (MeedroAI only - never substitute tools from other connectors)

| Tool | Cost | What it returns |
|---|---|---|
| my_info | Free | Handle, niche, connected platforms, Brand Voice digest |
| my_reels sort='outlier' | Free | All analyzed videos with full breakdown: views, likes, comments, engagementRate, outlierScore, durationSec, publishedAt, topic, hook, hookFormat, transcript, storyBeats, visualHook, scriptTemplate |
| search_viral_videos | Free | Niche and competitor video summaries from the library. Returns stats and metadata only, no transcript. Use dateFrom for 6-month window, minOutlier, category, searchIn. Single keywords only |
| search_account | Free | Find a creator by handle, name, or keyword. Requires platform |
| watchlist_videos | Free | Top videos from tracked creators with full breakdowns and transcripts included |
| analyze_profile | Free if creator is already on a watchlist. 50 credits if not yet in Meedro | Competitor stats, follower count, catalogue median. Requires explicit platform. Check watchlist membership before calling |
| get_brand_voice | Free | Full saved Brand Voice text. Read this to write scripts in tab 08 in the user's voice |
| get_video_analysis | Free if the user has already requested this video before. 5 credits first time on a library video | Full stored breakdown including transcript. Use this to read library videos. Never call analyze_video on a library video just to read it |
| analyze_video | 5 credits per not-yet-analyzed video | Analyze a specific new video. State exact cost and balance, wait for explicit yes before calling |

---

## STEP 0 - IDENTIFY AND CONFIRM (before pulling any data)

Call my_info first. It returns the connected handle, niche, and platforms. Never ask for what my_info already answers.

**If both Instagram and TikTok are connected:** ask once which platform to audit. Wait for the answer before calling my_reels.

**If no account is connected:** tell the user plainly: "I do not see a connected account. Connect your Instagram or TikTok in settings and I will run the full audit." Do not proceed.

Once confirmed, say in one line which account and platform you are building for, then proceed without further questions.

---

## STEP 1 - PULL THE DATA (silent, no narration)

Use two targeted pulls, not one. This keeps context lean and gives each tab the right time horizon.

**Pull 1: Recent performance (6 months)**
Call my_reels with sort='outlier' and datePreset='past_6_months'. Pull pages 0 and 1 (up to 40 reels). Check hasMore but stop at page 1 regardless. This is the primary data source for tabs 01, 02, 04, 05, 06, 07, and the scripts in tab 08.

If Pull 1 returns fewer than 8 reels, silently widen to datePreset='past_year' and pull again. Tell the user once that the report covers the last 12 months because the last 6 did not have enough data.

If the year pull also returns fewer than 8, pull with no date filter (all time, pages 0 and 1). Tell the user the report covers their full analyzed history and patterns are directional.

**Pull 2: All-time top performers**
Call my_reels with sort='outlier' and no date filter. Pull page 0 only (20 reels). Use this for tab 01 honest numbers baseline, tab 03 brand clarity, and tab 08 scripts source selection. This gives the strongest ever performers regardless of age, which is what those tabs need.

**If newUnanalyzedCount is above zero:** note once in plain language that the report covers the analyzed set. There is no re-analyze action. Never tell the user to re-run it.

**If fewer than 8 reels in total across both pulls:** tell the user the patterns will be a first pass and ask if they want to continue. If yes, build what the data supports and say plainly which sections are thin.

For competitor and niche data (tabs 02 and 03 only): call search_viral_videos with dateFrom set to 6 months before today and minOutlier around 3. Use single keywords, not phrases. Discard any result older than 6 months even if it went viral. search_viral_videos returns summaries only with no transcript, which is enough for identifying competitor topics and pillars. This costs zero credits.

If deeper competitor reads are needed (transcripts or hook verification): call get_video_analysis. This is free if the user has already requested that video before. It costs 5 credits the first time on any library video. Before calling get_video_analysis on any library video, state the count and total cost in chat and wait for explicit yes.

If analyze_profile is needed for a competitor: this is free if the creator is already on the user's watchlist. It costs 50 credits if the creator is not yet in Meedro at all. Check watchlist membership before calling. Never call analyze_profile silently on an untracked creator.

---

## STEP 2 - COMPUTE EVERYTHING IN CODE

Before writing any HTML, compute in code:
- Median and average views, engagement, outlier score across the full set
- Per-pillar median outlier and median views
- Hook format performance ranked by median outlier
- Discoverable vs community split and per-type medians
- Best duration bucket by median outlier
- Best posting day by median outlier from publishedAt timestamps
- Monthly median views

Rank every list by median, never by raw average or total count. The average is inflated by a single big outlier and describes almost none of the catalogue.

Hook autocorrect (silent): for every hook used anywhere in the report, use the stored hook field if it reads as a real spoken opening line. If it looks like a caption, a CTA, a hashtag line, or does not read as something said out loud at the start of a video, silently verify against the transcript and replace it with the first spoken line. Never mention this on the page.

---

## STEP 3 - BUILD THE EIGHT TABS

Build in reading order. Write Tab 01's executive summary last, after all other tabs are computed. Tabs 01 (trend, timing, hooks), 02, 04, 05, 06, and 07 use Pull 1 (recent 6 months). Tab 01 honest numbers and Tab 03 use Pull 2 (all-time top performers). Tab 08 scripts draw from Pull 2 for source selection but adapt topics from Pull 1 growth plan gaps.

---

### TAB 01: PERFORMANCE

**Order within this tab:** executive summary (written last), honest numbers, top videos by outlier, trend over time, monthly views, video length, timing and cadence, hook format performance.

**1a. Executive summary**
Write last. One plain verdict line framed as a contrast the user can act on. Three cells: what they are best at (highest performing pattern, real numbers), what is holding them back (clearest gap, never pinned posts), and the one move that matters most (single action, best reach for least effort, short reason why). Each cell names a real number and links a real video.

**1b. Honest numbers**
Snapshot card row: average views, average engagement, count at or above median, best outlier score. Then the median row directly below: median views, median engagement, median outlier, median length. Make the gap between the inflated average and the honest median the point.

**1c. Top videos by outlier**
Horizontal bar chart. Outlier descending, top 6 videos. Full topic label, never truncated. Each bar links to the real video.

**1d. Trend over time (interactive)**
Plot every video by publishedAt on x, outlierScore on y (log axis when a large outlier exists). Dashed median reference line, month labels, gridlines. Color dots by band only: pink (#E84393) for 3x or more, green (#2ECC71) for 1.5x to 3x, grey (#9A968A) for below. Three-item legend. Each dot is interactive: hover shows full topic plus stat, click opens the real video. Do not restate colors in the intro.

**1e. Monthly median views**
Vertical bar chart. Median views per publish month. Flag small-sample months. Plain axis labels and values above each bar.

**1f. Video length vs performance**
Three cards showing median outlier and median views per duration bucket. One short sentence per card.

**1g. Timing and cadence**
Median outlier by weekday as a labeled bar chart. Cards for typical posting time and monthly cadence. Flag small samples as directional.

**1h. Hook format performance**
One section covering hook patterns. Per pattern: reels count, median outlier, one real example from the best performer linked to the real video. Rank by median outlier. Close with which pattern is most consistently high-returning.

---

### TAB 02: CONTENT PILLARS

**2a. Your pillars**
Group every video into 4 to 7 pillars. Per pillar: count, median outlier, median views, best video as linked proof. Rank by median outlier. Tag each pillar with the buyer journey stage it serves. List every analyzed video under its pillar, sorted by outlier, each linked.

**2b. Discoverable vs community content**
Classify every video into discoverable (tutorials, how-tos, comparisons) or community (personality, behind the scenes). Compute split percentage and per-type medians. State which performs better and whether the mix serves the creator's current stage.

**2c. Competitor openings**
From the live niche scan: 2 to 3 high-reach pillars the user has zero presence in, using only videos from the last 6 months. Check every publish date and discard anything older. For each: real competitor examples with real hooks and view counts, all linked, plus one concrete starter topic for this creator.

---

### TAB 03: BRAND CLARITY

Each scorecard framework gets a small info button that opens a plain-language popup explaining what the framework means. Keep section copy short.

**3a. AAA scorecard (Appealing, Effective, Authentic)**
Three rows with a one-word verdict chip each (strong, mixed, weak) and a short read from real videos.
Info popup text: "The AAA Rule checks three things. Appealing is grabbing attention visually and with sound. Effective is whether the viewer feels something. Authentic is whether it feels real and personal, not polished or generic."

**3b. Triple C scorecard (Colors, Cinema, Consciousness)**
Three rows with verdict chips. Colors = visual consistency. Cinema = shot quality and movement. Consciousness = whether the content has a clear point of view.
Info popup text: "The Triple C Rule checks how your brand looks and feels. Colors is visual consistency across your videos. Cinema is shot quality, framing, and movement. Consciousness is whether your content has a clear perspective, or whether it could belong to anyone."

**3c. Story vs lesson ratio**
Whether the creator mostly teaches or mostly connects through story, and which performs better in their own data.

---

### TAB 04: PLAYBOOK

At least 5 do-more entries and 5 stop-doing entries. Two columns, green vs red. Each entry names one specific thing, cites a real number, and links a real video as proof. No generic advice. Every item is checkable.

---

### TAB 05: GROWTH PLAN

**5a. Your funnel**
Map every video to a funnel stage: top (reach new people), middle (build trust), bottom (convert). Per stage: count, median outlier, median views, best video linked. A clear focus box naming the single stage to prioritize next and why in plain terms. If a lower stage outperforms an upper one, explain what that means.

**5b. What to film next**
5 specific topics, not vague categories. Each with a why-it-works line, a "Why now:" line on its own line, and a proof point: a gap in the strongest pillar, an adjacent topic on a proven format, a niche proof point from the last 6 months with real views, or a demand signal. Link every proof point.

---

### TAB 06: STRATEGY

**6a. SWOT**
Four clear boxes with a colored accent chip each. Strengths and weaknesses are the highest and lowest performing real format and pillar combinations, cited with numbers. Opportunities are proven demand not yet captured. Threats are patterns that will cap growth if unchanged. Every cell cites real data. Never reference pinned posts.

**6b. Ranked fixes**
Rank fixes by leverage over effort. Lead with the fastest high-impact fix (a framing or content change, never pinning). Each fix names what is failing with evidence, what proven pattern to borrow, and one concrete test video.

---

### TAB 07: WEEKLY DIAGNOSTIC

Each framework gets a small info button with a plain popup.

**7a. VVA check (Visual, Verbal, Auditory)**
Three rows with verdict chips. Visual = set, framing, props. Verbal = whether the opening line carries a stake or a number. Auditory = clean audio and a spoken hook in the first second.
Info popup: "VVA checks your video works three ways. Visual is what the viewer sees. Verbal is the words, especially the first line. Auditory is whether the audio is clean and whether the hook lands when someone is not looking at the screen."

**7b. Hook layering**
For the last several videos, mark each with a check or cross for whether visual, text, and audio hooks all fire in the first 3 seconds. Show real views per video.

**7c. Fluff diagnostic**
Specific weak openings, slow middles, and filler lines from real videos. Each with a short "cut this" instruction.

**7d. Next session checklist**
Five concrete items from the diagnostics. Render each checkbox as a drawn CSS square, never a text character.

---

### TAB 08: SCRIPTS AND CALENDAR

**8a. Scripts**
2 to 3 scripts. Each picks a real winning video as the source, preserves its exact mechanic (structure, beat sequence, pacing, CTA style), and changes only the topic to a gap from the Growth Plan. Show the linked source. Label each beat with which source beat it mirrors. Include hook, full body, CTA, and on-screen text suggestions.

**8b. Weekly plan**
Five day cards, not a bare table. Each names the day, topic, pillar, and funnel stage. Explains in plain words what job that post does, why it sits on that day, and how to shoot it. Put the biggest reach bet on the creator's strongest posting day. Every topic traces to a real finding.

---

## STEP 4 - AFTER DELIVERY

Offer to write more scripts based on the findings, or to run a competitor comparison. Do not offer to save a Brand Voice. That is a separate skill the user can run on its own.

---

## LAYOUT AND HTML RULES

Produce ONE self-contained HTML file. No external JS libraries or frameworks. The goal is a report that looks like a paid agency deliverable.

**Layout:** Two-column app. Fixed dark left rail with tab navigation on the left. Wide content page on the right. Dark cover banner at the top. One tab panel visible at a time, switching on click with no page reload.

**Design tokens (in :root):**
--ink:#0F1210, --paper:#FAF7F0, --paper-dim:#F1ECE0, --signal:#B8FF3C, --signal-deep:#4A6B0E, --gray:#6B6459, --line:#E4DFD3, --white:#FFFFFF, --do-bg:#E7F5CE, --do-text:#3F6B0E, --dont-bg:#F3E3DD, --dont-text:#8C3E22, --alert-bg:#FBEFD2, --alert-text:#7A5A0A, --blue:#4A6B8A, --tan:#8B8567.

**Fonts (Google Fonts):** Fraunces 400/500/600 for headings and big numbers. Inter 400/500/600 for body copy and tab labels. IBM Plex Mono 400/500 for data labels, captions, and axis text. No italics anywhere.

**Rail:** Sticky, full height, dark background, right hairline border. Top to bottom: "Meedro" in Fraunces, creator handle, "Sections" label, tab buttons (two-digit number then UPPERCASE name), footer ("N analyzed videos / Prepared [date]"). Active tab: --signal background, dark text. Inactive: light text on dark.

**Cover:** Dark banner. Mono eyebrow "Meedro content audit / confidential". H1 in Fraunces: "The complete audit of [handle]" with handle in --signal. One plain summary line. Meta row: Account, Niche, Videos analyzed.

**Charts:** All inline SVG, no libraries. Trend chart dots: data-url, data-topic, data-stat attributes. On hover: small dark tooltip near cursor with full topic and stat, flips side near edges. On click: window.open the real video. Use a positioned HTML div for the tooltip, not SVG title tags.

**Info popups:** One modal overlay, swapped by key. Triggered by small round "i" buttons on scorecard headings. Close on X, overlay click, and Escape key.

**Hard rules (verify before delivering):**
- Zero em dashes or en dashes anywhere. Count must be zero.
- No italics anywhere.
- Every video link is real, never href="#".
- Checklist boxes are drawn CSS squares, never text characters.
- Balanced markup. File closes with </html>.
- Rail order and numbering match all eight tabs exactly.
