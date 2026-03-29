# System Components

## Web Interface (Axum + HTMX)
- Minimal pages: dashboard (track list + queues), configuration (language factors + vocab groups), practice screen.
- Keep it server-rendered for MVP; bots/mobile clients can come later once the HTTP surface stabilizes.

## LLM Orchestrator
- Two stateless prompt functions powered by `deterministic`:
  - **Generator** takes `(track_id, grammar_factor_id, vocab_group_id)` plus language metadata and returns one translation prompt + answer key.
  - **Judge** takes the prompt context + learner answer and emits a single verdict (no retries/state machines in MVP).
- Prompts live in `prompts/` alongside fixtures so we can spell out exactly what context we send and regression-test edits.

## Scheduler & Decay Engine
- Lightweight priority queue per track using the exponential decay math outlined in the Data Model chapter (start simple; evolve toward SM-2 if needed).
- Inputs: attempt history + the learner’s requested session length. No boosts or multi-step logic yet.
- Outputs the next `(grammar factor, vocab group)` pair whenever the user hits **Test Me**.

## Persistence Layer
- SQLite via `sqlx` to start.
- Tables cover: users, language_grammar_factors (curated in code), track_factor_selection, vocab_groups, vocab_items, attempts, judge_actions, srs_state, journal_entries.
- Migrations checked in; Postgres on Railway will use the same ones.

## Audit Trail (MVP)
- Basic request/response logging for LLM calls.
- Manual journal entries optional; auto-insights deferred until after the core loop is solid.
