# Discord Feedback Manager

> **Portfolio showcase — production source is private and this repository is intentionally non-runnable.**

Player feedback collection and staff triage system with persistent panels and SQLite storage.

## What it demonstrates

- Feedback modal up to 4000 characters
- Compact feedback headlines
- SQLite persistence
- Private staff triage
- Keep-for-patch/reject decisions
- Automatic panel recovery

## Technology

Python • discord.py • aiosqlite • Persistent Views • Async Tasks

## High-level workflow

1. Player opens feedback form
2. Store normalized feedback
3. Send to private staff channel
4. Staff triages item
5. Persist decision and clean working queue

## Public interface preview

The public skeleton exposes only the architectural surface:

- `submit_feedback(...)`
- `create_feedback_record(...)`
- `triage_feedback(...)`
- `restore_panel(...)`

The production implementations behind these methods are withheld. See [`NOTICE.md`](NOTICE.md).

## Repository contents

- `src/public_interface.py` — non-runnable interface skeleton;
- `docs/ARCHITECTURE.md` — high-level design;
- `examples/config.example.jsonc` — sanitized configuration shape;
- `LICENSE` — explicit all-rights-reserved notice.

## Status

Production-tested private project / portfolio edition.
