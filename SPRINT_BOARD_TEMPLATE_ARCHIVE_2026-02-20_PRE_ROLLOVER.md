# Sprint Board (Execution View)

Use this as your weekly operating board for the 7-site portfolio.
Recommended WIP limit: **max 2 active build sites**.

Supporting planning content moved to `SPRINT_BOARD_APPENDIX_FEB_2026.md`.

## Current Sprint

- **Sprint Window:** 2026-02-23 → 2026-02-27
- **Primary Site:** lunarblood
- **Secondary Site:** hollowpress
- **Maintenance Sites:** graveyardjokes, synthveil, thevelvetpulse, velvetradio
- **R&D Site:** studio
- **Sprint Goal:** Start the next AI-assisted sprint with production-safe throughput: ship two lunarblood outcomes, one hollowpress outcome, and complete portfolio reliability checks.
- **Execution Mode:** AI-assisted micro-sprints (target 4-8h cards; split any card that exceeds 1 day; every AI-generated change requires human validation evidence).

## Today Snapshot

- **Last Updated:** 2026-02-20

- **Status:** 🟢 Next sprint ready to start (scope and sequencing prepared).
- **Carryover Posture:** No feature carryovers; prior sprint goals shipped.
- **AI Readiness:** Board now requires prompt trace + validation evidence for each AI-assisted card.
- **Open Risks:** VM capacity contention, regression risk from dependency churn, and AI over-generation (scope drift).
- **Next Focus:** Monday kickoff with locked queue only; enforce WIP limits and same-day validation on every completed card.
- **Kickoff Gate:** next sprint starts only if each `Now` card has clear acceptance + validation commands + rollback note.

## Locked Queue (Sprint Start)

- [ ] **Card (6h): lunarblood — User profile management baseline**
  - Status: 🟢 (Ready)
  - Owner: Joshua
  - Acceptance:
    - [ ] profile view/edit flow works for authenticated user
    - [ ] validation + error handling are consistent
    - [ ] security checks (authz + validation) pass
  - AI workflow:
    - [ ] prompt + output summary logged in sprint notes
    - [ ] human validation run before marking complete
  - Validation: `php artisan test --filter=Profile`, `npm run build`, and smoke check on profile routes.

- [ ] **Card (4h): lunarblood — Monitoring/error review cadence docs**
  - Status: 🟢 (Ready)
  - Owner: Joshua
  - Acceptance:
    - [ ] daily + weekly review schedule documented
    - [ ] log sources and severity thresholds defined
    - [ ] owner/escalation path captured
  - AI workflow:
    - [ ] AI-generated draft reviewed and trimmed for accuracy
    - [ ] commands/paths in doc verified locally
  - Validation: doc walkthrough + one dry-run checklist execution.

- [ ] **Card (6h): hollowpress — Search relevance monitoring + tuning follow-up**
  - Status: 🟢 (Ready)
  - Owner: Joshua
  - Acceptance:
    - [ ] monitored query set documented (top 10 terms)
    - [ ] ranking/pagination behavior verified and tuned where needed
    - [ ] no regressions in listing pages
  - AI workflow:
    - [ ] AI used to generate test-query matrix and tuning candidates
    - [ ] final relevance decisions approved by human review
  - Validation: scripted query checks + `npm run build` in `hollowpress`.

## Lane: Now (This Sprint Commitments)

RAG legend: `🟢 On track` | `🟠 At risk` | `🔴 Blocked`

### lunarblood (Primary)
- [ ] **Card: User profile management baseline**
  - Status: 🟢 (Ready)
  - Owner: Joshua
- [ ] **Card: Monitoring/error review cadence docs**
  - Status: 🟢 (Ready)
  - Owner: Joshua
- [ ] **Card: Production promotion checklist refresh**
  - Status: 🟢 (Ready)
  - Owner: Joshua
- [ ] **Card: Dashboard follow-up hardening (post-baseline)**
  - Status: 🟠 (At risk)
  - Owner: Joshua
  - Risk note: prioritize only if profile + docs cards finish early.

### hollowpress (Secondary)
- [ ] **Card: Search relevance monitoring + tuning follow-up**
  - Status: 🟢 (Ready)
  - Owner: Joshua
- [ ] **Card: Dashboard empty-state QA regression sweep**
  - Status: 🟢 (Ready)
  - Owner: Joshua


### Portfolio-wide Ops (All Sites)
- [ ] **Card: Monday dependency and vuln triage sweep**
  - Status: 🟢 (Ready)
  - Owner: Joshua
- [ ] **Card: Backup verification spot-check (two highest-risk sites)**
  - Status: 🟢 (Ready)
  - Owner: Joshua
- [ ] **Card: AI usage quality review (weekly)**
  - Status: 🟢 (Ready)
  - Owner: Joshua
  - Acceptance:
    - [ ] sample 5 AI-assisted commits/cards and score quality
    - [ ] track rework rate and false-positive suggestions
    - [ ] add 2 process adjustments for next sprint

## Blocked

- [ ] **Card: Test VM capacity bottleneck during parallel deploys**
  - Owner: Joshua
  - Impact: Shared VM can cause SSR/process contention during parallel deploys.
  - Mitigation: deploy in batches, restart services between batches, and capture resource usage snapshots.

- [ ] **Card: Dependency update introduces build/test regressions**
  - Owner: Joshua
  - Impact: Broad Composer/npm updates can break legacy assumptions and slow delivery.
  - Mitigation: update in project order, pin problematic packages, and keep rollback commands documented.

- [ ] **Card: Scope creep from non-priority feature requests**
  - Owner: Joshua
  - Impact: Requests from paused sites can consume primary sprint capacity.
  - Mitigation: enforce lane rules and route non-priority requests to Next/Deferred at planning review.

- [ ] **Card: Security findings exceed sprint capacity**
  - Owner: Joshua
  - Impact: Multi-site vulnerability volume may exceed planned sprint effort.
  - Mitigation: triage by severity, fix critical/high immediately, and schedule medium/low in maintenance.

## Done (This Sprint)

- [x] **Card: Previous sprint closeout + Friday ship gate**
  - Outcome: prior sprint outcomes shipped and kickoff readiness confirmed for next sprint window.

- [x] **Card: Backup restore path not validated end-to-end**
  - Outcome: restore rehearsal completed and evidence captured in sprint notes.

- [x] **Card: graveyardjokes composer advisory (firebase/php-jwt <7)**
  - Outcome: upgraded to `google/auth v1.50.0` + `firebase/php-jwt v7.0.2`; `composer audit` now returns `0` advisories.
  - Validation: `composer test` passes in `graveyardjokes` (`75 passed, 0 failed`).

- [x] **Card: graveyardjokes Vite startup error in dev logs**
  - Outcome: frontend dependencies reinstalled and project restarted; Vite startup error cleared.

- [x] **Card: lunarblood SSR log errors (missing assets + undefined helper)**
  - Outcome: SSR assets rebuilt and project restarted; SSR log scan returns no flagged errors.

- [x] **Card: studio/synthveil SSR invalid hook call errors**
  - Outcome: aligned SSR React resolution/dedupe config and reran checks; both projects clean.
