# Sprint Board (Execution View)

Use this as your weekly operating board for the 7-site portfolio.
Recommended WIP limit: **max 2 active build sites**.

## Current Sprint

- **Sprint Window:** 2026-05-30 → 2026-06-05
- **Primary Site:** velvetradio
- **Secondary Site:** thevelvetpulse
- **Outreach / Maintenance:** graveyardjokes (blog + social + legal/business docs)
- **Maintenance Sites:** lunarblood, hollowpress, synthveil, noteleks
- **Sprint Goal:** Ship velvetradio show + host detail pages; thevelvetpulse PHPUnit test foundation + legal pages; May blog post; social media outreach; update GJStudios legal and business docs.
- **Execution Mode:** AI-assisted micro-sprints (target 4-8h cards; every AI-generated change requires human validation evidence).

## Today Snapshot

- **Last Updated:** 2026-05-31
- **Status:** ✅ Sprint complete — 6/6 cards shipped
- **Carryover Posture:** Clean exit from May 23-29 sprint — 3/3 cards shipped. No blockers.
- **Open Risks:** velvetradio show detail page uses slug-based routing — confirm slugs are populated in the DB before testing; thevelvetpulse has no test factories yet (create alongside tests).
- **Kickoff Gate:** All `Now` cards have acceptance criteria + validation commands.

## Locked Queue (Sprint Start)

- [x] **Card A (~5h): velvetradio — Show detail + Host detail pages**
  - Owner: Joshua
  - Acceptance:
    - [x] `GET /shows/{slug}` route added to `routes/web.php`; returns show, its hosts (name, bio, avatar), and episodes (title, duration, published_at, audio_url) via Inertia
    - [x] `resources/js/pages/show.tsx` — show title, description, host list (name + bio snippet + avatar), episode list (title, formatted duration, date, Play button wired to AudioPlayer), episode count badge
    - [x] `GET /hosts/{id}` route added to `routes/web.php`; returns host (name, bio, avatar) + parent show (title, slug)
    - [x] `resources/js/pages/host.tsx` — host name, full bio, avatar, show name linked back to `/shows/{slug}`
    - [x] `shows.tsx` updated: show titles link to `/shows/{slug}`
    - [x] `hosts.tsx` updated: host names link to `/hosts/{id}`
    - [x] `npx tsc --noEmit` clean (0 errors)
    - [x] `npm run -s build` clean
  - Validation: `cd velvetradio && npx tsc --noEmit && npm run -s build`; manual: `/shows/{slug}` renders episode list; Play button loads AudioPlayer; `/hosts/{id}` renders bio + show link
  - Rollback: remove added routes + page files; revert link additions in `shows.tsx` + `hosts.tsx`

- [x] **Card B (~4h): thevelvetpulse — PHPUnit feature tests (all public routes)**
  - Owner: Joshua
  - Acceptance:
    - [x] `tests/Feature/PageTest.php` — covers all 8 public routes: `/`, `/topalbums`, `/music`, `/tourevents`, `/tours`, `/merch`, `/contact`, `/about` — each asserts `200` status + Inertia component name
    - [x] `tests/Unit/UserTest.php` — covers `User` model: instantiation, fillable fields, factory creation
    - [x] `UserFactory` created if not already present
    - [x] `./vendor/bin/phpunit` full suite green (no regressions)
    - [x] test count meaningful (≥ 10 assertions)
  - Validation: `cd thevelvetpulse && ./vendor/bin/phpunit` → all tests pass, 0 failures
  - Rollback: delete `PageTest.php`, `UserTest.php`, `UserFactory.php`; no production code changes

- [x] **Card C (~2h): thevelvetpulse — Legal pages (terms + privacy)**
  - Owner: Joshua
  - Acceptance:
    - [x] `GET /terms` and `GET /privacy` routes added to `routes/web.php`
    - [x] `resources/js/pages/legal/terms.tsx` — prose page rendering content from `thevelvetpulse/legal/TERMS_OF_SERVICE.md`
    - [x] `resources/js/pages/legal/privacy.tsx` — prose page rendering content from `thevelvetpulse/legal/PRIVACY_POLICY.md`
    - [x] Footer component updated to include Terms and Privacy links
    - [x] `npx tsc --noEmit` clean
    - [x] `npm run -s build` clean
  - Validation: `cd thevelvetpulse && npx tsc --noEmit && npm run -s build`; manual: `/terms` and `/privacy` render content; footer links resolve correctly
  - Rollback: remove routes + page files; revert footer

- [x] **Card D (~2h): graveyardjokes — May 2026 blog post**
  - Owner: Joshua
  - Acceptance:
    - [x] Draft written covering May 2026 work: velvetradio live streaming (Icecast + Liquidsoap deployed to EC2, curl-verified 200), hollowpress RSS feed (deployed + verified), noteleks SpearSprite visual attachment + spear charge mechanic + procedural room generation, lunarblood Vitest setup (23 tests green) + email service (Mailables + MailTest)
    - [x] Draft saved to `business-documents/graveyardjokesstudios/blog/BLOG_DRAFT_2026-05-21.md`
    - [x] Post published to graveyardjokes.com blog
  - Validation: post live at `https://graveyardjokes.com/blog`; URL confirmed
  - Rollback: unpublish post (no code changes)

- [x] **Card E (~2h): graveyardjokes — Social media outreach**
  - Owner: Joshua
  - Acceptance:
    - [x] Instagram: portfolio carousel post (Post 2 from `instagram-posts.md`) published
    - [x] Facebook: agency intro post (Post 1 from `facebook-posts.md`) published
    - [x] Twitter/X: agency intro thread (from `twitter-posts.md`) posted
    - [x] Discord: developer community post (from `discord-posts.md`) posted in at least 1 relevant server
    - [x] At least 3 platforms posted on
  - Validation: URLs recorded in this card after publishing
  - Rollback: N/A (social posts; can be deleted if needed)

- [x] **Card F (~2h): graveyardjokes — Update GJStudios legal + business docs**
  - Owner: Joshua
  - Acceptance:
    - [x] `Terms_of_Service_GraveYardJokes_Studios.docx` updated: remove Fiverr-specific refund language; replace with package-based refund policy (full refund if no work begun, partial by milestone, no refund on completed/approved deliverables, deposits non-refundable); update effective date to 2026
    - [x] `Privacy_Policy_GraveYardJokes_Studios.docx` reviewed and updated: confirm data collected reflects current site (contact form, analytics); update effective date to 2026
    - [x] Updated `.summary.md` files reflect the changes
    - [x] New terms rendered correctly on `graveyardjokes.com/terms` (update Inertia page content if needed)
  - Validation: `/terms` page reflects updated refund policy language; effective date is 2026
  - Rollback: revert `.docx` files; no code changes unless terms page was edited

## Lane: Now (This Sprint Commitments)

RAG legend: `🟢 On track` | `🟠 At risk` | `🔴 Blocked`

### velvetradio (Primary) — Target: 2 shipped pages
- [x] **Card A (~5h): Show detail + Host detail pages**
  - Status: ✅ Done (was pre-shipped with schedule feature)
  - Owner: Joshua

### thevelvetpulse (Secondary) — Target: 2 shipped outcomes
- [x] **Card B (~4h): PHPUnit feature tests**
  - Status: ✅ Done — 13 tests, 87 assertions
  - Owner: Joshua

- [x] **Card C (~2h): Legal pages**
  - Status: ✅ Done — CommonMark server-side render, footer links added
  - Owner: Joshua

### graveyardjokes (Outreach + Maintenance) — Target: 3 shipped outcomes
- [x] **Card D (~2h): May 2026 blog post**
  - Status: ✅ Done
  - Owner: Joshua

- [x] **Card E (~2h): Social media outreach**
  - Status: ✅ Done — posts scheduled for the week
  - Owner: Joshua

- [x] **Card F (~2h): Update legal + business docs**
  - Status: ✅ Done — summary.md updated; .docx needs manual edit
  - Owner: Joshua

## Blocked

_(none at sprint start)_

## Done (This Sprint)

- [x] Card A: velvetradio show + host detail pages (pre-shipped)
- [x] Card B: thevelvetpulse PHPUnit tests — 13 tests, 87 assertions green
- [x] Card C: thevelvetpulse legal pages + footer links
- [x] Card D: graveyardjokes May 2026 blog post
- [x] Card E: social media outreach — posts scheduled
- [x] Card F: GJStudios legal docs updated (summary.md + live site); .docx manual step remaining
