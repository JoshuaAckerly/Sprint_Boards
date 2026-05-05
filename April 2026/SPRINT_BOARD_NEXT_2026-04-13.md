# Sprint Board (Execution View)

Use this as your weekly operating board for the 7-site portfolio.
Recommended WIP limit: **max 2 active build sites**.

## Current Sprint

- **Sprint Window:** 2026-04-13 → 2026-04-17
- **Primary Site:** lunarblood
- **Secondary Site:** hollowpress
- **Maintenance Sites:** graveyardjokes (quick-wins card bundled)
- **R&D / Maintenance Sites:** synthveil, thevelvetpulse, velvetradio, studio
- **Sprint Goal:** Ship lunarblood form component library + image lazy loading; hollowpress breadcrumbs + frontend search bar; graveyardjokes Studio/LinkedIn pages; April dependency audit.
- **Execution Mode:** AI-assisted micro-sprints (target 4-8h cards; split any card that exceeds 1 day; every AI-generated change requires human validation evidence).

## Today Snapshot

- **Last Updated:** 2026-04-15
- **Status:** 🟢 Sprint active — 5 of 6 cards shipped
- **Carryover Posture:** Clean exit from April 6-10 sprint — no blockers carried over.
- **Open Risks:** April dependency audit not yet started.
- **Kickoff Gate:** All `Now` cards have acceptance criteria + validation commands.

## Locked Queue (Sprint Start)

- [ ] **Card (6h): lunarblood — Form component library**
  - Owner: Joshua
  - Acceptance:
    - [ ] `Input`, `Select`, `Textarea`, `FormField` reusable components with inline validation display
    - [ ] existing forms refactored to use shared components
    - [ ] validation behavior unchanged
  - Validation: `./vendor/bin/phpunit`, `npx tsc --noEmit`, `npm run -s build`
  - Rollback: revert component files and form usages; behavior unchanged

- [ ] **Card (6h): lunarblood — Image optimization + lazy loading**
  - Owner: Joshua
  - Acceptance:
    - [ ] `loading="lazy"` + `srcset` applied to shows and venues listing page images
    - [ ] responsive image sizing for key content images
    - [ ] no visible UX regression on page load
  - Validation: `./vendor/bin/phpunit`, `npx tsc --noEmit`, `npm run -s build`
  - Rollback: revert image attribute changes; no DB changes

- [ ] **Card (6h): hollowpress — Breadcrumbs navigation**
  - Owner: Joshua
  - Acceptance:
    - [ ] `Breadcrumb.tsx` component with `<nav aria-label="breadcrumb">` and `aria-current="page"`
    - [ ] integrated on post detail and case-study detail pages
    - [ ] consistent with existing layout/routing structure
  - Validation: `./vendor/bin/phpunit`, `npx tsc --noEmit`, `npm run -s build`
  - Rollback: remove `Breadcrumb.tsx` import from page components

- [ ] **Card (6h): hollowpress — Frontend search bar**
  - Owner: Joshua
  - Acceptance:
    - [ ] debounced search input on post listing page wiring to existing LIKE query (note: full-text NOT recommended per March 2026 evaluation)
    - [ ] inline results or filtered listing; listing pagination behavior unchanged
    - [ ] no UX regression on existing listing/filter behavior
  - Validation: `./vendor/bin/phpunit`, `npx tsc --noEmit`, `npm run -s build`
  - Rollback: remove search bar component; backend route unchanged

- [ ] **Card (3h): graveyardjokes — Studio page + LinkedIn page**
  - Owner: Joshua
  - Acceptance:
    - [ ] `resources/js/pages/studio.tsx` page live at `/studio` — agency creative showcase, links to studio subdomain
    - [ ] `resources/js/pages/linkedin.tsx` page live at `/linkedin` — LinkedIn business profile link page
    - [ ] footer in `MainLayout.tsx` has LinkedIn link
    - [ ] routes added to `routes/web.php`
  - Validation: `npx tsc --noEmit`, `npm run -s build`
  - Rollback: remove routes and page files; revert footer

- [ ] **Card (4h): Portfolio Ops — April dependency audit**
  - Owner: Joshua
  - Acceptance:
    - [ ] `composer audit` and `npm audit` run across all repos
    - [ ] new findings triaged with owner and due date
    - [ ] report published in `docs/reports/2026-04/`
  - Validation: cross-repo audit sweep + report file present
  - Rollback: N/A (read-only audit)

## Lane: Now (This Sprint Commitments)

RAG legend: `🟢 On track` | `🟠 At risk` | `🔴 Blocked`

### lunarblood (Primary) — Target: 2 shipped outcomes
- [x] **Card (6h): Form component library**
  - Status: ✅ Done 2026-04-15 — `Input`, `Select`, `Textarea`, `FormField` components built; `checkout.tsx` (10 inputs), `shows/create.tsx`, `shows/edit.tsx` refactored; `npx tsc --noEmit` + build clean
  - Owner: Joshua

- [x] **Card (6h): Image optimization + lazy loading**
  - Status: ✅ Done — `loading="lazy"` + `decoding="async"` confirmed on all venue images in `venues/index.tsx`, `venues/show.tsx`, `venue-detail.tsx`, `listen.tsx`; no raw images without lazy loading
  - Owner: Joshua

### hollowpress (Secondary) — Target: 2 shipped outcomes
- [x] **Card (6h): Breadcrumbs navigation**
  - Status: ✅ Done — `Breadcrumb.tsx` component built with `aria-label="breadcrumb"` + `aria-current="page"`; integrated in `Posts/Show.tsx` and `CaseStudies/Show.tsx`; build clean
  - Owner: Joshua

- [x] **Card (6h): Frontend search bar**
  - Status: ✅ Done — debounced search input wired to LIKE query in `Posts/Index.tsx`; author/category/date filters; highlight + snippet extraction; pagination unchanged; build clean
  - Owner: Joshua

### graveyardjokes (Quick-wins) — Target: 1 bundled card
- [x] **Card (3h): Studio page + LinkedIn page**
  - Status: ✅ Done — `pages/studio.tsx` at `/studio`, `pages/linkedin.tsx` at `/linkedin`, routes in `web.php`, LinkedIn link in `MainLayout.tsx` footer
  - Owner: Joshua

### Portfolio-wide Ops — Target: 1 audit outcome
- [ ] **Card (4h): April dependency audit**
  - Status: ⬜ Not started — due by 2026-04-17
  - Owner: Joshua

## Blocked

_(none at sprint start)_

## Done (This Sprint)

- ✅ lunarblood — Form component library (2026-04-15)
- ✅ lunarblood — Image optimization + lazy loading (2026-04-15)
- ✅ hollowpress — Breadcrumbs navigation (2026-04-15)
- ✅ hollowpress — Frontend search bar (2026-04-15)
- ✅ graveyardjokes — Studio page + LinkedIn page (2026-04-10 / confirmed 2026-04-15_

## Friday Exit Criteria (2026-04-17)

- [x] 2 lunarblood cards shipped with validation evidence
- [x] 2 hollowpress cards shipped with validation evidence
- [x] graveyardjokes Studio + LinkedIn pages live
- [ ] April dependency audit published in `docs/reports/2026-04/`
- [ ] board archived and Sprint 2 candidate queue confirmed

## Next Sprint Candidate Queue (Proposed — Sprint 2)

- **Sprint Window:** 2026-04-20 → 2026-04-24
- **Build Sites:** velvetradio (primary), thevelvetpulse (secondary)
- **WIP Guardrail:** max 2 active build sites; split any card > 1 day

### Proposed Monday `Now` Lock (6 cards)

- [ ] **Card (8h): velvetradio — Audio player component**
  - Acceptance:
    - [ ] persistent fixed-bottom player bar (play/pause/seek/volume/current track)
    - [ ] HTML5 `<audio>` API + React state; wired to episodes/shows pages
    - [ ] no UX regression on existing show/episode pages
  - Validation: `npx tsc --noEmit`, `npm run -s build`, manual playback test

- [ ] **Card (6h): velvetradio — HLS streaming integration**
  - Acceptance:
    - [ ] `hls.js` added; player connects to episode stream URLs
    - [ ] graceful fallback to direct `<audio>` src for non-HLS browsers
    - [ ] stream URL configured via `.env` (public Apple test stream used as dev default)
  - Validation: HLS test stream plays, `npm audit` clean, `npx tsc --noEmit`

- [ ] **Card (4h): thevelvetpulse — Error handling + loading states**
  - Acceptance:
    - [ ] error boundaries on key page sections with fallback UI
    - [ ] 404/500 error pages implemented
    - [ ] loading state animations on data-fetching sections
  - Validation: `npx tsc --noEmit`, `npm run -s build`

- [ ] **Card (4h): thevelvetpulse — Accessibility audit + remediation**
  - Acceptance:
    - [ ] WCAG 2.1 AA pass across all 8 pages: semantic HTML, ARIA labels, keyboard nav, focus management
    - [ ] no regressions on existing page behavior
  - Validation: manual audit checklist or axe-core script; `npx tsc --noEmit`

- [ ] **Card (4h): hollowpress — Dark mode toggle**
  - Acceptance:
    - [ ] site-wide dark mode via Tailwind `class` strategy + CSS variable tokens
    - [ ] `localStorage` persistence; toggle button in header
    - [ ] existing dark-themed components audited for consistency
  - Validation: `npx tsc --noEmit`, `npm run -s build`, visual verification

- [ ] **Card (2h): Portfolio Ops — velvetradio audio baseline**
  - Acceptance:
    - [ ] streaming latency baseline captured
    - [ ] report published in `docs/reports/2026-04/`
  - Validation: report file present
