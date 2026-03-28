# Data Retention & Multi-user Plan

## Per-user Data Retained

| Category | Details | Retention & Controls |
| --- | --- | --- |
| Profile | handle, timezone, cadence, notification prefs | Stored in `users`. Editable at any time. |
| Grammar roadmap | concept statuses + freeform notes | Lives in `user_grammar_status`. Notes are plain text, exportable. |
| Vocabulary groups | natural-language descriptions, tags, optional seed words, expanded vocab items | Stored in `vocab_groups` + `vocab_items`. Each row references `user_id`. |
| Practice attempts | prompt payloads, learner answers, judge verdicts, hints exchanged | Stored in `attempts` + `judge_actions`. Redactable per attempt. Default retention: 180 days; older rows can be summarized or purged. |
| Journal entries | manually or automatically logged milestones | Stored in `journal_entries`. Users can delete individual entries. |
| Telemetry | anonymized timing + success metrics for tuning | Aggregated in `metrics_events` with user_id optional; raw events trimmed after 30 days.

All blobs are JSON (capped, gzip-compressed at rest) so we can re-run grading if prompts change. Users can trigger **Export my data** (zip of JSON/CSV) or **Forget me** (soft-delete immediately, hard-delete via nightly job).

## Storage & Isolation Strategy

- **Database:** SQLite for local dev, Postgres in production. Every table has a non-null `user_id` foreign key.
- **Service layer:** All queries flow through repositories that require an explicit `UserScope`. No raw SQL without `WHERE user_id = ?`.
- **Encryption:** `.env` config toggles envelope encryption for sensitive blobs (future work). Even before that, we keep secrets (PATs, API keys) outside the DB.
- **Backups:** Logical dumps run nightly. We rotate backups every 7 days; encryption-at-rest handled by the host environment.

## Multi-user Readiness

1. **Authentication**
   - Start with simple email magic links for local testing.
   - Abstract auth provider so we can plug in GitHub / OAuth later.

2. **Tenant-aware scheduler**
   - Scheduler jobs accept `(user_id, queue_window)` tuples and run independently, so adding more users scales linearly.
   - Background workers pull from a `scheduler_jobs` table keyed by user.

3. **Resource quotas**
   - Each user has LLM token budgets + max concurrent sessions to prevent one user from exhausting the system.

4. **Namespace hygiene**
   - mdBook references that surface in product are filtered per user (e.g., linking to grammar explanations) without exposing other users’ annotations.

5. **Moderation & privacy**
   - Judge prompts never include other users’ data.
   - Admin tooling can impersonate a user only through audited “support sessions”.

## Roadmap

- **Short term:** enforce per-user scoping everywhere, add export/delete endpoints, document retention defaults in the UI.
- **Mid term:** migrate to Postgres with row-level security and start wiring in account-level billing/quotas.
- **Long term:** support collaborative cohorts (shared vocab sets) using explicit sharing tables so private data stays private by default.
