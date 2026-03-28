# Configuration

## Study Profile

- **Language:** Currently Greek, but Mnemo stores a `target_language` field so we can expand later.
- **Experience level:** Beginner / returning / conversational. Used to seed default grammar priorities and generator tone.
- **Cadence settings:** Desired minutes per day + weekly goal. Scheduler uses these to size daily queues.

## Grammar Concepts

- Browse curated concepts (e.g., *Present tense*, *Aorist*, *Cases*, *Particles*) with short explanations.
- Mark each concept with a status: *Not started*, *Learning*, *Reinforcing*, *Confident*.
- Optional notes: “struggling with aspect vs tense”, “remember to drill feminine endings”. These notes feed the LLM prompts.

## Vocabulary Groups

- Authored as natural-language descriptions. Example: “verbs used when negotiating in a market, including polite forms.”
- Optional seed list: comma-separated Greek or English words if you want extra control.
- Tags: formality, context (travel, work), and “must include” vs “nice to include”.
- Mnemo tracks decay per group and per surfaced token.

## Notifications & Integrations

- Toggle reminders (Telegram bot ping, email, desktop).
- Export: CSV of attempts, Anki deck snapshot, raw journal entries.

Once configured, hit **Save profile**. Mnemo persists everything, migrates schema automatically, and the scheduler precomputes your first queue.
