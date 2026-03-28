# System Components

## Web Interface (Axum + HTMX/Leptos-lite)
- Serves HTML pages for dashboard, configuration, practice screen.
- Exposes JSON endpoints consumed by a future Telegram bot.

## LLM Orchestrator
- Defines two main agents:
  - **GeneratorAgent**: builds exercises from grammar + vocab focus.
  - **JudgeAgent**: evaluates responses, can trigger helper tools (ask retry, hint, rephrase request).
- Agents are versioned; prompts live in `prompts/` with unit tests using mock fixtures.

## Scheduler & Decay Engine
- Background task recomputes priorities per user.
- Inputs: attempt history, target cadence, manual boosts (“drill accusative today”).
- Outputs: queue entries for practice sessions.

## Persistence Layer
- SQLite via `sqlx` for MVP; schema easily portable to Postgres.
- Tables for users, grammar_concepts, vocab_groups, vocab_items, attempts, judge_actions, srs_state.
- Uses migrations (`sqlx migrate`) checked into repo.

## Telemetry & Journal Hooks
- Tracing instrumentation to watch LLM latency and scheduler behavior.
- Journal entries automatically capture key events (new concept unlocked, major streak, prompt regressions) so humans can audit progress.
