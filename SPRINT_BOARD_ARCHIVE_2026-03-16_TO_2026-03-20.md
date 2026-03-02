# Sprint Board (Execution View)

Use this as your weekly operating board for the 7-site portfolio.
Recommended WIP limit: **max 2 active build sites**.

## Current Sprint

- **Sprint Window:** 2026-03-16 → 2026-03-20
- **Primary Site:** lunarblood
- **Secondary Site:** hollowpress
- **Maintenance Sites:** graveyardjokes, synthveil, thevelvetpulse, velvetradio
- **R&D Site:** studio
- **Sprint Goal:** Ship one lunarblood improvement, one hollowpress tuning outcome, and two portfolio-ops reliability outcomes with evidence.
- **Execution Mode:** AI-assisted micro-sprints (target 4-8h cards; split any card that exceeds 1 day; every AI-generated change requires human validation evidence).

## Today Snapshot

- **Last Updated:** 2026-03-01
- **Status:** ✅ Sprint execution complete: 4/4 locked cards shipped with validation evidence.
- **Carryover Posture:** Promote wave-2 auditability follow-up (`synthveil` lockfile remediation) and monthly dependency checkpoint into next sprint queue.
- **Open Risks:** dependency regressions, local service/proxy drift causing false monitoring alarms, scope creep from maintenance asks.
- **Kickoff Gate:** sprint starts only if each `Now` card has acceptance criteria + validation commands + rollback note.

## Locked Queue (Sprint Start)

- [x] **Card (4h): Portfolio Ops — Service/process health triage for cross-site 502/timeout baseline runs**
  - Owner: Joshua
  - Acceptance:
    - [x] service and reverse-proxy process health checks documented and executed
    - [x] monitoring baseline run returns actionable HTTP sample (or explicit environment blocker note)
    - [x] triage note captured with root-cause direction + next action
  - Validation: `bash ./scripts/manage-all-projects.sh status`, `bash ./scripts/manage-all-projects.sh start`, `bash ./scripts/portfolio-monitoring.sh true`, `bash ./scripts/monitoring-history-summary.sh 7`, triage note in `docs/reports/2026-03/`

- [x] **Card (6h): lunarblood — Search baseline phase 2 (result relevance + UX refinement)**
  - Owner: Joshua
  - Acceptance:
    - [x] search relevance ordering tuned for common queries
    - [x] quick navigation behavior clarified for result cards
    - [x] no regressions in phase-1 edge-case handling
  - Validation: `./vendor/bin/phpunit tests/Feature/DashboardSearchTest.php`, `npm run types`, `npm run build`, `php artisan route:list --path=dashboard/search`

- [x] **Card (6h): hollowpress — Listing query/index tuning follow-up**
  - Owner: Joshua
  - Acceptance:
    - [x] hot query paths identified and documented
    - [x] at least one measurable tuning adjustment applied or explicitly deferred with rationale
    - [x] listing behavior remains stable (pagination/query persistence)
  - Validation: `./vendor/bin/phpunit tests/Feature/SearchRelevanceTest.php`, `npm run build`, `php artisan route:list --path=posts`, `php artisan route:list --path=case-studies`, before/after query notes

- [x] **Card (4h): Portfolio Ops — Dependency/vulnerability remediation wave 2 planning**
  - Owner: Joshua
  - Acceptance:
    - [x] remaining high findings inventoried by site
    - [x] owner + due date assigned for each update batch
    - [x] rollback note attached for risky changes
  - Validation: `composer audit --no-interaction`, `npm audit --audit-level=high --omit=dev`, report update in `docs/reports/2026-03/`

## Lane: Now (This Sprint Commitments)

RAG legend: `🟢 On track` | `🟠 At risk` | `🔴 Blocked`

### lunarblood (Primary) - Target: 1 shipped outcome
- [x] **Card (6h): Search baseline phase 2 (result relevance + UX refinement)**
  - Status: ✅ Completed
  - Owner: Joshua

### hollowpress (Secondary) - Target: 1 shipped outcome
- [x] **Card (6h): Listing query/index tuning follow-up**
  - Status: ✅ Completed
  - Owner: Joshua

### Portfolio-wide Ops - Target: 2 reliability outcomes
- [x] **Card (4h): Service/process health triage for cross-site 502/timeout baseline runs**
  - Status: ✅ Completed
  - Owner: Joshua

- [x] **Card (4h): Dependency/vulnerability remediation wave 2 planning**
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

- [x] **Card: Portfolio Ops — Service/process health triage for cross-site 502/timeout baseline runs**
  - Outcome: confirmed initial 502/timeout condition was driven by stopped managed app processes; restarted stack and restored actionable monitoring baseline (HTTP 200 across monitored sites, 0% error rate).
  - Validation: `bash ./scripts/manage-all-projects.sh status`, `bash ./scripts/manage-all-projects.sh start`, `bash ./scripts/manage-all-projects.sh status`, `bash ./scripts/portfolio-monitoring.sh true`, `bash ./scripts/monitoring-history-summary.sh 7`.
  - Paths: `docs/reports/2026-03/SERVICE_PROCESS_HEALTH_TRIAGE_2026-03-01.md`, `docs/reports/2026-03/PORTFOLIO_MONITORING_BASELINE_2026-03-01.md`.

- [x] **Card: lunarblood — Search baseline phase 2 (result relevance + UX refinement)**
  - Outcome: implemented weighted relevance ranking for shows and venues (exact/prefix/contains) and clarified quick navigation in dashboard search results with explicit `Open` and list-navigation actions.
  - Validation: `./vendor/bin/phpunit tests/Feature/DashboardSearchTest.php` (6 passed, 19 assertions), `npm run types`, `npm run build`, `php artisan route:list --path=dashboard/search`.
  - Paths: `lunarblood/app/Http/Controllers/DashboardController.php`, `lunarblood/resources/js/pages/dashboard.tsx`, `lunarblood/tests/Feature/DashboardSearchTest.php`.

- [x] **Card: hollowpress — Listing query/index tuning follow-up**
  - Outcome: reduced listing payload size for posts by selecting preview-sized content and reduced author filter option overhead with a single DB-level union/distinct query; trimmed case-study index payload to fields consumed by listing UI.
  - Validation: `./vendor/bin/phpunit tests/Feature/SearchRelevanceTest.php` (6 passed, 15 assertions), `npm run build`, `php artisan route:list --path=posts`, `php artisan route:list --path=case-studies`.
  - Before/after notes:
    - Before: post listings selected full `content` blobs and filter options were composed by merging two separate pluck arrays in PHP memory; case-study index selected extra fields not used by the listing page.
    - After: post listings select `LEFT(content, 1200)` previews, author options are resolved through a single union/distinct DB pipeline, and case-study listing query excludes unused fields.
  - Paths: `hollowpress/app/Http/Controllers/PostController.php`, `hollowpress/app/Http/Controllers/CaseStudyController.php`.

- [x] **Card: Portfolio Ops — Dependency/vulnerability remediation wave 2 planning**
  - Outcome: completed cross-site dependency audit refresh, documented current high/critical inventory (none detected in auditable projects), assigned wave-2 owners/dates, and captured rollback guidance for risky update batches.
  - Validation: `composer audit --no-interaction` and `npm audit --audit-level=high --omit=dev` sweep across portfolio projects.
  - Note: `synthveil` npm audit is currently blocked by missing lockfile (`ENOLOCK`) and is scheduled as Batch A remediation.
  - Paths: `docs/reports/2026-03/DEPENDENCY_VULN_REMEDIATION_WAVE2_PLAN_2026-03-01.md`, `docs/README.md`.

## Friday Exit Criteria (2026-03-20)

- [x] 1 lunarblood card shipped with validation evidence
- [x] 1 hollowpress card shipped with validation evidence
- [x] service/process triage documented with evidence path
- [x] dependency remediation wave 2 plan documented with owners/dates
- [x] board updated for next sprint candidate queue

## Next Sprint Candidate Queue (Draft)

- **Card (4h): synthveil — npm auditability restore (`ENOLOCK`)**
  - Goal: regenerate/commit lockfile state and restore reliable `npm audit` execution.

- **Card (4h): Portfolio Ops — Dependency audit addendum (post-synthveil fix)**
  - Goal: rerun high-level npm/composer audits and update monthly March triage evidence.

- **Card (6h): lunarblood — Dashboard search quality pass (query synonyms + empty-state polish)**
  - Goal: refine practical search discoverability while preserving current relevance ordering.

- **Card (6h): hollowpress — Index query performance metrics checkpoint**
  - Goal: capture measured before/after query timing evidence and identify next index candidates.
