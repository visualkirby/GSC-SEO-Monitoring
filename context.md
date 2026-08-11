# gsc-seo-monitoring - Session Log

Repo: `D:\Documents\Github\gsc-seo-monitoring` (private), pushed to `visualkirby/gsc-seo-monitoring`
Purpose: portfolio piece documenting the Google Search Console indexing audit-and-fix cycle for benchlineanalytics.com, per `Google_Tools_Portfolio_Plan_2026-07-16.docx` Section 1.5

---

## Session: 2026-08-10 (backfilled -- repo predates this file)

**Discovered mid-session that this repo already existed, complete, from a prior untracked session** (real audit dated 2026-07-29, repo initialized 2026-08-04) -- no `context.md` had ever been created for it, so it fell out of tracking entirely. Backfilling this file now to close that gap.

**Existing content (as of 08-04 initialization):** `README.md` + `Indexing_Audit.md` document a full real audit -- starting state (5 indexed, 8 not indexed), every excluded URL individually classified by real cause (robots.txt blocks, benign redirects, deprioritized thin content, dead links, genuinely-never-crawled), 3 priority crawl requests submitted for real product pages, 2 dead footer links found and fixed. `screenshots/` was empty until today.

**Added today:** first "Weekly Tracking" pass -- 3 real screenshots (Overview, Performance, Indexing) added to `screenshots/`, and a new **Weekly Tracking** table added to `README.md`, deliberately separate from the case-study narrative above it. Real numbers logged: 7 indexed / 11 not indexed, 2 total clicks / 86 impressions (3-month), avg. position 17.2. Per Sawandi's explicit direction: "all the ups and downs should be a part of these repos" -- this table exists to show real fluctuation over time, not just a flattering before/after.

Scrub policy per the plan doc: **no scrubbing needed** for this repo -- domain, click/impression numbers, and indexing status aren't sensitive the way GA4/GTM property/container IDs are.

### What Is Next
- Continue the Weekly Tracking table on the planned weekly cadence (see the new `google-tools-weekly` skill)
- No other known gaps

## Session: 2026-08-10 (2) -- 2 real indexing gaps fixed same day

Same session as above, after Sawandi asked to "fix some of the errors in search console." Drilled into each "Not indexed" reason via the Pages report:

- **`/products/freelanceflow/` and `/get-the-checklist/`**: both real, in the current sitemap, "Referring page: None detected" -- genuinely never crawled. Requested priority indexing for both via URL Inspection, confirmed "Indexing requested" for each.
- **4 "Page with redirect" flags**: all `?page_id=N` WordPress query-string auto-redirects -- confirmed benign, matches the exact pattern the 07-29 audit already established, no action needed.
- **2 stale 404s (`?page_id=89`, `/steadmark`)**: not linked from the current sitemap or homepage -- these are old crawl data Google is still holding onto, not live dead links on the site today. `/steadmark`'s 404 specifically was already confirmed intentional by Sawandi in a separate 2026-07-18 session (see `benchline-theme/context.md`), unrelated to today. No site-side fix needed; Google will drop these naturally on recrawl.
- **`robots.txt` block confirmed** as just `/wp-admin/*` -- expected, no action.
- **"Crawled - not indexed" (`/shop/`, `/hello-world/`)**: expected thin-content exclusions, `/hello-world/` entry is stale cached data from before its 07-29 deletion.

Not yet reflected in the README's Weekly Tracking table (that captured the numbers *before* these fixes) -- next weekly run should show the real effect of the 2 priority-crawl requests once Google processes them.

### What Is Next
- Watch next week's indexing numbers for whether the 2 priority-crawled pages actually get indexed
- No other known gaps
