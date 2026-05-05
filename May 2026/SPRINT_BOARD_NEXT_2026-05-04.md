# Sprint Board (Execution View)

Use this as your weekly operating board for the 7-site portfolio.
Recommended WIP limit: **max 2 active build sites**.

## Current Sprint

- **Sprint Window:** 2026-05-04 → 2026-05-08
- **Primary Site:** lunarblood
- **Secondary Site:** hollowpress
- **Wildcard / R&D Sites:** velvetradio (streaming architecture), studio (Noteleks mechanics)
- **Maintenance Sites:** graveyardjokes, synthveil, thevelvetpulse
- **Sprint Goal:** Ship lunarblood automated test foundation (PHPUnit feature tests + Vitest setup); hollowpress newsletter subscription full stack; velvetradio streaming architecture decision doc; studio Noteleks spear mechanics + room generation; graveyardjokes LinkedIn social posts.
- **Execution Mode:** AI-assisted micro-sprints (target 4-8h cards; split any card that exceeds 1 day; every AI-generated change requires human validation evidence).

## Today Snapshot

- **Last Updated:** 2026-05-05
- **Status:** ✅ Sprint closed 2026-05-05 — 5/6 cards shipped (studio Noteleks deferred to next sprint)
- **Carryover Posture:** Full carryover from April 27 sprint — 0/5 cards shipped. The April 20 and April 27 sprints were both unstarted (life circumstances, not scope rot). All 5 original cards remain valid and scoped with no changes needed.
- **Open Risks:** Vitest install may require vite.config.ts restructure; hollowpress newsletter needs DB migration run before testing.
- **Kickoff Gate:** All `Now` cards have acceptance criteria + validation commands.

## Locked Queue (Sprint Start)

- [ ] **Card (5h): lunarblood — PHPUnit feature tests: Shows + Venues CRUD**
  - Owner: Joshua
  - Acceptance:
    - [ ] `tests/Feature/ShowTest.php` covers: list, show, create, update, delete + validation failures
    - [ ] `tests/Feature/VenueTest.php` covers: list, show, create, update, delete + validation failures
    - [ ] uses `ShowFactory`, `VenueFactory`, `UserFactory` (already exist)
    - [ ] all tests pass; no regressions in existing suite
  - Validation: `./vendor/bin/phpunit --filter ShowTest`, `./vendor/bin/phpunit --filter VenueTest`, `./vendor/bin/phpunit` full suite clean
  - Rollback: delete `ShowTest.php` and `VenueTest.php`; no production code changes

- [ ] **Card (5h): lunarblood — Vitest setup + React component tests**
  - Owner: Joshua
  - Acceptance:
    - [ ] `vitest`, `@testing-library/react`, `@testing-library/jest-dom`, `jsdom` installed as devDependencies
    - [ ] `test` block added to `vite.config.ts` (environment: jsdom, setupFiles pointing to test setup)
    - [ ] tests written for `Input`, `Select`, `Textarea`, `FormField`, `Toast` components
    - [ ] `npx vitest run` all green
    - [ ] `npx tsc --noEmit` + `npm run -s build` still clean after config change
  - Validation: `npx vitest run`, `npx tsc --noEmit`, `npm run -s build`
  - Rollback: remove devDependencies + test config + test files; revert `vite.config.ts`

- [x] **Card (hollowpress — Newsletter subscription (UX demo)** ✅ 2026-05-05
  - Owner: Joshua
  - Scope revised: pure UX demo — form submits, shows success state, no DB writes (portfolio showcase)
  - Acceptance:
    - [x] `NewsletterForm.tsx` React component with loading → success state ✅ (pre-existing)
    - [x] routes: `POST /newsletter/subscribe` responds with JSON success ✅
    - [x] controller: rate-limited, validates email, returns simulated success — no DB dependency
    - [x] `npx tsc --noEmit` clean ✅
    - [x] `npm run -s build` clean ✅
  - Validation: tsc + build green; form submit → success state rendered
  - Rollback: revert `NewsletterController::subscribe()` to previous version

- [ ] **Card (3h): velvetradio — Streaming architecture document**
  - Owner: Joshua
  - Acceptance:
    - [ ] document covers: Icecast+Liquidsoap, HLS (self-hosted), and WebRTC options
    - [ ] each option has: infrastructure requirements, complexity, cost, trade-offs
    - [ ] clear recommendation with rationale for velvetradio use case
    - [ ] published to `docs/reports/2026-04/VELVETRADIO_STREAMING_ARCHITECTURE.md`
  - Validation: file present and recommendation section complete
  - Rollback: N/A (documentation only)

- [ ] **Card (5h): studio — Noteleks: spear mechanics + room generation**
  - Owner: Joshua
  - Acceptance:
    - [ ] spacebar hold charges spear (visual charge indicator)
    - [ ] spacebar release throws spear (projectile follows aimed direction)
    - [ ] new room layout generated procedurally each session (floor/wall tiles)
    - [ ] browser console clean (no errors on load or during gameplay)
  - Validation: manual browser test — spear fires on spacebar release; room layout differs between page reloads; console clean
  - Rollback: revert spear input handler and room gen files to previous state

- [x] **Card (2h): graveyardjokes — LinkedIn social media promotional posts** ✅ 2026-05-05
  - Owner: Joshua
  - Acceptance:
    - [x] 1–2 LinkedIn posts drafted promoting GJStudios services (web dev, web design, digital marketing)
    - [x] posts reference graveyardjokes.com
    - [x] at least one post published live on LinkedIn
    - [x] optional: repurpose May 4 blog post ("Still Here") as content hook / teaser
  - Validation: https://www.linkedin.com/feed/update/urn:li:activity:7457477662379384832
  - Rollback: N/A (social post; can be deleted if needed)

## Lane: Now (This Sprint Commitments)

RAG legend: `🟢 On track` | `🟠 At risk` | `🔴 Blocked`

### lunarblood (Primary) — Target: 2 shipped outcomes
- [x] **Card (5h): PHPUnit feature tests: Shows + Venues CRUD** ✅
  - Status: ✅ Shipped 2026-05-05
  - Owner: Joshua

- [x] **Card (5h): Vitest setup + React component tests** ✅
  - Status: ✅ Shipped 2026-05-05 (pre-implemented; verified 23/23 tests green)
  - Owner: Joshua

### hollowpress (Secondary) — Target: 1 shipped outcome
- [x] **Card: Newsletter subscription (UX demo)** ✅
  - Status: ✅ Shipped 2026-05-05 (scope revised to portfolio UX demo)
  - Owner: Joshua

### velvetradio (Wildcard) — Target: 1 architecture decision doc
- [x] **Card (3h): Streaming architecture document** ✅
  - Status: ✅ Shipped 2026-05-05
  - Owner: Joshua

### studio (R&D) — Target: 1 gameplay mechanics outcome
- [ ] **Card (5h): Noteleks — Spear mechanics + room generation**
  - Status: ⬜ Not started
  - Owner: Joshua

### graveyardjokes (Maintenance + Outreach) — Target: 1 published LinkedIn post
- [x] **Card (2h): LinkedIn promotional posts** ✅
  - Status: ✅ Shipped 2026-05-05
  - Owner: Joshua

## Blocked

_(none at sprint start)_

## Done (This Sprint)

- ✅ **lunarblood — PHPUnit feature tests: Shows + Venues CRUD** (2026-05-05) — 59/59 suite green; `ShowTest.php` + `VenueTest.php` both pass
- ✅ **lunarblood — Vitest setup + React component tests** (2026-05-05) — 23/23 Vitest green; tsc + build clean
- ✅ **velvetradio — Streaming architecture document** (2026-05-05) — `docs/reports/2026-04/VELVETRADIO_STREAMING_ARCHITECTURE.md`; recommendation: Icecast + Liquidsoap
- ✅ **graveyardjokes — LinkedIn promotional posts** (2026-05-05) — https://www.linkedin.com/feed/update/urn:li:activity:7457477662379384832
- ✅ **hollowpress — Newsletter subscription (UX demo)** (2026-05-05) — `NewsletterController::subscribe()` returns simulated success; no DB; rate-limited + validated; tsc + build clean
