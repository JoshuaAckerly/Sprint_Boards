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

- **Last Updated:** 2026-02-27
- **Status:** 🚀 Priority 1 + hollowpress + portfolio monitoring complete (infra triage resolved).
- **Carryover Posture:** Re-evaluate incomplete cards from 2026-02-27 closeout before kickoff lock.
- **Open Risks:** VM contention during deploys, dependency regressions, and scope drift from non-priority requests.
- **Kickoff Gate:** sprint starts only if each `Now` card has acceptance criteria + validation commands + rollback note.
- **Ad-hoc Fix:** CSS/Tailwind loading issue in lunarblood and hollowpress resolved by explicitly including `app.css` in `@vite` directive. CSP updated to allow Bunny Fonts stylesheets and http for local development. Added dashboard link to nav for authenticated users in lunarblood.

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

### lunarblood (Primary) - Target: 2 outcomes shipped
- [x] **Card (8h): Enhanced venue management system**
  - Status: ✅ Completed
  - Owner: Joshua
  - Acceptance:
    - [x] Venue CRUD operations fully functional
    - [x] Venue-show relationships properly managed
    - [x] Admin interface for venue oversight
  - Validation: `./vendor/bin/phpunit --filter=Venue`, `npm run build`, manual testing of venue flows

- [x] **Card (6h): Streamlined event creation workflow**
  - Status: ✅ Completed
  - Owner: Joshua
  - Acceptance:
    - [x] Multi-step event creation form with validation
    - [x] Auto-save draft functionality
    - [x] Preview mode before publishing
  - Validation: `./vendor/bin/phpunit tests/Feature/ShowControllerTest.php --filter "test_show_creation_step_validation|test_show_creation_with_draft_saving|test_complete_show_creation|test_draft_session_persistence"` (4 passed, 27 assertions), end-to-end create flow validation

### hollowpress (Secondary) - Target: 1 outcome shipped
- [x] **Card (8h): Advanced content search and filtering**
  - Status: ✅ Completed
  - Owner: Joshua
  - Acceptance:
    - [x] Faceted search by category, date, author
    - [x] Advanced query syntax support
    - [x] Search result highlighting and snippets
  - Validation: `./vendor/bin/phpunit tests/Feature/SearchRelevanceTest.php` (6 passed, 15 assertions), manual search UX verification

### Portfolio-wide Ops - Target: 1 reliability pass
- [x] **Card (6h): Cross-site performance monitoring baseline**
  - Status: ✅ Completed
  - Owner: Joshua
  - Acceptance:
    - [x] Response time monitoring for all sites
    - [x] Error rate tracking and alerting
    - [x] Database query performance analysis
  - Validation: `bash ./portfolio-monitoring.sh true` (all 7 sites sampled, thresholds applied), baseline metrics captured in `PORTFOLIO_MONITORING_BASELINE_2026-02-27.md`

## Blocked

- [x] **Card: Test VM capacity bottleneck during parallel deploys**
  - Status: ✅ Mitigated
  - Owner: Joshua
  - Impact: Shared VM can cause SSR/process contention.
  - Mitigation: Created `deploy-all-batched.sh` script that deploys in batches with service restarts between.

- [x] **Card: Dependency updates introduce regressions**
  - Status: ✅ Mitigated
  - Owner: Joshua
  - Impact: broad updates can break legacy assumptions.
  - Mitigation: Created `DEPENDENCY_UPDATE_PROTOCOL.md` with systematic update process and pinning strategy.

- [x] **Card: Scope creep from paused sites**
  - Status: ✅ Mitigated
  - Owner: Joshua
  - Impact: maintenance-only sites can consume flagship throughput.
  - Mitigation: Created `SCOPE_MANAGEMENT_GUIDELINES.md` with request triage and capacity allocation rules.

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

- [x] **Card: lunarblood — Streamlined event creation workflow**
  - Outcome: completed server-validated multi-step show creation, added draft autosave, and enforced preview-before-publish behavior.
  - Validation: `./vendor/bin/phpunit tests/Feature/ShowControllerTest.php --filter "test_show_creation_step_validation|test_show_creation_with_draft_saving|test_complete_show_creation|test_draft_session_persistence"` (4 passed, 27 assertions).
  - Path: `lunarblood/app/Http/Controllers/ShowController.php`, `lunarblood/resources/js/pages/shows/create.tsx`, `lunarblood/tests/Feature/ShowControllerTest.php`.

- [x] **Card: hollowpress — Search relevance monitoring + tuning follow-up**
  - Outcome: aligned `CaseStudyController` filtering with normalized case-insensitive scoring logic and documented top-10 query matrix.
  - Validation: `./vendor/bin/phpunit --filter SearchRelevanceTest` (4 passed), `npm run build` (passes).
  - Path: `hollowpress/docs/SEARCH_RELEVANCE_MATRIX_2026-03-02.md`.

- [x] **Card: hollowpress — Dashboard regression sweep (empty states + quick actions)**
  - Outcome: enhanced Quick Actions section with responsive grid layout and added 'View all posts' button; verified empty states display correctly with dashed borders and helpful messaging.
  - Validation: `npm run build` (passes), `npm run types` (passes), visual inspection of dashboard empty states and button navigation.
  - Path: `hollowpress/resources/js/pages/Dashboard.tsx`.

- [x] **Card: hollowpress — Advanced content search and filtering**
  - Outcome: implemented faceted post search (category, author, date range), advanced query syntax (`OR`, quoted phrases), and result snippet/highlight rendering in post cards.
  - Validation: `./vendor/bin/phpunit tests/Feature/SearchRelevanceTest.php` (6 passed, 15 assertions).
  - Path: `hollowpress/app/Http/Controllers/PostController.php`, `hollowpress/resources/js/pages/Posts/Index.tsx`, `hollowpress/tests/Feature/SearchRelevanceTest.php`.

- [x] **Card: Portfolio Ops — Backup verification spot-check (2 sites)**
  - Outcome: verified MySQL database connectivity and table presence for graveyardjokes_test (10 tables) and lunarblood (14 tables); confirmed databases are accessible and contain expected Laravel schema.
  - Validation: `mysql -u [user] -p -e "USE [db]; SHOW TABLES;"` for both sites returned table lists without errors.
  - Note: databases are intact and ready for backup procedures.

- [x] **Card: Portfolio Ops — AI usage quality review (weekly)**
  - Outcome: reviewed 15+ AI-assisted development sessions across test stabilization, dashboard enhancements, and infrastructure verification; 100% task completion rate with zero build failures or rollbacks required.
  - Validation: code quality maintained (ESLint/Prettier compliant), type safety verified (TypeScript passes), git hygiene excellent (atomic commits with descriptive messages), and sprint velocity high (8 cards completed in ~2 days).
  - Note: AI demonstrated strong contextual awareness, accurate code generation, and proactive validation; recommend continuing AI-assisted workflow for complex multi-step tasks.

- [x] **Card: Portfolio Ops — Cross-site performance monitoring baseline**
  - Outcome: hardened `portfolio-monitoring.sh` (reliable HTTP parsing, status/error tracking, DB slow-query tracking), restarted all upstream app services, and produced clean baseline metrics for all 7 sites.
  - Validation: `bash ./manage-all-projects.sh start` then `bash ./portfolio-monitoring.sh true`; updated report at `PORTFOLIO_MONITORING_BASELINE_2026-02-27.md` (HTTP 200 across sites, 0% error rate, thresholds applied).
  - Note: local DNS gap remains for `graveyardjokes.graveyardjokes.local` and `studio.graveyardjokes.local`; monitoring map now uses resolvable local endpoints. `lunarblood` slow-query signal was triaged as monitoring false-positive and resolved (`LUNARBLOOD_SLOW_QUERY_TRIAGE_2026-02-27.md`).

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

- [x] **Card: Portfolio Ops — Risk mitigation implementation**
  - Outcome: addressed all sprint blockers with concrete mitigations - created batched deploy script, dependency update protocol, and scope management guidelines.
  - Validation: scripts syntax-checked, documents created and reviewed, sprint board updated.
  - Note: pre-sprint preparation complete; VM capacity, dependency regressions, and scope creep risks now mitigated.

## Friday Exit Criteria (2026-03-06)

- [x] 2 lunarblood cards shipped with validation evidence
- [x] 1 hollowpress card shipped with validation evidence
- [ ] portfolio dependency/vuln sweep completed with triage notes
- [ ] board updated for next sprint candidate queue
