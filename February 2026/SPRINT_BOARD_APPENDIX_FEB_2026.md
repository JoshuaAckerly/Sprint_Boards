# Sprint Board Appendix (Planning + Templates)

This appendix stores planning/backlog/reference material that was moved out of the execution board.
Use `SPRINT_BOARD_TEMPLATE_FEB_2026.md` for daily execution (`Now`, `Blocked`, `Done`).

## Update Rule

- Refresh `Last Updated` in `SPRINT_BOARD_TEMPLATE_FEB_2026.md` whenever any card status changes.

## Timeline Mode (AI-Assisted)

- Planning horizon: 3 weeks (not 6 weeks) before re-ranking.
- Card SLA: 4-8 hours; split any card that exceeds 1 day.
- WIP: max 2 build sites, max 4 active cards total.
- AI output rule: treat AI output as draft until human validation evidence is captured.
- Evidence rule: every completed AI-assisted card must include prompt intent, verification commands, and final decision note.

## Lane: Next (Ready, Not Started)

### hollowpress
- [x] **Card (4h): Dashboard v1 polish + empty-state QA**
  - Acceptance:
    - [x] empty states render cleanly for zero posts/case studies
    - [x] quick-action links verified
    - [x] `npm run build` passes
  - Completed: 2026-02-18
- [x] **Card (6h): Search relevance tuning (`/posts`, `/case-studies`)**
  - Acceptance:
    - [x] top 10 search cases return expected ordering
    - [x] pagination + query persistence verified
    - [x] no regressions in list rendering
  - Completed: 2026-02-18
- [x] **Card (4h): Listing performance pass**
  - Acceptance:
    - [x] remove obvious over-render/duplicate query patterns
    - [x] keep initial list page responsive on realistic dataset
    - [x] document before/after notes in sprint log
  - Completed: 2026-02-18
  - Before/after notes:
    - Before: `/posts` merged full datasets in PHP memory before manual pagination.
    - After: `/posts` uses DB-level union, relevance ordering, and pagination; `case-studies` index now selects only columns needed for listing.

### lunarblood
- [ ] **Card (6h): Main dashboard functionality (post-MVP)**
  - Acceptance:
    - [ ] key dashboard widgets render with real data
    - [ ] loading/error states present
    - [ ] route + smoke checks pass
- [ ] **Card (8h): User profile management baseline**
  - Acceptance:
    - [ ] profile view/edit flow works
    - [ ] validation errors handled cleanly
    - [ ] security checks for update endpoint complete
- [ ] **Card (4h): Search functionality baseline**
  - Acceptance:
    - [ ] searchable entity scope defined and implemented
    - [ ] no-result + loading states present
    - [ ] smoke + basic edge-case checks pass
- [x] **Card (4h): API documentation outline**
  - Acceptance:
    - [x] endpoint inventory captured
    - [x] auth/validation/error patterns documented
    - [x] draft committed to docs folder
  - Completed: 2026-02-18
- [ ] **Card (3h): Monitoring/error review cadence docs**
  - Acceptance:
    - [ ] daily/weekly check schedule defined
    - [ ] log sources and alert thresholds listed
    - [ ] ownership/escalation path documented
- [ ] **Card (3h): Production promotion checklist**
  - Acceptance:
    - [ ] pre-flight, deploy, and rollback steps listed
    - [ ] verification commands included
    - [ ] sign-off owner + timestamp fields added

## Lane: Maintenance (Bug/Security/Infra Only)

### graveyardjokes
- [ ] Backup verification
- [ ] Security patch pass
- [ ] API response-time monitoring review

### synthveil
- [ ] Security baseline (CSRF/rate-limit/validation verification)
- [ ] Deployment hygiene review

### thevelvetpulse
- [ ] Error handling/logging baseline
- [ ] Security review + headers verification

### velvetradio
- [ ] Document streaming architecture options
- [ ] Keep non-streaming feature work paused

### studio (R&D)
- [ ] Continue Noteleks refactor milestones only
- [ ] Keep out of growth-delivery commitments

## Lane: Deferred (Intentionally Not This Cycle)

- [ ] Multi-language support across sites
- [ ] PWA initiatives
- [ ] Broad social/newsletter/comment systems across multiple sites
- [ ] New major platform features outside lunarblood/hollowpress scope
- [ ] lunarblood: real-time notifications and advanced interaction systems
- [ ] lunarblood: long-term architecture shifts (plugin system / microservices)
- [ ] lunarblood: mobile app development track

## Weekly Cadence (AI-Assisted)

### Monday (Plan, 45-60 min)
- Date: 2026-02-23
- Lock top 3 deliverables for lunarblood/hollowpress
- Pre-write AI prompts per card (goal, constraints, output format)
- Re-validate maintenance-only boundaries for other sites

### Tuesday-Thursday (Build + Verify)
- Date: 2026-02-24 to 2026-02-26
- Two focused execution blocks/day (60-90 min each)
- Validate each completed card immediately (build/routes/smoke + AI output review)
- Triage defects same day; carry only if explicitly re-scoped

### Friday (Ship + Review, 60 min)
- Date: 2026-02-27
- Production deploy window
- Review errors/performance/throughput + AI quality metrics
- Select next sprint cards from `Next`

## Monday Kickoff Checklist (2026-02-23)

Use this block to start the sprint fast without scope drift.

### 0) Timebox
- Total: 60 minutes
- Block A: 20 min (scope lock)
- Block B: 25 min (AI prep + execution plan)
- Closeout: 15 min (risk + evidence readiness)

### 1) Lock This Sprint’s Active Work (20 min)
- [ ] Confirm only 2 build sites are active: `lunarblood`, `hollowpress`
- [ ] Lock top 3 `Now` cards (no extra feature adds)
- [ ] Move all non-priority requests to `Next` or `Deferred`
- [ ] Confirm each `Now` card has owner + acceptance criteria

### 2) AI-Assist Prep (25 min)
- [ ] Write prompt intent for each `Now` card (goal, constraints, output shape)
- [ ] Add validation commands for each card (build/tests/routes/smoke)
- [ ] Predefine rollback/mitigation note for higher-risk cards
- [ ] Set expected card size to 4-8h; split any card >1 day

### 3) Evidence and Risk Gate (15 min)
- [ ] Confirm logging/monitoring paths to review after each completion
- [ ] Confirm dependency/security sweep slot on Monday/Tuesday
- [ ] Confirm how AI output will be captured in sprint notes
- [ ] Mark kickoff complete only when all `Now` cards are evidence-ready

### Kickoff Success Criteria
- [ ] Scope is locked and WIP limits are explicit
- [ ] Top 3 cards are AI-ready and validation-ready
- [ ] First execution block can begin immediately after kickoff

## Daily Execution Checklist (Tue-Thu)

Use once per day during 2026-02-24 to 2026-02-26.

### 0) Timebox
- Total: 90-120 minutes per execution cycle
- Block A: 45-60 min (implement one card slice)
- Block B: 30-45 min (validate + document evidence)
- Closeout: 10-15 min (status and next card decision)

### 1) Start-of-Block Gate
- [ ] Confirm current card is in `Now` and still within sprint scope
- [ ] Confirm acceptance criteria are unchanged and explicit
- [ ] Confirm AI prompt includes constraints and expected output format
- [ ] Confirm no more than 2 active build sites and 4 active cards total

### 2) Build (AI-Assisted)
- [ ] Generate one scoped change only (avoid multi-feature output)
- [ ] Review AI output before applying (security, correctness, scope)
- [ ] Apply change and keep commit/card notes concise
- [ ] If scope grows, split card before continuing

### 3) Validate Immediately
- [ ] Run card-specific validation commands
- [ ] Run smoke check for touched route/flow
- [ ] Review logs/errors for touched area
- [ ] Record observed result (pass/fail + short note)

### 4) Evidence Capture
- [ ] Save prompt intent summary (goal/constraints)
- [ ] Save commands executed and outcomes
- [ ] Note any rollback/mitigation if risk increased
- [ ] Update board status (`🟢`, `🟠`, `🔴`) and next action

### 5) End-of-Day Closeout
- [ ] Close completed cards only after validation evidence exists
- [ ] Move partial work to next day with clear first step
- [ ] Log one AI process improvement (prompt, guardrail, or test step)
- [ ] Confirm Friday ship review inputs are up to date

## AI Prompt Template Pack

Use these as copy/paste starters. Keep prompts short, scoped, and validation-first.

### 1) Feature Card Prompt
- **Goal:** Implement [feature slice] for [site/app area].
- **Constraints:** Stay within this card only; no unrelated refactors; keep current style/patterns.
- **Acceptance criteria:**
  1. [criterion]
  2. [criterion]
  3. [criterion]
- **Required output:**
  - Minimal code changes
  - List of files changed
  - Validation commands to run
  - Risks/rollback note

### 2) Bugfix Card Prompt
- **Goal:** Fix [bug] in [route/component/service].
- **Symptoms/evidence:** [error/log/steps to reproduce].
- **Constraints:** Root-cause fix only; do not add new features.
- **Acceptance criteria:**
  1. Repro no longer fails
  2. Adjacent behavior unchanged
  3. Relevant tests/checks pass
- **Required output:**
  - Root cause summary
  - Exact fix applied
  - Validation + regression checks
  - Rollback steps if needed

### 3) Docs/Process Card Prompt
- **Goal:** Draft/update [doc/checklist/runbook] for [scope].
- **Constraints:** Use only verified commands/paths; avoid speculative content.
- **Acceptance criteria:**
  1. Steps are executable and ordered
  2. Owners/escalation noted
  3. Verification commands included
- **Required output:**
  - Final doc structure
  - Command/path verification list
  - Open questions requiring human decision

### Prompt Footer (append to any template)
- “If uncertain, list assumptions explicitly before proposing changes.”
- “Do not mark complete without validation evidence.”
- “Prefer smallest viable change that meets acceptance criteria.”

## Filled Prompt Examples (Current Top 3 Cards)

### Example A — lunarblood: User profile management baseline
- **Goal:** Implement the user profile management baseline in lunarblood (view + edit for authenticated user).
- **Constraints:** Limit changes to profile flow only; no unrelated UI refactors; follow existing Laravel + frontend patterns.
- **Acceptance criteria:**
  1. Authenticated users can view and update profile fields.
  2. Validation and error states are clear and consistent.
  3. Authorization and endpoint validation checks pass.
- **Required output:**
  - Minimal file changes only
  - Changed file list
  - Validation commands: `php artisan test --filter=Profile`, `npm run build`
  - Risk/rollback note
- **Prompt footer:**
  - If uncertain, list assumptions before changing code.
  - Do not mark complete without validation evidence.
  - Prefer smallest viable change.

### Example B — lunarblood: Monitoring/error review cadence docs
- **Goal:** Draft/update monitoring cadence documentation for lunarblood operations.
- **Constraints:** Only include commands/paths that can be verified; avoid speculative monitoring claims.
- **Acceptance criteria:**
  1. Daily/weekly schedule is explicit.
  2. Log sources, thresholds, and escalation owner are listed.
  3. Verification commands/checklist are included.
- **Required output:**
  - Final doc outline
  - Verified command/path list
  - Open questions for human decision
- **Prompt footer:**
  - If uncertain, list assumptions before drafting.
  - Do not mark complete without command/path verification.
  - Keep wording concise and operational.

### Example C — hollowpress: Search relevance monitoring + tuning follow-up
- **Goal:** Improve and verify search relevance behavior for `/posts` and `/case-studies` in hollowpress.
- **Constraints:** Keep scope to relevance/pagination behavior; no unrelated feature additions.
- **Acceptance criteria:**
  1. Top query set is documented and replayable.
  2. Ranking/pagination behavior is verified and tuned where needed.
  3. Listing pages remain regression-free.
- **Required output:**
  - Query matrix + expected outcomes
  - Proposed tuning changes (minimal)
  - Validation commands: query checks + `npm run build`
  - Rollback note for tuning changes
- **Prompt footer:**
  - If uncertain, state assumptions before tuning.
  - Do not mark complete without validation evidence.
  - Prefer smallest viable adjustment set.

## Wednesday Kickoff Checklist (Completed Snapshot)

### 0) Timebox
- Total: 2 to 2.5 hours
- Block A: 75 min
- Break: 10 min
- Block B: 50 min
- Closeout: 15 min

### 1) Pick Today’s Cards (10-15 min)
- [x] `lunarblood` — **Card: Lock MVP scope (3-4 outcomes only)**
- [x] `Portfolio-wide Ops` — **Card: Dependency security updates across all sites**
- [x] `Portfolio-wide Ops` — **Card: Monitoring/log review after deploy**

### 2) Block A (90 min)
- [x] Finish `lunarblood` MVP scope lock card
- [x] Move all non-MVP requests to `Next` or `Deferred`
- [x] Update card status to 🟢 / 🟠 / 🔴

### 3) Block B (60 min)
- [x] Run dependency/security pass across portfolio and capture findings
- [x] Log breakages/pins and remediation outcomes
- [x] Add blockers to `Blocked` with mitigation and close resolved items

### 4) Closeout (20 min)
- [x] Update RAG status for all touched cards
- [x] Add notes under touched cards (changes and next steps)
- [x] Confirm next card sequence for continuation

### Success Criteria for Today
- [x] MVP scope locked for `lunarblood`
- [x] Dependency/security pass completed and risks identified
- [x] Board statuses updated with resolved blockers moved to `Done`

## Definition of Done (Per Card)

- [ ] Code complete and lint/tests pass for changed area
- [ ] Deployed to test environment
- [ ] QA checklist passed
- [ ] Monitoring/logs reviewed post-deploy
- [ ] Documentation/notes updated where needed
- [ ] AI prompt intent + output summary captured (if AI was used)
- [ ] Human verification evidence captured (commands and observed result)
- [ ] Rollback or mitigation note added for risky changes

## Scoring Check (Use at Sprint End)

Rate each active site 1-5 and compare trend weekly:

- **Impact delivered:** _/5
- **Stability:** _/5
- **Delivery speed:** _/5
- **Risk posture:** _/5

If primary site average < 3 for 2 consecutive sprints, re-rank priorities.

## Copyable Card Template

### [Site] Card Title
- **Owner:**
- **Why now:**
- **AI assist plan (optional):**
  - Prompt goal:
  - Constraints:
  - Expected output:
- **Acceptance criteria:**
  - [ ]
  - [ ]
- **Validation commands:**
  - [ ]
  - [ ]
- **Dependencies:**
- **Risk:** Low / Medium / High

## Friday 60-Second Review

Use this at the end of Friday review to decide what ships, what carries, and what gets cut.

| Metric | Value |
|---|---|
| Planned cards in `Now` | 14 |
| Completed cards this sprint | 14 |
| Carryover cards to next sprint | 0 |
| Cards moved to `Deferred` | 5 |
| New blockers added | 4 |

### Friday Precheck (2026-02-18)
- **Evidence readiness:** verified core reports/artifacts are present (`smoke`, `log review`, SSR verification, Vite fix, Hollowpress npm/composer audits).
- **Blocker posture:** no material blocker-category changes since last update; existing 4 blockers remain risk-management carries.
- **Decision readiness:** Friday meeting can focus on ship/carry/cut and next sprint lock (no additional discovery pass required).

### Ship / Carry / Cut (Prefill)
- **Ship:** lunarblood MVP baseline outcomes; hollowpress MVP baseline outcomes; portfolio ops baseline (security/backup/smoke/log review).
- **Carry:** active risk-management blockers (VM contention, dependency regression guardrails, scope-control governance, security-capacity balancing).
- **Cut:** non-priority feature requests not tied to flagship MVP traction (remain in `Deferred`).

### Quick Prompts
- What shipped to production this week?
- What did not ship, and why?
- What is the single biggest risk for next week?
- Which one card should be cut if capacity drops?

### Next Sprint Lock (fill before ending Friday)
- **Primary site:** lunarblood
- **Secondary site:** hollowpress
- **Top 3 `Now` cards:**
  1. lunarblood — User profile management baseline (6h)
  2. lunarblood — Monitoring/error review cadence docs (4h)
  3. hollowpress — Search relevance monitoring + tuning follow-up (6h)

### AI Quality Metrics (track each Friday)
- % of AI-assisted cards accepted without major rework
- Average validation time per AI-assisted card
- Number of AI-suggested changes reverted within 48h
- Top 2 prompt/template improvements for next sprint
