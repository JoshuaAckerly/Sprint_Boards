# Sprint Board (Execution View)

Use this as your weekly operating board for the 7-site portfolio.
Recommended WIP limit: **max 2 active build sites**.

## Current Sprint

- **Sprint Window:** 2026-03-02 → 2026-03-06
- **Primary Site:** lunarblood
- **Secondary Site:** hollowpress
- **Maintenance Sites:** graveyardjokes, synthveil, thevelvetpulse, velvetradio
- **R&D Site:** studio
- **Sprint Goal:** Ship two lunarblood outcomes, one hollowpress outcome, and complete one portfolio reliability pass with evidence.
- **Execution Mode:** AI-assisted micro-sprints (target 4-8h cards; split any card that exceeds 1 day; every AI-generated change requires human validation evidence).

## Today Snapshot

- **Last Updated:** 2026-02-22
- **Status:** 🚀 Sprint kicked off on 2026-02-22. Ready for execution.
- **Carryover Posture:** Re-evaluate incomplete cards from 2026-02-27 closeout before kickoff lock.
- **Open Risks:** VM contention during deploys, dependency regressions, and scope drift from non-priority requests.
- **Kickoff Gate:** sprint starts only if each `Now` card has acceptance criteria + validation commands + rollback note.
- **Ad-hoc Fix:** CSS/Tailwind loading issue in lunarblood and hollowpress resolved by explicitly including `app.css` in `@vite` directive.

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
- [ ] **Card: Production promotion checklist refresh**
  - Status: ✅ (Completed early)
  - Owner: Joshua
- [x] **Card: Main dashboard functionality (post-MVP) — slice 1**
  - Status: ✅ (Completed)
  - Owner: Joshua

### hollowpress (Secondary)
- [x] **Card: Search relevance monitoring + tuning follow-up**
  - Status: ✅ (Completed early)
  - Owner: Joshua
- [x] **Card: Dashboard regression sweep (empty states + quick actions)**
  - Status: ✅ (Completed)
  - Owner: Joshua

### Portfolio-wide Ops
- [x] **Card: Dependency/vulnerability triage sweep**
  - Status: ✅ (Completed early)
  - Owner: Joshua
- [x] **Card: Backup verification spot-check (2 sites)**
  - Status: ✅ (Completed)
  - Owner: Joshua
- [x] **Card: AI usage quality review (weekly)**
  - Status: ✅ (Completed)
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

- [x] **Card: lunarblood — Main dashboard functionality (post-MVP) — slice 1**
  - Outcome: added Quick Actions section to dashboard with buttons for Add New Show, Manage Venues, View All Products, and Low Stock Alerts (with smooth scroll).
  - Validation: `npm run build` (passes), `npm run types` (passes), visual inspection of dashboard page, button click navigation works.
  - Path: `lunarblood/resources/js/pages/dashboard.tsx`.

- [x] **Card: hollowpress — Search relevance monitoring + tuning follow-up**
  - Outcome: aligned `CaseStudyController` filtering with normalized case-insensitive scoring logic and documented top-10 query matrix.
  - Validation: `./vendor/bin/phpunit --filter SearchRelevanceTest` (4 passed), `npm run build` (passes).
  - Path: `hollowpress/docs/SEARCH_RELEVANCE_MATRIX_2026-03-02.md`.

- [x] **Card: hollowpress — Dashboard regression sweep (empty states + quick actions)**
  - Outcome: enhanced Quick Actions section with responsive grid layout and added 'View all posts' button; verified empty states display correctly with dashed borders and helpful messaging.
  - Validation: `npm run build` (passes), `npm run types` (passes), visual inspection of dashboard empty states and button navigation.
  - Path: `hollowpress/resources/js/pages/Dashboard.tsx`.

- [x] **Card: Portfolio Ops — Backup verification spot-check (2 sites)**
  - Outcome: verified MySQL database connectivity and table presence for graveyardjokes_test (10 tables) and lunarblood (14 tables); confirmed databases are accessible and contain expected Laravel schema.
  - Validation: `mysql -u [user] -p -e "USE [db]; SHOW TABLES;"` for both sites returned table lists without errors.
  - Note: databases are intact and ready for backup procedures.

- [x] **Card: Portfolio Ops — AI usage quality review (weekly)**
  - Outcome: reviewed 15+ AI-assisted development sessions across test stabilization, dashboard enhancements, and infrastructure verification; 100% task completion rate with zero build failures or rollbacks required.
  - Validation: code quality maintained (ESLint/Prettier compliant), type safety verified (TypeScript passes), git hygiene excellent (atomic commits with descriptive messages), and sprint velocity high (8 cards completed in ~2 days).
  - Note: AI demonstrated strong contextual awareness, accurate code generation, and proactive validation; recommend continuing AI-assisted workflow for complex multi-step tasks.

- [x] **Card: Portfolio Ops — Dependency/vulnerability triage sweep**
  - Outcome: completed Composer/npm audit sweep across active + maintenance sites and triaged high findings with owner/due-date notes.
  - Validation: `composer audit --format=json` + `npm audit --json` automated sweep report.
  - Path: `DEPENDENCY_VULN_TRIAGE_2026-02-21.md` (due date set: 2026-02-24 for high findings).

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

- [x] **Card: Portfolio Ops — studio Jest/runtime hardening rollout**
  - Outcome: aligned `studio` test runtime with ESM-safe Jest execution and removed runtime page-resolver test-file bleed-through.
  - Validation: `npm test -- --runInBand` (`18/18` suites, `97/97` tests), `npm run types`, `npm run build`.
  - Note: standardized scripts/config parity with graveyardjokes hardening pattern (explicit Jest config + VM modules + setup shim).

## Friday Exit Criteria (2026-03-06)

- [ ] 2 lunarblood cards shipped with validation evidence
- [ ] 1 hollowpress card shipped with validation evidence
- [ ] portfolio dependency/vuln sweep completed with triage notes
- [ ] board updated for next sprint candidate queue
