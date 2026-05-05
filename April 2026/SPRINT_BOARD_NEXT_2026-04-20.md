# Sprint Board (Execution View)

Use this as your weekly operating board for the 7-site portfolio.
Recommended WIP limit: **max 2 active build sites**.

## Current Sprint

- **Sprint Window:** 2026-04-20 → 2026-04-24
- **Primary Site:** lunarblood
- **Secondary Site:** hollowpress
- **Wildcard / R&D Sites:** velvetradio (streaming architecture), studio (Noteleks mechanics)
- **Maintenance Sites:** graveyardjokes, synthveil, thevelvetpulse
- **Sprint Goal:** Ship lunarblood automated test foundation (PHPUnit feature tests + Vitest setup); hollowpress newsletter subscription full stack; velvetradio streaming architecture decision doc; studio Noteleks spear mechanics + room generation.
- **Execution Mode:** AI-assisted micro-sprints (target 4-8h cards; split any card that exceeds 1 day; every AI-generated change requires human validation evidence).

## Today Snapshot

- **Last Updated:** 2026-04-20
- **Status:** ⬜ Sprint not yet started
- **Carryover Posture:** Clean exit from April 13-17 sprint — 5/5 build cards shipped; April dependency audit closed April 17. No blockers carried over.
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

- [ ] **Card (6h): hollowpress — Newsletter subscription (full stack)**
  - Owner: Joshua
  - Acceptance:
    - [ ] `NewsletterSubscriber` model with `email`, `subscribed_at`, `unsubscribe_token` fields
    - [ ] migration creates `newsletter_subscribers` table
    - [ ] `NewsletterController`: `subscribe()` (validate + dedup) and `unsubscribe()` (token-based)
    - [ ] routes: `POST /newsletter/subscribe`, `GET /newsletter/unsubscribe/{token}`
    - [ ] `NewsletterForm.tsx` React component with inline success / error state
    - [ ] email via log driver (no external service this sprint)
    - [ ] no UX regression on existing pages
  - Validation: `./vendor/bin/phpunit`, `npx tsc --noEmit`, `npm run -s build`; manual: subscribe form submits + shows success; duplicate submit shows error; unsubscribe link invalidates token
  - Rollback: delete model/migration/controller/component; remove routes; roll back migration

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

## Lane: Now (This Sprint Commitments)

RAG legend: `🟢 On track` | `🟠 At risk` | `🔴 Blocked`

### lunarblood (Primary) — Target: 2 shipped outcomes
- [ ] **Card (5h): PHPUnit feature tests: Shows + Venues CRUD**
  - Status: ⬜ Not started
  - Owner: Joshua

- [ ] **Card (5h): Vitest setup + React component tests**
  - Status: ⬜ Not started
  - Owner: Joshua

### hollowpress (Secondary) — Target: 1 shipped outcome
- [ ] **Card (6h): Newsletter subscription (full stack)**
  - Status: ⬜ Not started
  - Owner: Joshua

### velvetradio (Wildcard) — Target: 1 architecture decision doc
- [ ] **Card (3h): Streaming architecture document**
  - Status: ⬜ Not started
  - Owner: Joshua

### studio (R&D) — Target: 1 gameplay mechanics outcome
- [ ] **Card (5h): Noteleks — Spear mechanics + room generation**
  - Status: ⬜ Not started
  - Owner: Joshua

## Blocked

_(none at sprint start)_

## Done (This Sprint)

_(nothing yet)_
