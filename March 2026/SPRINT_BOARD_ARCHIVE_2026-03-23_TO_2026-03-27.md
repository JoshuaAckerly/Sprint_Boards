# Sprint Board (Execution View) — ARCHIVED

Use this as your weekly operating board for the 7-site portfolio.
Recommended WIP limit: **max 2 active build sites**.

> **Archive Note:** This sprint is complete. Active board: `SPRINT_BOARD_NEXT_2026-03-30.md`.

## Current Sprint

- **Sprint Window:** 2026-03-23 → 2026-03-27
- **Primary Site:** lunarblood
- **Secondary Site:** hollowpress
- **Maintenance Sites:** graveyardjokes, synthveil, thevelvetpulse, velvetradio
- **R&D Site:** studio
- **Sprint Goal:** Restore full dependency auditability, complete one lunarblood UX quality outcome, and complete one hollowpress performance evidence outcome with validation.
- **Execution Mode:** AI-assisted micro-sprints (target 4-8h cards; split any card that exceeds 1 day; every AI-generated change requires human validation evidence).

## Weekly Workload Summary

- **Locked Workload:** 20h
- **Delivered Workload:** 26h
- **Variance:** +6h (bonus synthveil UX reliability pass)

## Done (This Sprint)

- [x] **Card: synthveil — npm auditability restore (`ENOLOCK`)**
  - Outcome: restored npm auditability by generating `package-lock.json` with peer-conflict-aware lockfile flow and confirmed high-level npm security status is clean.
  - Validation: `npm install --package-lock-only --legacy-peer-deps`, `ls -la package-lock.json`, `npm audit --audit-level=high --omit=dev` (`found 0 vulnerabilities`).
  - Paths: `synthveil/package-lock.json`, `docs/reports/2026-03/SYNTHVEIL_NPM_AUDITABILITY_RESTORE_2026-03-01.md`, `docs/README.md`.

- [x] **Card: Portfolio Ops — Dependency audit addendum (post-synthveil fix)**
  - Outcome: completed full portfolio addendum audit after synthveil lockfile restoration; composer and npm high-level audit outputs are clean across all eight repos, with owner/due-date checkpoint tracking captured for March.
  - Validation: cross-repo `composer audit --no-interaction` and `npm audit --audit-level=high --omit=dev` sweep.
  - Paths: `docs/reports/2026-03/DEPENDENCY_AUDIT_ADDENDUM_2026-03-01.md`, `docs/README.md`.

- [x] **Card: synthveil — public UX reliability pass (loading/error + filter/pagination)**
  - Outcome: shipped global navigation loading/error messaging, improved contact submit error handling, and added searchable/filterable/paginated `music` + `events` experiences with URL-state persistence and clear-filter controls.
  - Validation: `npm run -s types`, `npm run -s lint`, `php artisan test --testsuite=Unit`.
  - Paths: `synthveil/resources/js/layouts/main.tsx`, `synthveil/resources/js/pages/contact.tsx`, `synthveil/resources/js/pages/music.tsx`, `synthveil/resources/js/pages/events.tsx`, `synthveil/resources/js/components/header.tsx`, `synthveil/TODO.md`.

- [x] **Card: lunarblood — Dashboard search quality pass (query synonyms + empty-state polish)**
  - Outcome: improved dashboard search with practical synonym term expansion (`gig`, `concert`, `ticket`, location shorthand) and polished no-result messaging with clearer guidance and reset action.
  - Validation: `./vendor/bin/phpunit tests/Feature/DashboardSearchTest.php` (7 passed), `npm run -s types`, `npm run -s build`.
  - Paths: `lunarblood/app/Http/Controllers/DashboardController.php`, `lunarblood/resources/js/pages/dashboard.tsx`, `lunarblood/tests/Feature/DashboardSearchTest.php`.

- [x] **Card: hollowpress — Index query performance metrics checkpoint**
  - Outcome: captured before/after timing evidence for `/posts` and `/case-studies`, documented next index candidates with rationale, and confirmed listing/search/pagination behavior remains stable.
  - Validation: `./vendor/bin/phpunit tests/Feature/SearchRelevanceTest.php` (6 passed), `npm run -s build`, benchmark checkpoint run via `php artisan tinker` HTTP-kernel timing pass.
  - Paths: `hollowpress/docs/reports/2026-03/INDEX_QUERY_PERFORMANCE_CHECKPOINT_2026-03-01.md`.

## Friday Exit Criteria (2026-03-27)

- [x] synthveil npm auditability restored (`ENOLOCK` resolved)
- [x] portfolio dependency audit addendum documented with current evidence
- [x] 1 lunarblood card shipped with validation evidence
- [x] 1 hollowpress card shipped with validation evidence
- [x] board updated for next sprint candidate queue

## Next Sprint Candidate Queue (Promoted)

Promoted to `SPRINT_BOARD_NEXT_2026-03-30.md`:

- **Card (6h): lunarblood — Dashboard search UX follow-up (saved queries + keyboard refinement)**
- **Card (6h): hollowpress — Listing index rollout phase 1 (safe migrations)**
- **Card (4h): Portfolio Ops — Cross-site perf checkpoint refresh**
- **Card (4h): Portfolio Ops — Sprint board hygiene + archive rollover**
