# Sprint Board (Execution View)

Use this as your weekly operating board for the 7-site portfolio.
Recommended WIP limit: **max 2 active build sites**.

## Current Sprint

- **Sprint Window:** 2026-03-23 → 2026-03-27
- **Primary Site:** lunarblood
- **Secondary Site:** hollowpress
- **Maintenance Sites:** graveyardjokes, synthveil, thevelvetpulse, velvetradio
- **R&D Site:** studio
- **Sprint Goal:** Restore full dependency auditability, complete one lunarblood UX quality outcome, and complete one hollowpress performance evidence outcome with validation.
- **Execution Mode:** AI-assisted micro-sprints (target 4-8h cards; split any card that exceeds 1 day; every AI-generated change requires human validation evidence).

## Today Snapshot

- **Last Updated:** 2026-03-01
- **Status:** 🟢 Kickoff-ready draft generated from prior sprint closeout queue.
- **Carryover Posture:** Prioritize auditability and evidence-first ops cards before optional feature expansion.
- **Open Risks:** dependency regressions during updates and scope creep from maintenance requests.
- **Kickoff Gate:** sprint starts only if each `Now` card has acceptance criteria + validation commands + rollback note.

## Locked Queue (Sprint Start)

- [x] **Card (4h): synthveil — npm auditability restore (`ENOLOCK`)**
  - Owner: Joshua
  - Acceptance:
    - [x] lockfile state restored and committed for consistent npm dependency graph
    - [x] `npm audit --audit-level=high --omit=dev` executes successfully
    - [x] remediation/evidence note captured in monthly report path
  - Validation: `npm install --package-lock-only --legacy-peer-deps`, `ls -la package-lock.json`, `npm audit --audit-level=high --omit=dev`, report update in `docs/reports/2026-03/`

- [x] **Card (4h): Portfolio Ops — Dependency audit addendum (post-synthveil fix)**
  - Owner: Joshua
  - Acceptance:
    - [x] composer/npm high-level audits rerun across all portfolio repos
    - [x] any new findings triaged with owner and due date
    - [x] monthly March triage evidence updated
  - Validation: portfolio audit command sweep + report update in `docs/reports/2026-03/`

- [x] **Card (6h): lunarblood — Dashboard search quality pass (query synonyms + empty-state polish)**
  - Owner: Joshua
  - Acceptance:
    - [x] at least one synonym/term quality refinement implemented for practical search queries
    - [x] empty/no-result messaging polished without changing page scope
    - [x] existing search edge-case behavior remains stable
  - Validation: `./vendor/bin/phpunit tests/Feature/DashboardSearchTest.php`, `npm run types`, `npm run build`

- [x] **Card (6h): hollowpress — Index query performance metrics checkpoint**
  - Owner: Joshua
  - Acceptance:
    - [x] before/after listing query timing evidence captured for `/posts` and `/case-studies`
    - [x] next index candidates documented with rationale
    - [x] listing behavior remains stable (search, pagination, filters)
  - Validation: `./vendor/bin/phpunit tests/Feature/SearchRelevanceTest.php`, `npm run build`, metrics note in `docs/reports/2026-03/`

## Lane: Now (This Sprint Commitments)

RAG legend: `🟢 On track` | `🟠 At risk` | `🔴 Blocked`

### Portfolio-wide Ops - Target: 2 reliability outcomes
- [x] **Card (4h): synthveil — npm auditability restore (`ENOLOCK`)**
  - Status: ✅ Completed
  - Owner: Joshua

- [x] **Card (4h): Dependency audit addendum (post-synthveil fix)**
  - Status: ✅ Completed
  - Owner: Joshua

- [x] **Card (6h): synthveil — public UX reliability pass (loading/error + filter/pagination)**
  - Status: ✅ Completed
  - Owner: Joshua

### lunarblood (Primary) - Target: 1 shipped outcome
- [x] **Card (6h): Dashboard search quality pass (query synonyms + empty-state polish)**
  - Status: ✅ Completed
  - Owner: Joshua

### hollowpress (Secondary) - Target: 1 shipped outcome
- [x] **Card (6h): Index query performance metrics checkpoint**
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
- [ ] board updated for next sprint candidate queue
