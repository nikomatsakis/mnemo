# Data Model & SRS

## Core Tables

| Table | Purpose | Key Fields |
| --- | --- | --- |
| `users` | learner profile | id, handle, timezone, notification defaults |
| `user_language_tracks` | per-language configuration | id, user_id, language_name, qualifier, descriptor, cadence prefs, experience level |
| `grammar_concepts` | canonical catalog per language family | slug, title, description, language, difficulty, tags |
| `user_grammar_status` | per-track progress | track_id, concept_id, status, notes |
| `vocab_groups` | user-authored sets per track | id, track_id, description, tags, seed list |
| `vocab_items` | resolved tokens | group_id, text, lemma, metadata |
| `attempts` | exercise log | id, track_id, generator_version, judge_version, prompt_blob, answer_blob |
| `judge_actions` | fine-grained decisions | attempt_id, action_type, payload |
| `srs_state` | decay metrics | entity_type (grammar/vocab/item), entity_id, track_id, score, last_reviewed |

We keep language-specific seed data in `grammar_concepts`, so the onboarding flow can ask the LLM to propose a concept subset for any language + descriptor.

## SRS Algorithm (v1)

- Each entity starts at score `0.3` (needs practice) within its track.
- After each attempt:
  - **Correct:** `score = min(1.0, score + α)`.
  - **Close:** `score = min(1.0, score + β)`.
  - **Incorrect:** `score = max(0.05, score - γ)`.
- Natural decay: `score *= e^{-λ * Δt_hours}` applied during scheduling.
- Scheduler targets entities whose effective score drops below track-specific thresholds.

We’ll iterate on α/β/γ/λ empirically and capture findings in the Journal.
