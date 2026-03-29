# Architecture Overview

Mnemo ships as a Rust web service with a lightweight front-end, a prompt-orchestration layer, and a persistence core. Key themes:

- **Deterministic orchestration.** Generator + judge agents use typed prompts so we can version/test them.
- **Event-sourced attempts.** Every learner response stores raw prompt, answer, judge verdict, and metadata for re-grading.
- **Modular decay engine.** Scheduling logic is isolated so we can evolve SRS math without touching UI layers.
- **Batteries-included hosting.** The repo includes a Dockerfile + Railway config so anyone can deploy with minimal setup (LLM API key + admin password). Built-in auth is simple email/password, with an admin login to delete users, lock sign-ups, or reset credentials.
- **Data governance & multi-user readiness.** Each table is scoped by `user_id`, retention policies are explicit, and export/delete flows are part of the contract (see the data retention section).

The following pages break down the components and data model.
