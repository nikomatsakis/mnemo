# System Components

## Web Interface (Axum + HTMX)
- Minimal pages: dashboard (track list + queues), configuration (language factors + vocab groups), practice screen.
- Keep it server-rendered for MVP; bots/mobile clients can come later once the HTTP surface stabilizes.

## LLM Orchestrator
- Two agents:
  - **Generator**: accepts `(track_id, grammar_factor_id, vocab_group_id)` and returns a translation prompt + answer key.
  - **Judge**: scores the learner response, optionally offering a single retry.
- Prompts live in `prompts/` with fixtures so we can regression-test prompt edits.

## Scheduler & Decay Engine
- Lightweight priority queue per track.
- Inputs: attempt history + target cadence. No fancy boosts yet—just “pick the lowest score”.
- Outputs the next `(grammar factor, vocab group)` pair when the learner requests a drill.

## Persistence Layer
- SQLite via `sqlx` to start.
- Tables cover: users, language_grammar_factors (curated in code), track_factor_selection, vocab_groups, vocab_items, attempts, judge_actions, srs_state, journal_entries.
- Migrations checked in; Postgres migration comes later if needed.

## Audit Trail (MVP)
- Basic request/response logging for LLM calls.
- Manual journal entries optional; auto-insights deferred until after the core loop is solid.
