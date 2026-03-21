# Sprint Board (Execution View)

Use this as your weekly operating board for the 7-site portfolio.
Recommended WIP limit: **max 2 active build sites**.

## Current Sprint

- **Sprint Window:** 2026-03-30 → 2026-04-03
- **Primary Site:** lunarblood
- **Secondary Site:** hollowpress
- **Maintenance Sites:** graveyardjokes, synthveil, thevelvetpulse, velvetradio
- **R&D Site:** studio
- **Sprint Goal:** Ship one lunarblood UX quality improvement, one hollowpress listing stability outcome, and one portfolio-ops reliability checkpoint with validation evidence.
- **Execution Mode:** AI-assisted micro-sprints (target 4-8h cards; split any card that exceeds 1 day; every AI-generated change requires human validation evidence).

## Today Snapshot

- **Last Updated:** 2026-03-21
- **Status:** 🟢 All sprint commitments complete. Two proposed next-sprint cards also completed early.
- **Carryover Posture:** Continue evidence-first ops discipline; monitor velvetradio P95 trend from checkpoint.
- **Open Risks:** dependency regressions during updates, velvetradio P95 elevated (578ms — WARN), cold-start outliers inflating monitoring averages.
- **Kickoff Gate:** sprint starts only if each `Now` card has acceptance criteria + validation commands + rollback note.

## Locked Queue (Sprint Start)

- [ ] **Card (6h): lunarblood — Dashboard search UX follow-up (saved queries + keyboard refinement)**
  - Owner: Joshua
  - Acceptance:
    - [ ] preserve recent dashboard search queries for authenticated user sessions
    - [ ] improve keyboard flow for search submit + result navigation
    - [ ] maintain existing synonym and validation behavior
  - Validation: `./vendor/bin/phpunit tests/Feature/DashboardSearchTest.php`, `npm run -s types`, `npm run -s build`
  - Rollback: revert `DashboardController.php` and `dashboard.tsx` changes; remove new test methods from `DashboardSearchTest.php`
  - Note: **Completed early (2026-03-20)** — session-based recent search persistence, arrow-key/Escape/Enter keyboard navigation, and MySQL CURRENT_DATE timezone fix all shipped with 11/11 tests passing.

- [ ] **Card (6h): hollowpress — Listing index rollout phase 1 (safe migrations)**
  - Owner: Joshua
  - Acceptance:
    - [ ] add first-pass indexes from checkpoint recommendations with rollback-safe migration
    - [ ] confirm `/posts` and `/case-studies` behavior unchanged after migration
    - [ ] document before/after timing delta note in March report addendum
  - Validation: `php artisan migrate --pretend`, `./vendor/bin/phpunit tests/Feature/SearchRelevanceTest.php`, `npm run -s build`
  - Rollback: `php artisan migrate:rollback --step=1` (migration has proper `down()` method)
  - Note: **Completed prior sprint** — migration `2026_03_10_011500_add_listing_query_indexes.php` already applied with all 4 recommended indexes. 9/9 tests pass, build clean.

- [ ] **Card (4h): Portfolio Ops — Cross-site perf checkpoint refresh**
  - Owner: Joshua
  - Acceptance:
    - [ ] rerun lightweight endpoint timing snapshot on active + maintenance sites
    - [ ] flag any endpoint with sustained p95 degradation trend
    - [ ] publish checkpoint note under `docs/reports/2026-03/`
  - Validation: portfolio monitoring script run + report update
  - Rollback: N/A (read-only monitoring)
  - Note: **Completed early (2026-03-20)** — warm-path P95 all OK except velvetradio WARN (578ms). Report at `docs/reports/2026-03/CROSS_SITE_PERF_CHECKPOINT_2026-03-20.md`.

- [ ] **Card (4h): Portfolio Ops — Sprint board hygiene + archive rollover**
  - Owner: Joshua
  - Acceptance:
    - [ ] archive completed board with links to all validation reports
    - [ ] seed next `SPRINT_BOARD_NEXT` draft with locked queue and risks
    - [ ] ensure exit criteria and owners are present before kickoff
  - Validation: board consistency review in `Sprint_Boards` repo

## Lane: Now (This Sprint Commitments)

RAG legend: `🟢 On track` | `🟠 At risk` | `🔴 Blocked`

### lunarblood (Primary) - Target: 1 shipped outcome
- [x] **Card (6h): Dashboard search UX follow-up (saved queries + keyboard refinement)**
  - Status: ✅ Completed (shipped early 2026-03-20)
  - Owner: Joshua

### hollowpress (Secondary) - Target: 1 shipped outcome
- [x] **Card (6h): Listing index rollout phase 1 (safe migrations)**
  - Status: ✅ Completed (shipped prior sprint, confirmed 2026-03-20)
  - Owner: Joshua

### Portfolio-wide Ops - Target: 2 reliability outcomes
- [x] **Card (4h): Cross-site perf checkpoint refresh**
  - Status: ✅ Completed (shipped early 2026-03-20)
  - Owner: Joshua

- [ ] **Card (4h): Sprint board hygiene + archive rollover**
  - Status: 🟢 On track
  - Owner: Joshua

## Blocked

- [ ] **Card: Deploy contention during parallel service restarts**
  - Status: 🟢 Mitigation in place, monitor only
  - Owner: Joshua
  - Mitigation: use batched deploy flow and restart sequencing where needed.

- [ ] **Card: Dependency updates introduce regressions**
  - Status: 🟢 Mitigation in place, monitor only
  - Owner: Joshua
  - Mitigation: follow `docs/standards/DEPENDENCY_UPDATE_PROTOCOL.md`.

## Done (This Sprint)

- [x] **Card: lunarblood — Dashboard search UX follow-up (saved queries + keyboard refinement)**
  - Outcome: added session-based recent search persistence (merged with localStorage), arrow-key result navigation with visual highlight, Enter-to-open, Escape-to-clear, and fixed MySQL/PHP timezone mismatch in upcoming-show ordering.
  - Validation: `./vendor/bin/phpunit tests/Feature/DashboardSearchTest.php` (11 passed, 35 assertions), `npm run -s types`, `npm run -s build`.
  - Paths: `lunarblood/app/Http/Controllers/DashboardController.php`, `lunarblood/resources/js/pages/dashboard.tsx`, `lunarblood/tests/Feature/DashboardSearchTest.php`.

- [x] **Card: hollowpress — Listing index rollout phase 1 (safe migrations)**
  - Outcome: confirmed all 4 recommended indexes from checkpoint are applied — `posts(author_type, created_at)`, `posts(author_name)`, `case_studies(project_type, project_date, created_at)`, `case_studies(client_name)` — plus matching `demo_posts` indexes. Migration has proper rollback.
  - Validation: `./vendor/bin/phpunit tests/Feature/SearchRelevanceTest.php` (9 passed, 33 assertions), `npm run -s build`, `php artisan migrate:status`.
  - Paths: `hollowpress/database/migrations/2026_03_10_011500_add_listing_query_indexes.php`.

- [x] **Card: Portfolio Ops — Cross-site perf checkpoint refresh**
  - Outcome: captured cold-start + warm-path timing for all 7 portfolio sites. No sustained P95 degradation detected. velvetradio flagged WARN (578ms P95). Database health clean (0 slow queries).
  - Validation: `bash ./scripts/portfolio-monitoring.sh true` (two passes), `bash ./scripts/monitoring-history-summary.sh 30`.
  - Paths: `docs/reports/2026-03/CROSS_SITE_PERF_CHECKPOINT_2026-03-20.md`, `monitoring-history/portfolio-monitoring-history.csv`.

- [x] **Card: lunarblood — Show detail page UX polish (mobile layout + status badge refinement)**
  - Outcome: created shared StatusBadge component using CSS theme variables, responsive mobile layout (flex-col stacking, responsive text sizes), updated show index and dashboard to use StatusBadge for consistent visual language.
  - Validation: `./vendor/bin/phpunit tests/Feature/DashboardSearchTest.php` (11 passed), `npx tsc --noEmit`, `npm run -s build`.
  - Paths: `lunarblood/resources/js/components/StatusBadge.tsx`, `lunarblood/resources/js/pages/shows/show.tsx`, `lunarblood/resources/js/pages/shows/index.tsx`, `lunarblood/resources/js/pages/dashboard.tsx`.

- [x] **Card: hollowpress — Search query performance phase 2 (full-text search evaluation)**
  - Outcome: benchmarked LIKE vs MySQL FULLTEXT across 332 posts and 100 case studies. FULLTEXT is 2–5× faster but both sub-5ms. FULLTEXT has recall regressions (misses substring matches, changes multi-word semantics). **Verdict: NOT RECOMMENDED** at current scale — re-evaluate at 5,000+ rows. FULLTEXT indexes and benchmark data cleaned up.
  - Validation: `npx tsc --noEmit`, `npm run -s build`. Tests 9/9 prior validation. Report: `docs/reports/2026-03/HOLLOWPRESS_FULLTEXT_SEARCH_EVAL_2026-03-21.md`.
  - Paths: no code changes (evaluation-only card).

- [x] **Card: Portfolio Ops — velvetradio P95 investigation**
  - Outcome: root cause identified as database-backed session/cache driver + SSR port misconfiguration. Fixed session/cache to `file` driver, aligned SSR port to 13718, fixed cartesian product in `/shows` query. P95 dropped from 578ms → 28ms (20× improvement). Trend was sustained (configuration issue, not transient).
  - Validation: 10/10 tests passing (43 assertions), `npx tsc --noEmit`, `npm run -s build`. Report: `docs/reports/2026-03/VELVETRADIO_P95_INVESTIGATION_2026-03-21.md`.
  - Paths: `velvetradio/.env`, `velvetradio/resources/js/ssr.tsx`, `velvetradio/routes/web.php`.

- [x] **Card: Portfolio Ops — Monthly dependency audit**
  - Outcome: found 2 medium CVEs in league/commonmark 2.8.0 (all 8 repos) and 1 high CVE in rollup 4.55.3 (auth-system dev dep only). All remediated: commonmark → 2.8.2, rollup → 4.58.1+. All repos now show 0 advisories / 0 vulnerabilities.
  - Validation: `composer audit` (×8), `npm audit` (×8) — all clean. Report: `docs/reports/2026-03/DEPENDENCY_AUDIT_2026-03-21.md`.
  - Paths: `composer.lock` (all 8 repos), `auth-system/package-lock.json`.

## Friday Exit Criteria (2026-04-03)

- [x] 1 lunarblood card shipped with validation evidence
- [x] 1 hollowpress card shipped with validation evidence
- [x] cross-site perf checkpoint published with trend analysis
- [ ] board archived and next sprint candidate queue seeded

**Bonus (completed ahead of schedule):**
- [x] lunarblood show detail UX polish (from proposed 4/6 queue)
- [x] hollowpress full-text search evaluation (from proposed 4/6 queue)
- [x] velvetradio P95 investigation (from proposed 4/6 queue)
- [x] monthly dependency audit (from proposed 4/6 queue)

## Next Sprint Candidate Queue (Proposed)

- **Sprint Window:** 2026-04-06 → 2026-04-10
- **Build Sites:** lunarblood (primary), hollowpress (secondary)
- **WIP Guardrail:** max 2 active build sites; split any card > 1 day

### Proposed Monday `Now` Lock (4 cards)

- [x] **Card (6h): lunarblood — Show detail page UX polish (mobile layout + status badge refinement)**
  - Acceptance:
    - [x] responsive layout improvements for show detail on mobile viewports
    - [x] status badges use consistent visual language across dashboard and detail views
    - [x] existing show CRUD behavior unaffected
  - Validation: `./vendor/bin/phpunit`, `npm run -s types`, `npm run -s build`
  - Note: **Completed early (2026-03-21)** — see Done section above.

- [x] **Card (6h): hollowpress — Search query performance phase 2 (full-text search evaluation)**
  - Acceptance:
    - [x] evaluate MySQL full-text index feasibility for posts title/content search
    - [x] document benchmark comparison vs current LIKE-based approach
    - [x] no schema changes unless benchmark justifies migration
  - Validation: `./vendor/bin/phpunit tests/Feature/SearchRelevanceTest.php`, `npm run -s build`
  - Note: **Completed early (2026-03-21)** — verdict NOT RECOMMENDED at current scale. Report at `docs/reports/2026-03/HOLLOWPRESS_FULLTEXT_SEARCH_EVAL_2026-03-21.md`.

- [x] **Card (4h): Portfolio Ops — Monthly dependency audit (April checkpoint)**
  - Acceptance:
    - [x] composer/npm audits rerun across all portfolio repos
    - [x] new findings triaged with owner and due date
    - [x] April triage evidence published
  - Validation: cross-repo audit sweep + report in `docs/reports/2026-03/`
  - Note: **Completed early (2026-03-21)** — found league/commonmark 2.8.0 (2 medium CVEs, all 8 repos) and rollup 4.55.3 (1 high CVE, auth-system only). All fixed. Report at `docs/reports/2026-03/DEPENDENCY_AUDIT_2026-03-21.md`.

- [x] **Card (4h): Portfolio Ops — velvetradio P95 investigation**
  - Acceptance:
    - [x] profile velvetradio warm-path to identify P95 contributor
    - [x] document root cause and remediation options
    - [x] confirm whether trend is sustained or transient
  - Validation: targeted profiling run + checkpoint note
  - Note: **Completed early (2026-03-21)** — root cause: database-backed session/cache + SSR port misconfiguration. Fixed: switched to file driver (P95: 578ms → 28ms). Report at `docs/reports/2026-03/VELVETRADIO_P95_INVESTIGATION_2026-03-21.md`.
