---
name: competitor-analysis
description: The full competitive audit. Ranks every tracked competitor by reach per 1,000 followers, decodes what is working in the niche from verified transcripts, flags bought reach, reads trial reels before they publish, names the openings nobody has taken, and ends on six videos the creator can shoot. MUST be used for "analyze my competitors", "competitor analysis", "competitive audit", "who is beating me", "what are my competitors doing", "where is my opening", "who is winning in my niche", "how do I stand out". Quotes any analysis cost in chat before spending. Free on already-analyzed data.
---


# Competitor Analysis Skill

Everything needed is in this file. Read the engine rules first, then the playbook.

---

## TOOLS (MeedroAI only - never substitute tools from other connectors)

| Tool | Cost | What it returns |
|---|---|---|
| my_info | Free | Creator handle, niche, follower count, saved Brand Voice |
| list_watchlist | Free | All watchlists and their member counts |
| watchlist_videos sort='outlier' filter='all' | Free | All competitor videos with full breakdowns. Page with offset until coverage is complete. READ THE COVERAGE BLOCK before any absence claim |
| creator_info | Free | Per-competitor stat card: followers, following, posts, bio, profile link, typical posting time. Use this for the comparison table, NOT analyze_profile |
| get_creator_videos type='trial' | Free | Instagram Trial Reels per competitor. Requires watchlist membership |
| get_creator_videos analyzed=true | Free | Only the already-analyzed videos for one creator. Use this to check what is stored before spending anything |
| search_account | Free | Find accounts by SINGLE keyword. Accepts minFollowers for tier searches |
| search_viral_videos | Free | Niche-wide video summaries. Returns stats and metadata only, no transcript. SINGLE keywords only |
| add_to_watchlist | Free | Add a competitor to the watchlist. Does NOT analyze them |
| get_video_analysis | Free if already requested before. 5 credits first time | Full stored breakdown including transcript |
| analyze_profile | 50 credits if new to Meedro. Free if already on Meedro servers | Use ONLY when a competitor has never been analyzed and has zero stored videos. Never call it to get stats, creator_info is free and sufficient |
| analyze_video | 5 credits per not-yet-analyzed video | Only called after explicit user yes through the credit gate |

**Money rule:** Before any paid batch, state the exact total cost and the exact balance in chat and wait for a clear yes. A question is not consent. Silence is not consent. Never spend silently. Never re-analyze a row already marked Analyzed. Never mention credits anywhere on the report page.

---

## STEP 0 - PREFLIGHT (run before building anything)

Call my_info, list_watchlist, and one page of watchlist_videos on the candidate list. Then check every line below.

Show a READINESS CHECK in chat in this exact format before asking anything:

```
READINESS CHECK
Connected account:   @handle, [N] followers
Saved profile:       [found with N pillars / not found]
Competitor set:      [N] on "[watchlist name]"
Tier spread:         [N] accounts at or above your size
Analyzed videos:     [N] in window, [N] with usable hooks
Concentration:       top account holds [N]%
Trial reels:         [N] of [N] accounts have tests
```

Judge each line against these thresholds and ask only the questions the failures require, in one message:

**No connected account (HARD FAIL)**
"I do not see a connected account, so there is nothing to measure the field against. Connect your Instagram or TikTok in settings and I will run this. Want a niche-only version in the meantime? It shows who is winning but cannot tell you where you sit."

**Fewer than 3 competitors (HARD FAIL)**
"You have [N] competitors tracked and I need at least 3 for this to mean anything. Give me their handles, or tell me 2 or 3 words for your niche and I will find candidates and show their real follower counts before adding anyone."
Then: search_account with SINGLE keywords, propose real accounts with real follower counts. Add only the ones the user confirms. Never pick competitors silently.

**Multiple watchlists match**
"You have more than one list this could be built from: [names with counts]. Which one?" Note if strong candidates sit on other lists and are missing from the chosen one.

**All accounts smaller than the creator**
"Every account you track is smaller than you, so every comparison will flatter you. Want me to find accounts at or above your size first?" On yes: search_account with minFollowers above the creator's count. Propose 2 to 3 with real follower counts and efficiency estimates. Label any unverified suggestion clearly.

**No saved profile (SOFT)**
"I do not have your saved profile, so I can compare accounts but cannot tell you which formats fit you or where your gap is. Two options: run the Content Audit first and this report gets sharper. Or continue now and I will leave your side of the comparison out rather than guess it."

**Not enough analyzed videos or too lopsided (HARD for tabs 02 and 03) - THE CREDIT GATE**

This fires on either:
- VOLUME: fewer than 8 analyzed rows in the last 6 months, or fewer than 2 accounts represented
- SPREAD: enough rows but one account holds more than 40% of them

Select videos to fix this: highest outlier first, inside the 6-month window, not already analyzed. On a spread failure, take only from under-represented accounts. Cap at 12 videos total.

Say in chat (never on the report page):

On VOLUME: "Right now [N] of your competitors' videos are analyzed inside the six month window. I need about 8 for the mechanics and steal sections to mean anything.

On SPREAD: "You have [N] analyzed videos in the window. The problem is [X] of them, [Y]%, belong to @[handle]. Built on that, the mechanics section describes one creator, not your field.

Here is the full cost breakdown before I spend anything:

Videos to analyze (5 credits each, only for not-yet-analyzed videos):
1. @handle   24.1x   2026-05-12   [link]
2. @handle   18.6x   2026-03-10   [link]
...

Competitors with no stored videos at all (50 credits each to run first analysis):
- @handle (never analyzed, no stored data)
...

Total: [grand total] credits
Your balance: [balance], leaving [balance minus total] after.

Reply yes to run all of them. Or give me a smaller number and I will take the top ones by outlier score. Or say skip and I will build on what is already there, with the thin sections clearly marked."

**If the balance cannot cover the full batch:** offer only what the balance affords. Never ask for more than the balance.

**No trial reels anywhere:** skip Tab 04 entirely, renumber remaining tabs, and note once in the report that nobody in this field is testing before publishing, which is itself an opening.

Once all hard checks pass, say in one line what the report will and will not contain, then build without further questions.

---

## STEP 1 - PULL THE DATA (silent)

Page watchlist_videos until coverage is complete. Read the coverage block on every page. A creator absent from one page has not stopped posting. Never claim absence without full pagination.

Pull creator_info per competitor for the stat card: followers, following, and post count. This is free. Use these numbers combined with median views from watchlist_videos to compute reach per 1,000 followers and fill the comparison table. Do NOT call analyze_profile just to get stats.

Pull watchlist_videos sort='outlier' filter='all' and page until coverage is complete. This gives all stored videos with full breakdowns. A creator absent from one page has not stopped posting. Never claim absence without full pagination.

Pull get_creator_videos type='trial' per competitor for Tab 04. Free, requires watchlist membership.

Pull search_viral_videos on single keywords for niche-wide context beyond the tracked set.

If a competitor shows "Not analyzed yet" in the coverage block (zero stored videos): this means they have never been analyzed. Call get_creator_videos analyzed=false first to confirm nothing is stored. If truly empty, include them in the credit gate: analyze_profile costs 50 credits if they are new to Meedro, and the user must say yes before calling it.

Compute in code before building: each account's median outlier, median views, median engagement rate, and reach per 1,000 followers using the follower count from creator_info and median views from watchlist_videos.

For every hook used anywhere in the report: use the stored hook field if it reads as a real spoken opening line. If it looks like a caption, a CTA, a hashtag line, or does not read as something said out loud at the start of a video, silently verify against the transcript and replace it with the first spoken line. Never mention this on the page.

Pull get_creator_videos type='trial' per competitor for Tab 04.

Pull search_viral_videos on single keywords for niche-wide context beyond the tracked set.

Compute in code before building: each account's median outlier, median views, median engagement rate, and reach per 1,000 followers.

---

## STEP 2 - THE REPORT (six tabs in this exact order)

**Five rules that apply everywhere and never appear in the report:**
1. Hook autocorrect (silent): for every hook used anywhere in the report, use the stored hook field if it reads as a real spoken opening line. If it looks like a caption, a CTA, a hashtag line, or does not read as something said out loud at the start of a video, silently verify against the transcript and replace it with the first spoken line. Never mention this on the page.
2. No credits mention anywhere on the page.
3. No tool names or product names on the page.
4. No pinned post claims. The field is unreliable.
5. No visual field claims. Read structure from transcripts only.

The creator's own handle is never inside a competitor list. It appears only as a labeled baseline, visually separated.

Every section has a PURPOSE (written into the intro in plain words) and a BUILD (how to compute it). Every claim links a source video. If a section cannot be backed by real data, say so plainly rather than inventing it.

---

### TAB 01: THE FIELD

**Order:** executive summary (written last), the roster, reach efficiency chart, full comparison table, closing action block.

**Executive summary (write last)**
One plain verdict line stating who is actually beating the creator and on what measure. Three cells: who beats them and how (real numbers), what they are doing that the creator is not (clearest difference with evidence), and the one opening worth taking (single move, real number, short reason). Each cell links a real video.

**The roster**
One card per competitor inside an explicit grid container (4 columns above 1000px, 3 to 560px, 2 below, minmax(0,1fr)). Ranked by reach per 1,000 followers, not follower count. Each card: avatar with two-letter initial fallback on image error, handle linked to real profile, name, rank number, status chip, followers, median reach, reach per 1k, best ever multiplier, linked best video. The creator's card sits above the ranked grid, labeled "Your baseline", not numbered, not inside the competitor list.

**Reach efficiency chart**
Horizontal SVG bars, median views per 1,000 followers, descending, creator's value as a labeled dashed reference line. Define the metric in one plain sentence. At most two callouts: the most efficient account and the least, with the real contrast in numbers.

**Full comparison table**
All rivals ranked by efficiency, creator's row highlighted as the baseline. Columns: account, followers, posts, median reach, reach per 1k, best ever, median engagement, posts per week. Every cell is a computed real value. Where a value cannot be computed, write "not available" and say why. Every account name links to the real profile.

**Closing action block (green pair):** short plain instruction on what to do with this information.

---

### TAB 02: HOW THEY GO VIRAL

**Order:** mechanic performance chart, mechanic cards, bought reach flag, field over time timeline, closing action block.

**Mechanic performance chart**
Group every verified hook by its opening move, not by topic. Per mechanic: reels count spanning distinct accounts, median outlier. Vertical SVG bars, values above, "reels=N" beneath, dashed field median line. Early signal mechanics in a lighter fill.

**Mechanic cards**
One card per mechanic, ordered by median outlier. Each: the move in one short paragraph, why it travels in one short paragraph, the shape with the topic removed as a fill-in line, and the real videos as linked cards showing outlier and views. One account means a signature. Two or more separate accounts means a field pattern. Say which.

**Bought reach flag**
Split every rival's window using: partnership language in the caption, OR engagement rate below 30% of that account's own median. Report both group medians. Flag videos stay visible and ranked, struck through with a one-line reason and the account's own median beside it. If nothing trips the flag, say the window is clean.

**Field over time (interactive)**
Interactive SVG timeline. Every breakout in the 6-month window. x = time with month labels. y = outlier on a log axis when one video dominates. Dashed field median. Color dots by band: pink (#E84393) 3x or more, green (#2ECC71) 1.5x to 3x, grey (#9A968A) below. Three-item legend. Hover: full hook and handle. Click: opens the real video.

**Closing action block (green pair).**

---

### TAB 03: FLOPS

Recent posts that landed below that account's own baseline, never below the creator's. State the comparison in one line. Rank by how far below baseline. Show verified hook, handle, real views, and multiplier, each row linking to the real video. Read the pattern across them in one or two lines. If no pattern connects them, say so.

**Closing action block (green pair).**

---

### TAB 04: TRIAL PIPELINE (skip entirely and renumber if no trials exist)

Open with a short plain explanation of what trial reels are and how to read them, attached to an info popup. One block per competitor with trials: their test count, public baseline, what they appear to be testing, their 4 strongest tests as linked cards showing multiplier, views, and test date, and the real distribution of how tests landed. Close on the hit rate across the field.

If an account has no trials, one line saying no tests were found. That is a finding.

**Closing action block (green pair).**

---

### TAB 05: THE GAP

Exactly 3 gaps, fewer if the evidence supports fewer. A gap is only allowed if it can point at evidence: a format proven in the field but absent from the creator's account, a mechanic only used at scales far below theirs, a shape their own record proves they are good at, or demand visible in an adjacent niche. Each gap: the claim, the evidence in one short paragraph with real numbers from both sides, and linked proof chips. Cut any gap that cannot link its proof.

The gap names the opening. It does not prescribe the video. Each closing line either points at the steal card that executes it, or describes the positioning commitment if it is not a video. No duplicate instructions between the gap and the steal list.

No closing action block. The steal list is the action.

---

### TAB 06: THE STEAL LIST

5 or 6 cards ranked by how well the mechanic transfers to the creator, not by raw score. Exclude bought reach. Exclude anything older than 6 months. Each card: the mechanic name, source account with real outlier and views, the verified opening line in Fraunces regular with a left rule, the shape with the topic removed, why it travels in one short paragraph, and the creator's version naming which of their own proven formats it rides on with that format's real number.

End on ONE card named as the one to shoot first and why, citing the real number behind it.

No closing action block. This is the last thing the creator reads.

---

## CLOSE

End on one concrete move. Name which gap to take first and why, citing the real number. Offer to script the first card, or to add the proposed tier-above accounts from Tab 01.

---

## LAYOUT AND HTML RULES

Produce ONE self-contained HTML file. No external JS libraries. Premium agency quality.

**Layout:** Two-column app. Fixed dark left rail on the left. Wide content page on the right. Dark cover banner. One tab panel visible at a time.

**Design tokens (in :root):**
--ink:#0F1210, --paper:#FAF7F0, --paper-dim:#F1ECE0, --signal:#B8FF3C, --signal-deep:#4A6B0E, --gray:#6B6459, --line:#E4DFD3, --white:#FFFFFF, --do-bg:#E7F5CE, --do-text:#3F6B0E, --dont-bg:#F3E3DD, --dont-text:#8C3E22, --alert-bg:#FBEFD2, --alert-text:#7A5A0A, --blue:#4A6B8A, --tan:#8B8567.

**Fonts (Google Fonts):** Fraunces 400/500/600 for headings, big numbers, and quoted hooks. Inter 400/500/600 for body copy and tab labels. IBM Plex Mono 400/500 for data labels, captions, handles, and axis text. No italics anywhere, including quoted hooks. Set hooks in Fraunces regular with a left rule, not italic.

**Rail:** Sticky, full height, dark background. Top to bottom: brand word in Fraunces, creator handle, "Sections" label, tab buttons (two-digit number then UPPERCASE name), footer ("N rivals profiled / N videos read / Prepared [date]"). Active tab: --signal background, dark text. Inactive: light text on dark.

**Cover:** Dark banner. Mono eyebrow. H1 in Fraunces stating the single most important finding, key phrase in --signal. One plain summary line. Meta row: Niche, Rivals profiled, Videos read, Window.

**Rival card grid:** Explicit grid-template-columns with counts and breakpoints. 4 columns above 1000px, 3 down to 560px, 2 below. Every track minmax(0,1fr). Truncate long text with ellipsis. Never auto-fill with a large minimum.

**Charts:** All inline SVG, no libraries. Trend dots: data-url, data-topic, data-stat attributes. HTML tooltip div (not SVG title). Click opens the real video. Every bar chart has plain axis labels and values above bars.

**Info popups:** Four terms get info buttons: outlier score, reach per 1,000 followers, trial reels, bought reach. One modal overlay, swapped by key. Close on X, overlay click, and Escape.

**Hard rules (verify before delivering):**
- Zero em dashes or en dashes anywhere. Count must be zero.
- No italics anywhere.
- Every video link is real, never href="#".
- Every competitor name links to their real profile.
- Creator handle appears zero times inside any competitor list.
- Balanced markup. File closes with </html>.
- Rail order and numbering match the active tab count exactly (5 or 6 depending on trial reels).
