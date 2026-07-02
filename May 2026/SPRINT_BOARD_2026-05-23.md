# Sprint Board (Execution View)

Use this as your weekly operating board for the 7-site portfolio.
Recommended WIP limit: **max 2 active build sites**.

## Current Sprint

- **Sprint Window:** 2026-05-23 → 2026-05-29
- **Primary Site:** velvetradio
- **Secondary Site:** hollowpress
- **R&D / Commit Site:** noteleks
- **Maintenance Sites:** graveyardjokes, synthveil, thevelvetpulse, lunarblood
- **Sprint Goal:** Ship velvetradio live streaming foundation (Icecast + Liquidsoap config files + React wiring); hollowpress RSS feed; noteleks SpearSprite visual weapon attachment.
- **Execution Mode:** AI-assisted micro-sprints (target 4-8h cards; every AI-generated change requires human validation evidence).

## Today Snapshot

- **Last Updated:** 2026-05-21
- **Status:** ✅ All 3 cards shipped — Card A 2026-05-20, Card C 2026-05-21, Card B 2026-05-21
- **Carryover Posture:** No carryover from May 16-22 sprint — all 5 cards shipped. May 4-8 backlog fully resolved.
- **Open Risks:** None active. Card A fully deployed to EC2.
- **Kickoff Gate:** All cards have acceptance criteria + validation commands.

## Locked Queue (Sprint Start)

- [x] **Card A (~5h): velvetradio — Icecast + Liquidsoap streaming setup** ✅ 2026-05-20
  - Owner: Joshua
  - Acceptance:
    - [x] `config/icecast.xml` — Icecast server config committed to repo; mount point `/live`, passwords placeholdered for `.env` substitution, max-listeners set
    - [x] `config/radio.liq` — Liquidsoap script: fallback `.mp3` playlist from `storage/audio/fallback/`; live input on port 8001; outputs to Icecast `/live` mount
    - [x] `config/systemd/liquidsoap.service` — systemd unit file for auto-restart on crash
    - [x] `docs/NGINX_STREAMING_SETUP.md` — nginx proxy block documented (`location /stream { proxy_pass http://127.0.0.1:8000/live; }`)
    - [x] `resources/js/components/AudioPlayer.tsx` — updated: accepts optional `streamUrl` prop; when set, displays LIVE badge; works alongside existing episode player
    - [x] `resources/js/pages/listen.tsx` — imports AudioPlayer with `/stream` as streamUrl for live radio section
    - [x] `npx tsc --noEmit` clean (0 errors)
  - Validation: EC2 — `curl -s -m 3 -o /dev/null -w "%{http_code}" http://127.0.0.1:8087/stream` → **200**; Icecast admin shows `/live` + `/fallback` mounts active (Liquidsoap 2.2.4); `total_bytes_sent: 1568431` on `/live`
  - Deployed: 2026-05-20 to `ubuntu@3.19.68.125`

- [x] **Card B (~4h): hollowpress — RSS feed for blog** ✅ 2026-05-21
  - Owner: Joshua
  - Acceptance:
    - [x] `app/Http/Controllers/RssController.php` — returns `application/rss+xml`; latest 20 published posts; valid RSS 2.0 channel structure
    - [x] `routes/web.php` — `GET /feed.rss` → `RssController@feed`
    - [x] `resources/views/rss/feed.blade.php` — RSS 2.0 XML template: channel (title, description, link, language) + items (title, link, description, pubDate, guid)
    - [x] App layout `<head>` includes `<link rel="alternate" type="application/rss+xml" href="/feed.rss" title="Hollow Press">`
    - [x] `tests/Feature/RssFeedTest.php` — 3 tests: 200 status, Content-Type `application/rss+xml`, response body contains `<channel>` and at least one `<item>` when posts exist
    - [x] `./vendor/bin/phpunit` full suite green (0 regressions)
  - Validation: `./vendor/bin/phpunit` → 52 tests, 135 assertions, OK; `curl -sI https://hollowpress.graveyardjokes.com/feed.rss` → `HTTP/2 200`, `content-type: application/rss+xml; charset=UTF-8`
  - Deployed: 2026-05-21 to `ubuntu@3.19.68.125` (commit `3d8395a`)

- [x] **Card C (~4h): noteleks — SpearSprite + weapon visual attachment** ✅ 2026-05-21
  - Owner: Joshua
  - Acceptance:
    - [x] `resources/js/SpearSprite.js` — Phaser Image-based class; constructor takes `(scene, player)`; `update()` positions sprite offset from player based on facing direction; `destroy()` removes sprite from scene
    - [x] `WeaponManager.js` updated — instantiates `SpearSprite` on weapon creation; calls `spearSprite.update()` each frame in weapon update loop; calls `spearSprite.destroy()` on collision
    - [x] `resources/js/__tests__/SpearSprite.test.js` — 4+ tests: sprite created; correct offset for facing-right; correct offset for facing-left; destroy removes sprite from scene
    - [x] All Noteleks Jest suites pass: 22+ suites, 200+ tests (0 regressions)
  - Validation: `cd noteleks && npx jest --no-coverage` → 23 suites, 208 tests, all green
  - Deployed: 2026-05-21 to `ubuntu@3.19.68.125` (commit `127dc05`)

## Lane: In Progress

_(empty at sprint start)_

## Lane: Done

_(empty at sprint start)_

## Files Changed This Sprint

_(populated as cards ship)_
