# Configuration

## Study Profile

- **Study tracks:** Maintain multiple languages at once (e.g., “Greek – conversational refresh”, “German – basic travel”). Each track stores the language name, optional dialect qualifier, and a descriptor (“basic German”).
- **Bootstrap grammar catalog:** When you add a track, Mnemo asks the LLM to assemble an initial set of grammar factors for that language/descriptor. You can accept, prune, or add items manually.
- **Experience level & cadence:** Per track, set level (beginner / returning / conversational / fluent-but-rusty) plus preferred minutes per day and weekly targets. Scheduler keeps independent queues per track.

## Grammar Concepts

- Concepts live inside each study track. Browse the auto-generated list or add your own (“Subjunctive mood for polite requests”).
- Mark status: *Not started*, *Learning*, *Reinforcing*, *Confident*. Status + notes stay scoped to the track so German progress doesn’t affect Greek.
- Attach optional notes (feed into prompts): “Practice dative plural endings,” “focus on separable prefixes.”

## Vocabulary Groups

- Authored per track using natural language: “breakfast foods you’d mention in Athens”, “verbs for negotiating in German flea markets”.
- Optional seed list: comma-separated source/target words for extra control.
- Tags: formality, context, register. Mnemo tracks decay per group, per item, and per track.

## Out of Scope (for now)

- Notifications, external integrations, and cohort sharing ship later. MVP focuses on: define track → curate grammar/vocab → practice translations → log progress.

After saving, Mnemo persists the tracks, runs migrations if needed, and precomputes queues independently for each language.
