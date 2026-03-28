# Architecture Overview

Mnemo will ship as a Rust web service with a lightweight front-end, a prompt-orchestration layer, and a persistence core. Key themes:

- **Deterministic orchestration.** We’ll use the `deterministic` crate to define generator + judge agents with typed inputs/outputs, making prompts versionable and testable.
- **Event-sourced attempts.** Every learner response stores raw prompt, answer, judge verdict, and metadata so we can re-grade later if prompts change.
- **Modular decay engine.** Scheduling logic is isolated so we can tweak algorithms (SM-2, exponential decay, hybrid) without touching UI layers.
- **mdBook-driven knowledge.** Docs live next to code, letting us link architecture sections directly from the app when learners need help.
- **Data governance & multi-user readiness.** From day one every table is scoped by `user_id`, retention policies are explicit, and export/delete flows are part of the contract (see the data retention section for details).

The following pages break down the components and data model.
