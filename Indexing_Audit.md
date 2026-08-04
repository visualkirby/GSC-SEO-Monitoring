# Indexing Audit

A real Google Search Console indexing review for benchlineanalytics.com, run 2026-07-29. The goal: don't assume "not indexed" means broken -- classify every excluded URL by its actual reason, fix what's real, leave what's correct behavior alone, and push Google to (re)crawl what's genuinely missing.

---

## Starting State

- Sitemap `/page-sitemap.xml` submitted 2026-07-16, 8 pages listed, last successfully read 2026-07-27.
- Indexing status at audit time: **5 indexed, 8 not indexed.**

An earlier open item had assumed `wp-sitemap.xml` (WordPress's default sitemap path) needed submitting. It didn't -- Yoast SEO's sitemap was already live and successful under a different filename (`/page-sitemap.xml`). That stale assumption was closed out, not acted on.

---

## Classifying the 8 "Not Indexed" URLs

Rather than treat "not indexed" as one problem, each excluded URL was checked individually in GSC and sorted by real cause:

| Reason | Count | Verdict |
|---|---|---|
| Blocked by `robots.txt` (`/wp-admin/*`) | -- | **Correct, expected.** WordPress admin routes should never be indexed. Not a bug. |
| `?page_id=175` query-string redirect | 1 | **Benign.** WordPress's own auto-redirect behavior, not a real page. |
| Discovered via sitemap, never crawled at all | 3 | **Real gap.** `/products/career-engine/`, `/products/freelanceflow/`, `/products/progress-dash/` -- all three showed "Referring page: None detected," meaning Google had the URLs from the sitemap but had never actually visited them. |
| Crawled but not indexed | 1 | **Correct, expected.** `/hello-world/`, WordPress's default placeholder post -- Google correctly deprioritized it as thin/default content. (Since permanently deleted from the site itself.) |
| Real 404s | 2 | **Confirmed dead links**, addressed separately (see below). |

The 3 real gaps -- product pages that existed, were in the sitemap, but Google had never crawled -- were the only genuine indexing problem in the batch.

---

## Fix: Priority Crawl Requests

Used Search Console's URL Inspection tool to manually request indexing for all 3 never-crawled product pages:

- `/products/career-engine/`
- `/products/freelanceflow/`
- `/products/progress-dash/`

All three confirmed **"Indexing requested"** and added to Google's priority crawl queue.

## Fix: Dead Links Cleanup

The 2 real 404s traced back to the site's own footer navigation linking to `/steadmark` and `/vitalmetrics` -- pages that were removed from the build but never unlinked. Both dead links removed from the footer; FreelanceFlow (a real, live page) added to both nav menus in their place.

---

## What's Left

Re-crawling is on Google's own timeline, not something a priority-crawl request forces immediately. The next real check is a follow-up GSC pull to confirm the 3 requested pages moved from "not indexed" to "indexed" -- not yet done as of this audit.
