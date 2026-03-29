# Data Retention & Multi-user Plan

## Per-user Data Retained (MVP)

| Category | Details | Notes |
| --- | --- | --- |
| Profile | `user_id`, display name, primary email (+ optional secondary emails), password hash, native language, timezone | Stored in `users`. Admin can reset passwords or lock sign-ups. |
| Grammar roadmap | Enabled factors + status + notes | Stored in `track_factor_selection`. Notes stay plain text for easy export. |
| Vocabulary | Areas + generated words (with shared word table) | `vocab_groups`, `vocab_items`, `group_words` join table so one word can belong to many areas. |
| Practice attempts | Prompt metadata + learner answer + judge verdict | Structured columns in `attempts` and `judge_actions` (no opaque JSON). We keep full history until a user deletes it. |
| Journal entries | Freeform reflections | Optional; user-controlled. |

Exports produce JSON/CSV dumps of the tables above. “Forget me” deletes rows immediately.

## Storage & Isolation

- SQLite locally, Postgres on Railway. Same schema and migrations in both.
- Every table includes `user_id` (and `track_id` where relevant) so queries always scope to the current user.
- Credentials/LLM keys live in Railway/`.env`, never inside the DB.
- Backups: Railway keeps daily snapshots; later we can add a “dump to Git repo” toggle if we want versioned backups.

## Authentication & Admin Controls

- Simple email/password login for now. No magic links or external OAuth in MVP.
- Admin password (set via env) unlocks a tiny console to delete users, reset passwords, or toggle “allow new sign-ups”.
- Users can change their own email, password, and native language at any time.
