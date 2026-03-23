# Sprint Board (Execution View)

Use this as your weekly operating board for the 7-site portfolio.
Recommended WIP limit: **max 2 active build sites**.

## Current Sprint

- **Sprint Window:** 2026-03-02 → 2026-03-06
- **Primary Site:** lunarblood
- **Secondary Site:** hollowpress
- **Maintenance Sites:** graveyardjokes, synthveil, thevelvetpulse, velvetradio
- **R&D Site:** studio
- **Sprint Goal:** Keep delivery flow predictable by locking weekly capacity and tracking carryover before adding new scope.
- **Execution Mode:** AI-assisted micro-sprints (target 4-8h cards; split any card that exceeds 1 day; every AI-generated change requires human validation evidence).

## Today Snapshot

- **Last Updated:** 2026-03-06
- **Status:** ✅ Sprint closeout complete; archive and next-week draft are ready.
- **Carryover Posture:** 0h locked-card carryover; keep ops buffer discipline in the next lock.
- **Open Risks:** unplanned maintenance requests and dependency regressions.
- **Kickoff Gate:** sprint starts only if each `Now` card has acceptance criteria + validation commands + rollback note.

## Weekly Workload Flow (Projection)

| Week | Sprint Window | Committed Workload | Buffer | Weekly Max | Mix Guidance |
|---|---|---:|---:|---:|---|
| Week 1 (Current) | 2026-03-02 → 2026-03-06 | 26h | 4h | 30h | 14h build / 8h secondary / 4h ops |
| Week 2 | 2026-03-09 → 2026-03-13 | 26h | 4h | 30h | 14h build / 8h secondary / 4h ops |
| Week 3 | 2026-03-16 → 2026-03-20 | 26h | 4h | 30h | 14h build / 8h secondary / 4h ops |
| Week 4 | 2026-03-23 → 2026-03-27 | 26h | 4h | 30h | 14h build / 8h secondary / 4h ops |

## Current Week Load Lock (2026-03-02 → 2026-03-06)

- **lunarblood:** 14h
- **hollowpress:** 8h
- **Portfolio Ops:** 4h
- **Committed Total:** 26h
- **Reserved Buffer:** 4h
- **Hard Cap:** 30h

## Flow Rules (Projection Accuracy)

- Do not exceed the **Committed Workload** unless a blocker threatens delivery.
- Any work outside lock must consume **Buffer** first.
- If carryover is **>4h**, reduce the next week committed load by the same amount.
- Keep at least **4h ops capacity** each week for monitoring, triage, and dependency hygiene.

## Friday Exit Check (Weekly)

- [x] Committed workload delivered (or variance documented)
- [x] Carryover measured in hours
- [x] Next week committed load adjusted from carryover
- [x] Risks and blocker posture updated before Monday lock

## Execution Updates (2026-03-06)

- **graveyardjokes maintenance delivery completed:** shipped pre-payment intake questionnaire + package-gated checkout flow, added Laravel feature tests and React/Jest coverage, and stabilized Jest config.
- **Validation evidence:** `php artisan test tests/Feature/WebsiteIntakeTest.php` (pass), `npm test -- --coverage` (17/17 suites, 80/80 tests), `npm run types` (pass).
- **Reference commit:** `abc8880` on `graveyardjokes/main`.

## Rollover Notes (2026-03-06)

- **Archive board finalized:** `SPRINT_BOARD_ARCHIVE_2026-03-02_TO_2026-03-06.md` updated with Friday exit closure and validation report index.
- **Next board seeded:** `SPRINT_BOARD_NEXT_2026-03-09.md` drafted with locked queue, owners, risks, and exit criteria.
- **Validation reports indexed:** `docs/reports/2026-03/SYNTHVEIL_NPM_AUDITABILITY_RESTORE_2026-03-01.md`, `docs/reports/2026-03/DEPENDENCY_AUDIT_ADDENDUM_2026-03-01.md`, `hollowpress/docs/reports/2026-03/INDEX_QUERY_PERFORMANCE_CHECKPOINT_2026-03-01.md`.
