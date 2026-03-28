# Data Model & SRS

## Core Tables

| Table | Purpose | Key Fields |
| --- | --- | --- |
| `users` | learner profile | id, handle, timezone, notification defaults |
| `user_language_tracks` | per-language configuration | id, user_id, language_name, qualifier, descriptor, cadence prefs, experience level |
| `language_grammar_factors` | curated grammar factors per language (checked into code + seeded to DB) | id, language_name, category, factor_key, description |
| `track_factor_selection` | per-track subset + status | track_id, language_factor_id, status, notes |
| `vocab_groups` | user-authored sets per track | id, track_id, description, tags, seed list |
| `vocab_items` | resolved tokens | group_id, text, lemma, metadata |
| `attempts` | exercise log | id, track_id, grammar_factor_id, vocab_group_id, generator_version, judge_version, prompt_blob, answer_blob |
| `judge_actions` | fine-grained decisions | attempt_id, action_type, payload |
| `srs_state` | decay metrics | entity_type (factor/group/item), entity_id, track_id, score, last_reviewed |

The key idea: we version and store the grammar/vocab factors ourselves when we add a language. LLMs can still suggest subsets, but the authoritative catalog ships with Mnemo.

## SRS Algorithm (v1)

- Each entity starts at score `0.3` (needs practice) within its track.
- After each attempt:
  - **Correct:** `score = min(1.0, score + α)`.
  - **Close:** `score = min(1.0, score + β)`.
  - **Incorrect:** `score = max(0.05, score - γ)`.
- Natural decay: `score *= e^{-λ * Δt_hours}` applied during scheduling.
- Scheduler targets entities whose effective score drops below track-specific thresholds.

We’ll iterate on α/β/γ/λ empirically and capture findings in the Journal.
