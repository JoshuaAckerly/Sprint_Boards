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

- **Last Updated:** 2026-02-21
- **Status:** 🟢 Planned and ready for Monday kickoff.
- **Carryover Posture:** Re-evaluate incomplete cards from 2026-02-27 closeout before kickoff lock.
- **Open Risks:** VM contention during deploys, dependency regressions, and scope drift from non-priority requests.
- **Kickoff Gate:** sprint starts only if each `Now` card has acceptance criteria + validation commands + rollback note.

## Locked Queue (Sprint Start)

- [ ] **Card (6h): lunarblood — User profile management baseline**
  - Status: 🟢 (Ready)
  - Owner: Joshua
  - Acceptance:
    - [ ] profile view/edit flow works for authenticated user
    - [ ] validation + error handling are consistent
    - [ ] authorization + endpoint checks pass
  - Validation: `php artisan test --filter=Profile`, `npm run build`, and route smoke check.

- [ ] **Card (4h): lunarblood — Production promotion checklist refresh**
  - Status: 🟢 (Ready)
  - Owner: Joshua
  - Acceptance:
    - [ ] pre-flight, deploy, and rollback steps are explicit
    - [ ] verification commands are included and tested
    - [ ] sign-off owner + timestamp fields added
  - Validation: checklist dry run in test environment.

- [ ] **Card (6h): hollowpress — Search relevance monitoring + tuning follow-up**
  - Status: 🟢 (Ready)
  - Owner: Joshua
  - Acceptance:
    - [ ] monitored query set documented (top 10 terms)
    - [ ] ranking/pagination behavior verified and tuned if needed
    - [ ] no listing regressions
  - Validation: scripted query checks + `npm run build` in `hollowpress`.

- [ ] **Card (4h): Portfolio Ops — Dependency/vulnerability triage sweep**
  - Status: 🟢 (Ready)
  - Owner: Joshua
  - Acceptance:
    - [ ] run Composer/npm audit pass on active/maintenance sites
    - [ ] critical/high issues triaged with owner and due date
    - [ ] rollback notes captured for risky updates
  - Validation: audit output archived in sprint notes.

## Lane: Now (This Sprint Commitments)

RAG legend: `🟢 On track` | `🟠 At risk` | `🔴 Blocked`

### lunarblood (Primary)
- [ ] **Card: User profile management baseline**
  - Status: 🟢 (Ready)
  - Owner: Joshua
- [ ] **Card: Production promotion checklist refresh**
  - Status: 🟢 (Ready)
  - Owner: Joshua
- [ ] **Card: Main dashboard functionality (post-MVP) — slice 1**
  - Status: 🟠 (At risk)
  - Owner: Joshua
  - Risk note: only start if top 2 lunarblood cards complete by mid-week.

### hollowpress (Secondary)
- [ ] **Card: Search relevance monitoring + tuning follow-up**
  - Status: 🟢 (Ready)
  - Owner: Joshua
- [ ] **Card: Dashboard regression sweep (empty states + quick actions)**
  - Status: 🟢 (Ready)
  - Owner: Joshua

### Portfolio-wide Ops
- [ ] **Card: Dependency/vulnerability triage sweep**
  - Status: 🟢 (Ready)
  - Owner: Joshua
- [ ] **Card: Backup verification spot-check (2 sites)**
  - Status: 🟢 (Ready)
  - Owner: Joshua
- [ ] **Card: AI usage quality review (weekly)**
  - Status: 🟢 (Ready)
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

- [ ] Add completed cards here with outcome + validation evidence.

## Friday Exit Criteria (2026-03-06)

- [ ] 2 lunarblood cards shipped with validation evidence
- [ ] 1 hollowpress card shipped with validation evidence
- [ ] portfolio dependency/vuln sweep completed with triage notes
- [ ] board updated for next sprint candidate queue
