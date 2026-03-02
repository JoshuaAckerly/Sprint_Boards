# Sprint Board (Execution View)

Use this as your weekly operating board for the 7-site portfolio.
Recommended WIP limit: **max 2 active build sites**.

## Current Sprint

- **Sprint Window:** 2026-03-09 → 2026-03-13
- **Primary Site:** lunarblood
- **Secondary Site:** hollowpress
- **Maintenance Sites:** graveyardjokes, synthveil, thevelvetpulse, velvetradio
- **R&D Site:** studio
- **Sprint Goal:** Ship two lunarblood outcomes, one hollowpress outcome, and complete one portfolio reliability/documentation pass with evidence.
- **Execution Mode:** AI-assisted micro-sprints (target 4-8h cards; split any card that exceeds 1 day; every AI-generated change requires human validation evidence).

## Today Snapshot

- **Last Updated:** 2026-03-01
- **Status:** ✅ Sprint execution complete: 4/4 locked cards shipped with validation evidence.
- **Carryover Posture:** Move unresolved monitoring environment-state triage into next sprint queue; keep non-priority feature requests deferred.
- **Open Risks:** dependency regressions during updates, scope drift from maintenance requests, and deploy contention.
- **Kickoff Gate:** sprint starts only if each `Now` card has acceptance criteria + validation commands + rollback note.

## Locked Queue (Sprint Start)

- [x] **Card (6h): lunarblood — Dashboard data hardening + state coverage**
  - Owner: Joshua
  - Acceptance:
    - [x] key dashboard widgets use production-shape data and avoid null-state errors
    - [x] explicit loading, empty, and error states for each widget block
    - [x] route smoke checks pass for dashboard and linked quick-action paths
  - Validation: `npm run types`, `npm run build`, `php artisan route:list --path=dashboard`, `php artisan route:list --path=tour`, `php artisan route:list --path=venues`, `php artisan route:list --path=shop`

- [x] **Card (6h): lunarblood — Search functionality baseline (phase 1)**
  - Owner: Joshua
  - Acceptance:
    - [x] searchable entity scope documented and implemented (shows + venues)
    - [x] no-results and loading states present
    - [x] basic edge-case checks pass (empty query, special chars, long query)
  - Validation: `./vendor/bin/phpunit tests/Feature/DashboardSearchTest.php`, `npm run types`, `npm run build`, `php artisan route:list --path=dashboard/search`

- [x] **Card (6h): hollowpress — Listing performance pass (query + render stability)**
  - Owner: Joshua
  - Acceptance:
    - [x] `/posts` and `/case-studies` keep pagination/query persistence stable
    - [x] no obvious over-fetching/over-render paths in index views
    - [x] before/after notes recorded for any query/render tuning
  - Validation: `./vendor/bin/phpunit tests/Feature/SearchRelevanceTest.php`, `npm run build`, `php artisan route:list --path=posts`, `php artisan route:list --path=case-studies`

- [x] **Card (4h): Portfolio Ops — Monitoring/error review cadence docs refresh**
  - Owner: Joshua
  - Acceptance:
    - [x] daily and weekly review schedule captured for all active/maintenance sites
    - [x] log paths, threshold triggers, and escalation owner listed
    - [x] verification checklist includes exact commands and evidence path
  - Validation: `bash ./scripts/portfolio-monitoring.sh true`, `bash ./scripts/monitoring-history-summary.sh 7`, docs index refresh in `docs/README.md`

## Lane: Now (This Sprint Commitments)

RAG legend: `🟢 On track` | `🟠 At risk` | `🔴 Blocked`

### lunarblood (Primary) - Target: 2 outcomes shipped
- [x] **Card (6h): Dashboard data hardening + state coverage**
  - Status: ✅ Completed
  - Owner: Joshua

- [x] **Card (6h): Search functionality baseline (phase 1)**
  - Status: ✅ Completed
  - Owner: Joshua

### hollowpress (Secondary) - Target: 1 outcome shipped
- [x] **Card (6h): Listing performance pass (query + render stability)**
  - Status: ✅ Completed
  - Owner: Joshua

### Portfolio-wide Ops - Target: 1 reliability/docs pass
- [x] **Card (4h): Monitoring/error review cadence docs refresh**
  - Status: ✅ Completed
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

- [x] **Card: lunarblood — Dashboard data hardening + state coverage**
  - Outcome: normalized dashboard payload handling to prevent null/shape crashes, added explicit loading/error/empty state handling for widget blocks, and improved low-stock quick action anchor scrolling.
  - Validation: `npm run types`, `npm run build`, `php artisan route:list --path=dashboard`, `php artisan route:list --path=tour`, `php artisan route:list --path=venues`, `php artisan route:list --path=shop`.
  - Paths: `lunarblood/resources/js/pages/dashboard.tsx`, `lunarblood/app/Http/Controllers/DashboardController.php`.

- [x] **Card: lunarblood — Search functionality baseline (phase 1)**
  - Outcome: implemented authenticated dashboard search for shows and venues with scoped JSON endpoint, search UI results panels, and explicit loading/no-results/error states.
  - Validation: `./vendor/bin/phpunit tests/Feature/DashboardSearchTest.php` (5 passed, 16 assertions), `npm run types`, `npm run build`, `php artisan route:list --path=dashboard/search`.
  - Paths: `lunarblood/app/Http/Controllers/DashboardController.php`, `lunarblood/routes/web.php`, `lunarblood/resources/js/pages/dashboard.tsx`, `lunarblood/tests/Feature/DashboardSearchTest.php`.

- [x] **Card: hollowpress — Listing performance pass (query + render stability)**
  - Outcome: optimized listing option-query load with short-lived cache in controllers and stabilized search highlight rendering to avoid regex state drift; memoized featured/regular case-study splits to reduce unnecessary recomputation.
  - Validation: `./vendor/bin/phpunit tests/Feature/SearchRelevanceTest.php` (6 passed, 15 assertions), `npm run build`, `php artisan route:list --path=posts`, `php artisan route:list --path=case-studies`.
  - Before/after notes:
    - Before: author and case-study filter options were rebuilt from DB on every listing request; highlight rendering relied on `RegExp.test` with a global regex during map rendering.
    - After: filter options are cached for 10 minutes (`posts.author_filter_options`, `case_studies.filter_options`), highlight rendering is index-based and deterministic, and case-study featured/regular partitions are memoized.
  - Paths: `hollowpress/app/Http/Controllers/PostController.php`, `hollowpress/app/Http/Controllers/CaseStudyController.php`, `hollowpress/resources/js/pages/Posts/Index.tsx`, `hollowpress/resources/js/pages/CaseStudies/Index.tsx`.

- [x] **Card: Portfolio Ops — Monitoring/error review cadence docs refresh**
  - Outcome: published portfolio-level monitoring cadence standard with daily/weekly schedule, thresholds, log sources, and escalation ownership; added command verification report and moved generated baseline report into monthly evidence path.
  - Validation: `bash ./scripts/portfolio-monitoring.sh true`, `bash ./scripts/monitoring-history-summary.sh 7`.
  - Paths: `docs/standards/PORTFOLIO_MONITORING_ERROR_REVIEW_CADENCE.md`, `docs/reports/2026-03/MONITORING_CADENCE_COMMAND_VERIFICATION_2026-03-01.md`, `docs/reports/2026-03/PORTFOLIO_MONITORING_BASELINE_2026-03-01.md`, `docs/README.md`.

## Friday Exit Criteria (2026-03-13)

- [x] 2 lunarblood cards shipped with validation evidence
- [x] 1 hollowpress card shipped with validation evidence
- [x] monitoring/error cadence docs refreshed with command/path verification
- [x] board updated for next sprint candidate queue

## Next Sprint Candidate Queue (Draft)

- **Card (4h): Portfolio Ops — Service/process health triage for cross-site 502/timeout baseline runs**
  - Goal: restore clean HTTP sampling conditions for portfolio monitoring and confirm app/upstream process health.

- **Card (6h): lunarblood — Search baseline phase 2 (result relevance + UX refinement)**
  - Goal: tighten ranking quality and quick navigation behavior based on phase-1 usage.

- **Card (6h): hollowpress — Listing query/index tuning follow-up**
  - Goal: convert observed hot paths into explicit DB/index tuning tasks with measured before/after impact.

- **Card (4h): Portfolio Ops — Dependency/vulnerability remediation wave 2 planning**
  - Goal: assign owners/dates for remaining high findings and define rollback-safe update batches.
