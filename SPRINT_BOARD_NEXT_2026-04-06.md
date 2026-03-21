# Sprint Board (Execution View)

Use this as your weekly operating board for the 7-site portfolio.
Recommended WIP limit: **max 2 active build sites**.

## Current Sprint

- **Sprint Window:** 2026-04-06 → 2026-04-10
- **Primary Site:** lunarblood
- **Secondary Site:** hollowpress
- **Maintenance Sites:** graveyardjokes, synthveil, thevelvetpulse, velvetradio
- **R&D Site:** studio
- **Sprint Goal:** Ship one lunarblood UX polish outcome (loading states), one hollowpress content-discovery feature, and one portfolio-ops reliability checkpoint with validation evidence.
- **Execution Mode:** AI-assisted micro-sprints (target 4-8h cards; split any card that exceeds 1 day; every AI-generated change requires human validation evidence).

## Today Snapshot

- **Last Updated:** 2026-03-21
- **Status:** 🟡 Draft — pending Monday kickoff gate review.
- **Carryover Posture:** Continue evidence-first discipline. velvetradio P95 resolved (578ms → 28ms), verify sustained improvement in next monitoring pass.
- **Open Risks:** dependency regressions during updates, scope creep from maintenance requests.
- **Kickoff Gate:** sprint starts only if each `Now` card has acceptance criteria + validation commands + rollback note.

## Locked Queue (Sprint Start)

- [ ] **Card (6h): lunarblood — Loading states & skeleton screens (dashboard + key pages)**
  - Owner: Joshua
  - Acceptance:
    - [ ] loading/skeleton states added to dashboard, shows index, and venues index pages
    - [ ] skeleton states match page layout to prevent content layout shift
    - [ ] existing page behavior and data loading unaffected
  - Validation: `./vendor/bin/phpunit`, `npx tsc --noEmit`, `npm run -s build`
  - Rollback: revert new skeleton components and page-level loading state changes

- [ ] **Card (6h): lunarblood — Toast notification system + error boundaries**
  - Owner: Joshua
  - Acceptance:
    - [ ] reusable toast notification component with success/error/info variants
    - [ ] React error boundary wrapping key page sections with fallback UI
    - [ ] flash message integration with Inertia shared data
  - Validation: `./vendor/bin/phpunit`, `npx tsc --noEmit`, `npm run -s build`
  - Rollback: revert toast component, error boundary wrapper, and Inertia middleware changes

- [ ] **Card (6h): hollowpress — Related posts feature (content discovery)**
  - Owner: Joshua
  - Acceptance:
    - [ ] related posts section on post detail page (tag/category-based matching)
    - [ ] graceful handling when no related posts exist
    - [ ] listing/search/pagination behavior unchanged
  - Validation: `./vendor/bin/phpunit tests/Feature/SearchRelevanceTest.php`, `npx tsc --noEmit`, `npm run -s build`
  - Rollback: revert controller changes and remove related posts component

- [ ] **Card (4h): Portfolio Ops — Post-fix monitoring validation (velvetradio + cross-site)**
  - Owner: Joshua
  - Acceptance:
    - [ ] velvetradio warm-path P95 confirmed ≤100ms (sustained post-fix)
    - [ ] cross-site endpoint timing snapshot refreshed
    - [ ] checkpoint note published under `docs/reports/2026-04/`
  - Validation: `bash ./scripts/portfolio-monitoring.sh true` (warm pass), report in `docs/reports/2026-04/`
  - Rollback: N/A (read-only monitoring)

## Lane: Now (This Sprint Commitments)

RAG legend: `🟢 On track` | `🟠 At risk` | `🔴 Blocked`

### lunarblood (Primary) - Target: 2 shipped outcomes
- [ ] **Card (6h): Loading states & skeleton screens (dashboard + key pages)**
  - Status: 🟢 On track
  - Owner: Joshua

- [ ] **Card (6h): Toast notification system + error boundaries**
  - Status: 🟢 On track
  - Owner: Joshua

### hollowpress (Secondary) - Target: 1 shipped outcome
- [ ] **Card (6h): Related posts feature (content discovery)**
  - Status: 🟢 On track
  - Owner: Joshua

### Portfolio-wide Ops - Target: 1 reliability outcome
- [ ] **Card (4h): Post-fix monitoring validation (velvetradio + cross-site)**
  - Status: 🟢 On track
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

## Done (This Sprint)

_(empty — sprint not started)_

## Friday Exit Criteria (2026-04-10)

- [ ] 2 lunarblood cards shipped with validation evidence
- [ ] 1 hollowpress card shipped with validation evidence
- [ ] post-fix monitoring checkpoint published with velvetradio confirmation
- [ ] board archived and next sprint candidate queue seeded

## Next Sprint Candidate Queue (Proposed)

- **Sprint Window:** 2026-04-13 → 2026-04-17
- **Build Sites:** lunarblood (primary), hollowpress (secondary)
- **WIP Guardrail:** max 2 active build sites; split any card > 1 day

### Proposed Monday `Now` Lock (4 cards)

- [ ] **Card (6h): lunarblood — Image optimization + lazy loading**
  - Acceptance:
    - [ ] lazy loading for images on shows/venues listing pages
    - [ ] responsive image sizing or srcset for key content images
    - [ ] no visible UX regression on page load
  - Validation: `./vendor/bin/phpunit`, `npx tsc --noEmit`, `npm run -s build`

- [ ] **Card (6h): hollowpress — Breadcrumbs navigation**
  - Acceptance:
    - [ ] breadcrumb component on post detail, case-study detail, and nested pages
    - [ ] accessible markup (nav + aria attributes)
    - [ ] consistent with existing layout/routing structure
  - Validation: `./vendor/bin/phpunit`, `npx tsc --noEmit`, `npm run -s build`

- [ ] **Card (6h): lunarblood — Form component library (reusable inputs + validation)**
  - Acceptance:
    - [ ] reusable form input components (text, select, textarea) with validation display
    - [ ] existing forms refactored to use shared components
    - [ ] validation behavior unchanged
  - Validation: `./vendor/bin/phpunit`, `npx tsc --noEmit`, `npm run -s build`

- [ ] **Card (4h): Portfolio Ops — April dependency audit checkpoint**
  - Acceptance:
    - [ ] composer/npm audits rerun across all portfolio repos
    - [ ] new findings triaged with owner and due date
    - [ ] April evidence published
  - Validation: cross-repo audit sweep + report in `docs/reports/2026-04/`
