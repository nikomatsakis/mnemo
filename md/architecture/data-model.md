# Data Model & SRS

## Core Tables

| Table | Purpose | Key Fields |
| --- | --- | --- |
| `users` | learner profile | id, handle, timezone, cadence prefs |
| `grammar_concepts` | canonical catalog | slug, title, description, difficulty, tags |
| `user_grammar_status` | per-user progress | user_id, concept_id, status, notes |
| `vocab_groups` | user-authored sets | id, user_id, description, tags, seed list |
| `vocab_items` | resolved tokens | group_id, text, lemma, metadata |
| `attempts` | exercise log | id, user_id, generator_version, judge_version, prompt_blob, answer_blob |
| `judge_actions` | fine-grained decisions | attempt_id, action_type, payload |
| `srs_state` | decay metrics | entity_type (grammar/vocab/item), entity_id, score, last_reviewed |

## SRS Algorithm (v1)

- Each entity starts at score `0.3` (needs practice).
- After each attempt:
  - **Correct:** `score = min(1.0, score + α)`.
  - **Close:** `score = min(1.0, score + β)`.
  - **Incorrect:** `score = max(0.05, score - γ)`.
- Natural decay: `score *= e^{-λ * Δt_hours}` applied during scheduling.
- Scheduler targets entities whose effective score drops below user-defined thresholds.

We’ll iterate on α/β/γ/λ empirically and capture findings in the Journal.
