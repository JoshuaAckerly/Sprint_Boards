# Sprint Board (Execution View)

Use this as your weekly operating board for the 7-site portfolio.
Recommended WIP limit: **max 2 active build sites**.

## Current Sprint

- **Sprint Window:** 2026-03-09 -> 2026-03-13
- **Primary Site:** lunarblood
- **Secondary Site:** hollowpress
- **Maintenance Sites:** graveyardjokes, synthveil, thevelvetpulse, velvetradio
- **R&D Site:** studio
- **Sprint Goal:** Ship two lunarblood outcomes, one hollowpress outcome, and one portfolio reliability/docs outcome with evidence.
- **Execution Mode:** AI-assisted micro-sprints (target 4-8h cards; split any card that exceeds 1 day; every AI-generated change requires human validation evidence).

## Today Snapshot

- **Last Updated:** 2026-03-08
- **Status:** 🟢 Lunarblood cards shipped with validation evidence; hollowpress + ops cards remain queued.
- **Carryover Posture:** no locked-card carryover from prior week; keep non-priority requests deferred.
- **Open Risks:** dependency regressions during updates, deploy contention during service restarts, and scope drift from maintenance requests.
- **Kickoff Gate:** sprint starts only if each `Now` card has acceptance criteria + validation commands + rollback note.

## Weekly Workload Summary

- **Locked Workload:** 22h
- **Reserved Buffer:** 8h
- **Weekly Max:** 30h
- **Mix Guidance:** 12h lunarblood / 6h hollowpress / 4h portfolio ops

## Locked Queue (Sprint Start)

- [x] **Card (6h): lunarblood — Dashboard data hardening + state coverage**
  - Owner: Joshua
  - Acceptance:
    - [x] key dashboard widgets use production-shape data and avoid null-state errors
    - [x] explicit loading, empty, and error states for each widget block
    - [x] route smoke checks pass for dashboard and linked quick-action paths
  - Validation: `npm run build`, `npm run types`, dashboard route smoke + quick-action click-through
  - Evidence (2026-03-08): `php artisan test tests/Feature/DashboardControllerTest.php tests/Feature/DashboardSearchTest.php` (11 tests, 85 assertions, pass), `npm run types` (pass), `npm run build` (pass)

- [x] **Card (6h): lunarblood — Search functionality baseline (phase 1)**
  - Owner: Joshua
  - Acceptance:
    - [x] searchable entity scope documented and implemented (shows + venues)
    - [x] no-results and loading states present
    - [x] basic edge-case checks pass (empty query, special chars, long query)
  - Validation: `./vendor/bin/phpunit --filter=Search`, `npm run build`, manual search smoke checks
  - Evidence (2026-03-08): `./vendor/bin/phpunit --filter=Search` (7 tests, 24 assertions, pass), `npm run types` (pass), `npm run build` (pass)

- [ ] **Card (6h): hollowpress — Listing performance pass (query + render stability)**
  - Owner: Joshua
  - Acceptance:
    - [ ] `/posts` and `/case-studies` keep pagination/query persistence stable
    - [ ] no obvious over-fetching/over-render paths in index views
    - [ ] before/after notes recorded for any query/render tuning
  - Validation: `./vendor/bin/phpunit --filter=SearchRelevanceTest`, `npm run build`, manual listing smoke checks

- [ ] **Card (4h): Portfolio Ops — Monitoring/error review cadence docs refresh**
  - Owner: Joshua
  - Acceptance:
    - [ ] daily and weekly review schedule captured for all active/maintenance sites
    - [ ] log paths, threshold triggers, and escalation owner listed
    - [ ] verification checklist includes exact commands and evidence path
  - Validation: command/path verification pass + docs review in `docs/`

## Lane: Now (This Sprint Commitments)

RAG legend: `🟢 On track` | `🟠 At risk` | `🔴 Blocked`

### lunarblood (Primary) - Target: 2 outcomes shipped
- [x] **Card (6h): Dashboard data hardening + state coverage**
  - Status: 🟢 Done (validated 2026-03-08)
  - Owner: Joshua

- [x] **Card (6h): Search functionality baseline (phase 1)**
  - Status: 🟢 Done (validated 2026-03-08)
  - Owner: Joshua

### hollowpress (Secondary) - Target: 1 outcome shipped
- [ ] **Card (6h): Listing performance pass (query + render stability)**
  - Status: 🟢 Ready
  - Owner: Joshua

### Portfolio-wide Ops - Target: 1 reliability/docs pass
- [ ] **Card (4h): Monitoring/error review cadence docs refresh**
  - Status: 🟢 Ready
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

- [ ] **Card: Scope creep from maintenance requests**
  - Status: 🟢 Mitigation in place, monitor only
  - Owner: Joshua
  - Mitigation: route non-priority asks to candidate queue unless they are security/availability incidents.

## Friday Exit Criteria (2026-03-13)

- [x] 2 lunarblood cards shipped with validation evidence
- [ ] 1 hollowpress card shipped with validation evidence
- [ ] monitoring/error cadence docs refreshed with command/path verification
- [ ] board updated for next sprint candidate queue

## Next Sprint Candidate Queue (Draft)

- **Card (4h): Portfolio Ops — Service/process health triage for cross-site 502/timeout baseline runs**
  - Goal: restore clean HTTP sampling conditions for portfolio monitoring and confirm app/upstream process health.

- **Card (6h): lunarblood — Search baseline phase 2 (result relevance + UX refinement)**
  - Goal: tighten ranking quality and quick navigation behavior based on phase-1 usage.

- **Card (6h): hollowpress — Listing query/index tuning follow-up**
  - Goal: convert observed hot paths into explicit DB/index tuning tasks with measured before/after impact.

- **Card (4h): Portfolio Ops — Dependency/vulnerability remediation wave 2 planning**
  - Goal: assign owners/dates for remaining high findings and define rollback-safe update batches.
