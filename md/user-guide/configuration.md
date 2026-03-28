# Configuration

## Study Profile

- **Study tracks:** You can maintain multiple languages at once (e.g., “Greek – conversational refresh”, “German – basic travel”). Each track stores the language name, optional dialect qualifier, and a freeform descriptor (“basic German”, “advanced European Portuguese”).
- **Bootstrap grammar catalog:** When you add a track, Mnemo asks the LLM to assemble an initial grammar concept list tailored to your descriptor. You can accept it wholesale or prune/add items manually.
- **Experience level & cadence:** Per track you set level (beginner / returning / conversational / fluent-but-rusty) plus preferred minutes per day and weekly targets. Scheduler keeps independent queues per track.

## Grammar Concepts

- Concepts live inside each study track. Browse the auto-generated list or add your own (“Subjunctive mood in polite requests”).
- Mark status: *Not started*, *Learning*, *Reinforcing*, *Confident*. Status + notes stay scoped to the track so German progress doesn’t affect Greek.
- Optional notes (feed into prompts): “Practice dative plural endings,” “focus on separable prefixes.”

## Vocabulary Groups

- Authored per track using natural language: “breakfast foods you’d mention in Athens”, “verbs for negotiating in German flea markets”.
- Optional seed list: comma-separated source/target words for extra control.
- Tags: formality, context, register, “must include” vs “nice to include.”
- Mnemo tracks decay per group, per item, and per track.

## Notifications & Integrations

- Reminders can be global or per track (e.g., weekday ping for Greek, weekend ping for German).
- Export tools let you download all data or filter by track (CSV, Anki, JSON journal).

After saving, Mnemo persists the tracks, runs migrations if needed, and precomputes queues independently for each language.
