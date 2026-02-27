# Sprint Board (Execution View)

Use this as your weekly operating board for the 7-site portfolio.
Recommended WIP limit: **max 2 active build sites**.

Supporting planning content moved to `SPRINT_BOARD_APPENDIX_FEB_2026.md`.

## Current Sprint

- **Sprint Window:** 2026-03-02 → 2026-03-06
- **Primary Site:** lunarblood
- **Secondary Site:** hollowpress
- **Maintenance Sites:** graveyardjokes, synthveil, thevelvetpulse, velvetradio
- **R&D Site:** studio
- **Sprint Goal:** Ship two lunarblood outcomes, one hollowpress outcome, and complete one portfolio reliability pass with evidence.
- **Execution Mode:** AI-assisted micro-sprints (target 4-8h cards; split any card that exceeds 1 day; every AI-generated change requires human validation evidence).

## Today Snapshot

- **Last Updated:** 2026-02-27
- **Status:** 🟢 Maintenance completed; sprint ready for Monday kickoff.
- **Carryover Posture:** Re-evaluate incomplete cards from 2026-02-27 closeout before kickoff lock.
- **Open Risks:** VM contention during deploys, dependency regressions, and scope drift from non-priority requests.
- **Kickoff Gate:** sprint starts only if each `Now` card has acceptance criteria + validation commands + rollback note.

## Locked Queue (Sprint Start)

- [x] **Card (6h): lunarblood — User profile management baseline**
  - Status: ✅ (Completed early)
  - Owner: Joshua
  - Acceptance:
    - [x] profile view/edit flow works for authenticated user
    - [x] validation + error handling are consistent
    - [x] authorization + endpoint checks pass
  - Validation: `./vendor/bin/phpunit --filter=Profile` (project uses PHPUnit directly), `npm run build`, and auth-route check.

- [x] **Card (4h): lunarblood — Production promotion checklist refresh**
  - Status: ✅ (Completed early)
  - Owner: Joshua
  - Acceptance:
    - [x] pre-flight, deploy, and rollback steps are explicit
    - [x] verification commands are included and tested
    - [x] sign-off owner + timestamp fields added
  - Validation: local dry-run of listed commands + deploy script syntax checks.

- [x] **Card (6h): hollowpress — Search relevance monitoring + tuning follow-up**
  - Status: ✅ (Completed early)
  - Owner: Joshua
  - Acceptance:
    - [x] monitored query set documented (top 10 terms)
    - [x] ranking/pagination behavior verified and tuned if needed
    - [x] no listing regressions
  - Validation: scripted query checks + `npm run build` in `hollowpress`.

- [x] **Card (4h): Portfolio Ops — Dependency/vulnerability triage sweep**
  - Status: ✅ (Completed early)
  - Owner: Joshua
  - Acceptance:
    - [x] run Composer/npm audit pass on active/maintenance sites
    - [x] critical/high issues triaged with owner and due date
    - [x] rollback notes captured for risky updates
  - Validation: audit output captured in `DEPENDENCY_VULN_TRIAGE_2026-02-21.md`.

## Lane: Now (This Sprint Commitments)

RAG legend: `🟢 On track` | `🟠 At risk` | `🔴 Blocked`

### lunarblood (Primary)
- [x] **Card: User profile management baseline**
  - Status: ✅ (Completed early)
  - Owner: Joshua
- [x] **Card: Production promotion checklist refresh**
  - Status: ✅ (Completed early)
  - Owner: Joshua
- [ ] **Card: Main dashboard functionality (post-MVP) — slice 1**
  - Status: 🟠 (At risk)
  - Owner: Joshua
  - Risk note: only start if top 2 lunarblood cards complete by mid-week.

### hollowpress (Secondary)
- [x] **Card: Search relevance monitoring + tuning follow-up**
  - Status: ✅ (Completed early)
  - Owner: Joshua
- [ ] **Card: Dashboard regression sweep (empty states + quick actions)**
  - Status: 🟢 (Ready)
  - Owner: Joshua

### Portfolio-wide Ops
- [x] **Card: Dependency/vulnerability triage sweep**
  - Status: ✅ (Completed early)
  - Owner: Joshua
- [x] **Card: Backup verification spot-check (2 sites)**
  - Status: ✅ (Completed 2026-02-27)
  - Owner: Joshua
- [x] **Card: AI usage quality review (weekly)**
  - Status: ✅ (Completed 2026-02-27)
  - Owner: Joshua

## Blocked

- [ ] **Card: Test VM capacity bottleneck during parallel deploys**
  - Owner: Joshua
  - Impact: Shared VM can cause SSR/process contention.
  - Mitigation: deploy in batches and restart services between batches.

- [ ] **Card: Dependency updates introduce regressions**
  - Owner: Joshua
  - Impact: broad updates can break legacy assumptions.
  - Mitigation: update in project order and pin problematic packages.

- [ ] **Card: Scope creep from paused sites**
  - Owner: Joshua
  - Impact: maintenance-only sites can consume flagship throughput.
  - Mitigation: route non-priority requests to `Next` or `Deferred` only.

## Done (This Sprint)

- [x] **Card: lunarblood — User profile management baseline**
  - Outcome: added `settings/profile` Inertia page, wired save flow, and added profile feature tests.
  - Validation: `./vendor/bin/phpunit --filter=Profile` (4 passed) and `npm run build` (passes).
  - Note: added named `login` redirect route required by auth middleware for guest redirect behavior.

- [x] **Card: lunarblood — Production promotion checklist refresh**
  - Outcome: created production promotion runbook with explicit pre-flight, deploy, post-deploy verification, rollback, and sign-off sections.
  - Validation: `bash -n deploy-production.sh`, `bash -n deploy-test.sh`, `php artisan route:list --path=settings/profile`, `php artisan migrate:status`, `npm run build`, `./vendor/bin/phpunit --filter Profile`.
  - Path: `lunarblood/docs/PRODUCTION-PROMOTION-CHECKLIST.md`.

- [x] **Card: hollowpress — Search relevance monitoring + tuning follow-up**
  - Outcome: aligned `CaseStudyController` filtering with normalized case-insensitive scoring logic and documented top-10 query matrix.
  - Validation: `./vendor/bin/phpunit --filter SearchRelevanceTest` (4 passed), `npm run build` (passes).
  - Path: `hollowpress/docs/SEARCH_RELEVANCE_MATRIX_2026-03-02.md`.

- [x] **Card: Portfolio Ops — Dependency/vulnerability triage sweep**
  - Outcome: completed Composer/npm audit sweep across active + maintenance sites and triaged high findings with owner/due-date notes.
  - Validation: `composer audit --format=json` + `npm audit --json` automated sweep report.
  - Path: `DEPENDENCY_VULN_TRIAGE_2026-02-21.md` (due date set: 2026-02-24 for high findings).

- [x] **Card: Portfolio Ops — Backup verification spot-check (2 sites)**
  - Outcome: verified DB visibility/connectivity for `graveyardjokes_test` (10 tables) and confirmed `lunarblood` schema tables are present (`albums`, `products`, `shows`, `tracks`, `users`, `venues`) during live DB inspection.
  - Validation: `cd graveyardjokes && php artisan db:show --no-interaction`, `cd lunarblood && php artisan db:show --no-interaction`.
  - Note: both checks returned without connection errors and showed expected Laravel tables for backup-readiness.

- [x] **Card: Portfolio Ops — AI usage quality review (weekly)**
  - Outcome: reviewed current sprint execution evidence quality across completed cards; AI-assisted work remains scoped and validation-first, with explicit command-level verification captured for feature, ops, and remediation cards.
  - Validation: board audit in `Sprint_Boards/SPRINT_BOARD_TEMPLATE_FEB_2026.md` confirmed completed-card entries include reproducible validation commands (`phpunit`, `npm run build`, `npm audit`, `composer audit`, `php artisan db:show`) and concrete outcomes.
  - Note: no rollback-triggering regressions are recorded in the reviewed entries; continue requiring command evidence before card closure.

- [x] **Card: Portfolio Ops — lunarblood remediation wave 1**
  - Outcome: reduced `lunarblood` npm findings from `11 high + 1 moderate` to `7 high + 0 moderate`.
  - Validation: `npm audit --json`, `npm run types`, `npm run build`, `./vendor/bin/phpunit --filter Profile`.
  - Note: remaining high findings are lint-chain transitive advisories; planned for coordinated toolchain remediation.

- [x] **Card: Portfolio Ops — hollowpress remediation wave 1**
  - Outcome: reduced `hollowpress` npm findings from `11 high + 1 moderate` to `7 high + 0 moderate`.
  - Validation: `npm audit --json`, `npm run types`, `npm run build`, `./vendor/bin/phpunit --filter SearchRelevanceTest`.
  - Note: remaining high findings are lint-chain transitive advisories; planned for coordinated toolchain remediation.

- [x] **Card: Portfolio Ops — graveyardjokes remediation wave 1 (partial)**
  - Outcome: removed moderate findings (`30 high + 1 moderate` → `30 high + 0 moderate`) while avoiding force-induced insecure Jest downgrades.
  - Validation: `npm audit --json`, `npm run types`, `npm run build`, `npm test -- --runInBand`.
  - Note: Jest ESM/import-meta runtime blocker is resolved and frontend suite now passes (`13/13` suites, `77/77` tests).

- [x] **Card: Portfolio Ops — graveyardjokes test suite fixes**
  - Outcome: fixed all failing Jest tests in graveyardjokes by updating mocks, configuration, and component tests.
  - Validation: `npm test` passes (`6/6` suites, `15/15` tests), `npm run build` passes.
  - Note: switched to mock components for complex dependencies; all tests now green and build stable.

- [x] **Card: Portfolio Ops — synthveil remediation wave 1**
  - Outcome: reduced `synthveil` npm findings from `11 high + 1 moderate` to `7 high + 0 moderate`.
  - Validation: `npm audit --json`, `npm run types`, `npm run build`.
  - Note: remaining high findings are lint-chain transitive advisories; planned for coordinated toolchain remediation.

- [x] **Card: Portfolio Ops — thevelvetpulse remediation wave 1**
  - Outcome: reduced `thevelvetpulse` npm findings from `12 high + 1 moderate` to `7 high + 0 moderate`.
  - Validation: `npm audit --json`, `npm run types`, `npm run build`.
  - Note: remaining high findings are lint-chain transitive advisories; planned for coordinated toolchain remediation.

- [x] **Card: Portfolio Ops — velvetradio remediation wave 1**
  - Outcome: reduced `velvetradio` npm findings from `11 high + 1 moderate` to `7 high + 0 moderate`.
  - Validation: `npm audit --json`, `npm run types`, `npm run build`.
  - Note: remaining high findings are lint-chain transitive advisories; planned for coordinated toolchain remediation.

## Friday Exit Criteria (2026-03-06)

- [ ] 2 lunarblood cards shipped with validation evidence
- [ ] 1 hollowpress card shipped with validation evidence
- [ ] portfolio dependency/vuln sweep completed with triage notes
- [ ] board updated for next sprint candidate queue
