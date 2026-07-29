# Sprint Board (Execution View)

Use this as your weekly operating board for the 7-site portfolio.
Recommended WIP limit: **max 2 active build sites**.

## Current Sprint

- **Sprint Window:** 2026-07-29 → 2026-08-04
- **Primary Site:** synthveil
- **Secondary Site:** Portfolio Ops (dependency audit)
- **Urgent / Ops:** studio (production thumbnail refresh)
- **Maintenance Sites:** graveyardjokes, hollowpress, lunarblood, thevelvetpulse, velvetradio, noteleks
- **Sprint Goal:** Ship synthveil real-time contact notifications (Reverb + Echo + admin badge); complete July dependency audit across all 9 projects; restore missing studio production thumbnails.
- **Execution Mode:** AI-assisted micro-sprints (target 4-8h cards; split any card that exceeds 1 day; every AI-generated change requires human validation evidence).

## Today Snapshot

- **Last Updated:** 2026-07-29
- **Status:** ⬜ Sprint not yet started
- **Carryover Posture:** Clean exit from May 30 sprint — 6/6 cards shipped. Two-month maintenance window covered guzzle security patch (all projects), noteleks PHP 8.4 + CI, auth-system CI overhaul, graveyardjokes eCommerce add-on.
- **Open Risks:** Reverb requires a WebSocket port open on the production server; confirm firewall rules before deploying. Studio thumbnail artisan commands must be run on the production server (not local).
- **Kickoff Gate:** All `Now` cards have acceptance criteria + validation commands.

## Locked Queue (Sprint Start)

- [ ] **Card A (~1h): studio — Production thumbnail refresh**
  - Owner: Joshua
  - Acceptance:
    - [ ] SSH into studio production server
    - [ ] `php artisan tiktok:fetch-thumbnails --force` exits 0; output confirms thumbnails fetched/cached
    - [ ] `php artisan gallery:fetch-thumbnails --force` exits 0; output confirms thumbnails fetched/cached
    - [ ] VideoLog page (`/video`) renders thumbnails without broken images
    - [ ] Illustrations page (`/illustrations`) renders cover images without broken images
  - Validation: manual browser check of `/video` and `/illustrations` on production; no broken image placeholders
  - Rollback: N/A (read-only cache refresh; thumbnails were already missing)

- [ ] **Card B (~6h): synthveil — Real-time contact notifications (admin dashboard)**
  - Owner: Joshua
  - Acceptance:
    - [ ] `laravel/reverb` installed and configured (`config/reverb.php`, `.env` keys: `REVERB_APP_ID`, `REVERB_APP_KEY`, `REVERB_APP_SECRET`, `REVERB_HOST`, `REVERB_PORT`, `REVERB_SCHEME`)
    - [ ] `App\Events\ContactSubmitted` event created — implements `ShouldBroadcast`, broadcasts on private channel `contacts` with `contact` payload (id, name, created_at)
    - [ ] `ContactController::store()` dispatches `ContactSubmitted::dispatch($contact)` after `Contact::create()`
    - [ ] `laravel-echo` + `pusher-js` installed as frontend devDependencies
    - [ ] Echo configured in `resources/js/app.tsx` (Reverb as the broadcaster)
    - [ ] `resources/js/hooks/useContactNotifications.ts` — subscribes to `private-contacts` channel; maintains `unreadCount` state; exposes `markAllRead()`
    - [ ] Admin dashboard (`resources/js/pages/admin/dashboard.tsx`) displays unread contact badge using the hook; badge increments in real-time on new submission without page refresh
    - [ ] `npx tsc --noEmit` clean (0 errors)
    - [ ] `npm run -s build` clean
    - [ ] `php artisan test` full suite green (no regressions)
  - Validation: `cd synthveil && npx tsc --noEmit && npm run -s build && php artisan test`; manual: open admin dashboard in one tab, submit contact form in another — badge count increments without refresh
  - Rollback: remove `ContactSubmitted` event; revert `ContactController::store()`; remove Echo config + hook; uninstall `laravel-echo`, `pusher-js`, `laravel/reverb`

- [ ] **Card C (~3h): Portfolio Ops — July 2026 dependency audit**
  - Owner: Joshua
  - Acceptance:
    - [ ] `npm audit --audit-level=high` run across all 9 projects; all high/critical findings triaged
    - [ ] `composer audit` run across all 9 projects; all high/critical findings triaged
    - [ ] Any actionable high/critical vulnerabilities patched and committed (per-project `fix(deps):` commits)
    - [ ] Findings documented in `docs/reports/2026-07/DEPENDENCY_AUDIT_2026-07-29.md` (project, severity, package, action taken)
    - [ ] All 9 project test suites still green after any patches applied
  - Validation: `npm audit --audit-level=high` and `composer audit` report 0 high/critical unresolved across all projects; report file exists
  - Rollback: `git checkout HEAD~1 -- package-lock.json composer.lock && npm install` (per-project if a patch causes regressions)

## Lane: Now (This Sprint Commitments)

RAG legend: `🟢 On track` | `🟠 At risk` | `🔴 Blocked`

### studio (Urgent Ops) — Target: thumbnails restored on production
- [ ] **Card A (~1h): Production thumbnail refresh**
  - Status: ⬜ Not started
  - Owner: Joshua

### synthveil (Primary) — Target: real-time notifications shipped
- [ ] **Card B (~6h): Real-time contact notifications (admin dashboard)**
  - Status: ⬜ Not started
  - Owner: Joshua

### Portfolio Ops (Secondary) — Target: July audit complete + report filed
- [ ] **Card C (~3h): July 2026 dependency audit**
  - Status: ⬜ Not started
  - Owner: Joshua

## Blocked

_(none at sprint start)_

## Done (This Sprint)

_(nothing yet)_

---

## Backlog (Not This Sprint)

Ordered by priority:

1. hollowpress — RSS feed (`/feed` XML route for blog posts)
2. lunarblood — Image optimization + lazy loading
3. lunarblood — File upload security review
4. lunarblood — Input sanitization review (controller-level)
5. lunarblood — Form component library
6. graveyardjokes — Google Places API production setup (add `GOOGLE_PLACES_API_KEY` + `GOOGLE_PLACES_PLACE_ID` to `.env`, `cache:clear`)
7. graveyardjokes — GBP API quota increase request (Google Cloud Console)
8. studio — Move Noteleks game to its own subdomain
9. noteleks — Update Studio legal pages for Noteleks game content
10. noteleks — Weapon system (spear class, skeleton hand attachment, weapon-specific attacks)
11. noteleks — Level geometry (platforms, obstacles, jumpable heights)
12. noteleks — Game UI (health bar, better score display)
13. noteleks — Sound effects (attacks, hits, deaths)
14. thevelvetpulse — Caching strategy for database queries
15. thevelvetpulse — Loading states + animations
16. synthveil — Real-time notifications (post-Reverb follow-up: toast alerts, notification history page)
17. velvetradio — User authentication + profiles
18. velvetradio — Automated backups
19. velvetradio — Icecast streaming integration (**blocked**: needs original music content)
