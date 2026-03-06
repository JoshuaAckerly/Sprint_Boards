# Sprint Boards Repository

This repository contains sprint planning and tracking documents for the 7-site portfolio management system.

## Structure

- `SPRINT_BOARD_NEXT_*.md`: Current active sprint board
- `SPRINT_BOARD_TEMPLATE_*.md`: Sprint planning templates
- `SPRINT_BOARD_APPENDIX_*.md`: Supporting documentation and appendices
- `SPRINT_BOARD_TEMPLATE_ARCHIVE_*.md`: Archived templates for reference
- `SPRINT_BOARD_ARCHIVE_*.md`: Archived completed sprint execution boards

## Latest Archives

- `SPRINT_BOARD_ARCHIVE_2026-03-16_TO_2026-03-20.md`
- `SPRINT_BOARD_ARCHIVE_2026-03-09_TO_2026-03-13.md`
- `SPRINT_BOARD_ARCHIVE_2026-03-02_TO_2026-03-06.md`

## Monthly Rollups

- Archived weeks total: **62h locked / 76h delivered / +14h variance**.
- April 2026 placeholder: **0h locked / 0h delivered / 0h variance** (update after first April archive).

## Current Active Board

- `SPRINT_BOARD_NEXT_2026-03-03.md`

## Recent Updates

- **2026-03-06:** Added completed graveyardjokes pre-payment intake + checkout gate execution notes and validation evidence to `SPRINT_BOARD_ARCHIVE_2026-03-02_TO_2026-03-06.md` and `SPRINT_BOARD_NEXT_2026-03-03.md`.
- **2026-03-03:** Added April 2026 monthly rollup placeholder line in `README.md` for next-month tracking readiness.
- **2026-03-03:** Added March archived-weeks workload rollup to `README.md` (62h locked / 76h delivered / +14h variance).
- **2026-03-03:** Realigned active sprint board timeline to current week and added workload-by-week projection flow in `SPRINT_BOARD_NEXT_2026-03-03.md`.
- **2026-03-01:** Added Synthveil public UX reliability completion entry (loading/error handling, search/filtering, pagination, URL-state persistence) to `SPRINT_BOARD_NEXT_2026-03-23.md`.
- **2026-03-01:** Mirrored the same Synthveil completion entry into `SPRINT_BOARD_TEMPLATE_FEB_2026.md` for consistency.
- **2026-03-01:** Synced task completion state in `synthveil/TODO.md` for loading/error handling, search/filtering, and pagination.

## Usage

1. Clone this repository to maintain sprint history across different database environments
2. Copy the current template to create new sprint boards
3. Update the "NEXT" board with current sprint commitments
4. Archive completed sprints by renaming them appropriately

## Sprint Methodology

- **Sprint Window**: Weekly cycles (Sunday start)
- **WIP Limit**: Maximum 2 active build sites
- **Execution Mode**: AI-assisted micro-sprints (target 4-8h cards)
- **Quality Gates**: Every AI-generated change requires human validation

## Portfolio Sites

- graveyardjokes (primary maintenance)
- lunarblood (primary development)
- hollowpress (secondary development)
- synthveil (maintenance)
- thevelvetpulse (maintenance)
- velvetradio (maintenance)
- studio (R&D)
- auth-system (infrastructure)

## Contributing

- Keep sprint boards updated with real-time status
- Document validation evidence for all completed cards
- Archive completed sprints with outcome summaries