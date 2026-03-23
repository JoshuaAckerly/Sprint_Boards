# Sprint Board (Execution View) — ARCHIVED

Use this as your weekly operating board for the 7-site portfolio.
Recommended WIP limit: **max 2 active build sites**.

> **Archive Note:** This sprint is complete. Active board: `SPRINT_BOARD_NEXT_2026-04-06.md`.

## Current Sprint

- **Sprint Window:** 2026-03-30 → 2026-04-03
- **Primary Site:** lunarblood
- **Secondary Site:** hollowpress
- **Maintenance Sites:** graveyardjokes, synthveil, thevelvetpulse, velvetradio
- **R&D Site:** studio
- **Sprint Goal:** Ship one lunarblood UX quality improvement, one hollowpress listing stability outcome, and one portfolio-ops reliability checkpoint with validation evidence.
- **Execution Mode:** AI-assisted micro-sprints (target 4-8h cards; split any card that exceeds 1 day; every AI-generated change requires human validation evidence).

## Weekly Workload Summary

- **Locked Workload:** 22h (4 cards)
- **Delivered Workload:** 44h (8 cards — 4 locked + 4 bonus from proposed April 6 queue)
- **Variance:** +22h

## Done (This Sprint)

### Committed Cards (4/4)

- [x] **Card: lunarblood — Dashboard search UX follow-up (saved queries + keyboard refinement)**
  - Outcome: added session-based recent search persistence (merged with localStorage), arrow-key result navigation with visual highlight, Enter-to-open, Escape-to-clear, and fixed MySQL/PHP timezone mismatch in upcoming-show ordering.
  - Validation: `./vendor/bin/phpunit tests/Feature/DashboardSearchTest.php` (11 passed, 35 assertions), `npm run -s types`, `npm run -s build`.
  - Paths: `lunarblood/app/Http/Controllers/DashboardController.php`, `lunarblood/resources/js/pages/dashboard.tsx`, `lunarblood/tests/Feature/DashboardSearchTest.php`.

- [x] **Card: hollowpress — Listing index rollout phase 1 (safe migrations)**
  - Outcome: confirmed all 4 recommended indexes from checkpoint are applied — `posts(author_type, created_at)`, `posts(author_name)`, `case_studies(project_type, project_date, created_at)`, `case_studies(client_name)` — plus matching `demo_posts` indexes. Migration has proper rollback.
  - Validation: `./vendor/bin/phpunit tests/Feature/SearchRelevanceTest.php` (9 passed, 33 assertions), `npm run -s build`, `php artisan migrate:status`.
  - Paths: `hollowpress/database/migrations/2026_03_10_011500_add_listing_query_indexes.php`.

- [x] **Card: Portfolio Ops — Cross-site perf checkpoint refresh**
  - Outcome: captured cold-start + warm-path timing for all 7 portfolio sites. No sustained P95 degradation detected. velvetradio flagged WARN (578ms P95), subsequently resolved to 30ms after production fix (March 21). Database health clean (0 slow queries).
  - Validation: `bash ./scripts/portfolio-monitoring.sh true` (two passes), `bash ./scripts/monitoring-history-summary.sh 30`.
  - Paths: `docs/reports/2026-03/CROSS_SITE_PERF_CHECKPOINT_2026-03-20.md`, `monitoring-history/portfolio-monitoring-history.csv`.

- [x] **Card: Portfolio Ops — Sprint board hygiene + archive rollover**
  - Outcome: archived 03/23→03/27 sprint board with validation report links. Seeded `SPRINT_BOARD_NEXT_2026-04-06.md` with 4 locked cards (2 lunarblood UX, 1 hollowpress feature, 1 ops) and proposed 04/13 queue.
  - Validation: `SPRINT_BOARD_ARCHIVE_2026-03-23_TO_2026-03-27.md` created, `SPRINT_BOARD_NEXT_2026-04-06.md` seeded with acceptance criteria + validation commands + rollback notes.
  - Paths: `Sprint_Boards/SPRINT_BOARD_ARCHIVE_2026-03-23_TO_2026-03-27.md`, `Sprint_Boards/SPRINT_BOARD_NEXT_2026-04-06.md`.

### Bonus Cards (4/4 — pulled forward from proposed April 6 queue)

- [x] **Card: lunarblood — Show detail page UX polish (mobile layout + status badge refinement)**
  - Outcome: created shared StatusBadge component using CSS theme variables, responsive mobile layout (flex-col stacking, responsive text sizes), updated show index and dashboard to use StatusBadge for consistent visual language.
  - Validation: `./vendor/bin/phpunit tests/Feature/DashboardSearchTest.php` (11 passed), `npx tsc --noEmit`, `npm run -s build`.
  - Paths: `lunarblood/resources/js/components/StatusBadge.tsx`, `lunarblood/resources/js/pages/shows/show.tsx`, `lunarblood/resources/js/pages/shows/index.tsx`, `lunarblood/resources/js/pages/dashboard.tsx`.

- [x] **Card: hollowpress — Search query performance phase 2 (full-text search evaluation)**
  - Outcome: benchmarked LIKE vs MySQL FULLTEXT across 332 posts and 100 case studies. FULLTEXT is 2–5× faster but both sub-5ms. FULLTEXT has recall regressions (misses substring matches, changes multi-word semantics). **Verdict: NOT RECOMMENDED** at current scale — re-evaluate at 5,000+ rows.
  - Validation: `npx tsc --noEmit`, `npm run -s build`. Tests 9/9 prior validation.
  - Paths: no code changes (evaluation-only card). Report: `docs/reports/2026-03/HOLLOWPRESS_FULLTEXT_SEARCH_EVAL_2026-03-21.md`.

- [x] **Card: Portfolio Ops — velvetradio P95 investigation**
  - Outcome: root cause identified as database-backed session/cache driver + SSR port misconfiguration. Fixed session/cache to `file` driver, aligned SSR port to 13718, fixed cartesian product in `/shows` query. P95 dropped from 578ms → 28ms (20× improvement). Confirmed sustained (30ms warm-path, March 21).
  - Validation: 10/10 tests passing (43 assertions), `npx tsc --noEmit`, `npm run -s build`.
  - Paths: `velvetradio/.env`, `velvetradio/resources/js/ssr.tsx`, `velvetradio/routes/web.php`. Report: `docs/reports/2026-03/VELVETRADIO_P95_INVESTIGATION_2026-03-21.md`.

- [x] **Card: Portfolio Ops — Monthly dependency audit**
  - Outcome: found 2 medium CVEs in league/commonmark 2.8.0 (all 8 repos) and 1 high CVE in rollup 4.55.3 (auth-system dev dep only). All remediated: commonmark → 2.8.2, rollup → 4.58.1+. All repos now show 0 advisories / 0 vulnerabilities.
  - Validation: `composer audit` (×8), `npm audit` (×8) — all clean.
  - Paths: `composer.lock` (all 8 repos), `auth-system/package-lock.json`. Report: `docs/reports/2026-03/DEPENDENCY_AUDIT_2026-03-21.md`.

## Friday Exit Criteria (2026-04-03)

- [x] 1 lunarblood card shipped with validation evidence
- [x] 1 hollowpress card shipped with validation evidence
- [x] cross-site perf checkpoint published with trend analysis
- [x] board archived and next sprint candidate queue seeded

## Next Sprint

Promoted to `SPRINT_BOARD_NEXT_2026-04-06.md`. See that board for locked queue and proposed 04/13 follow-up.
