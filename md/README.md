# Mnemo

Mnemo is a language-learning co-pilot that blends human-curated goals with adaptive LLM-driven practice. These docs describe the experience we’re aiming for so we can stay aligned before writing code.

## MVP Scope

1. **Define study tracks.** A learner can add multiple target languages, set a level/descriptor (“basic German”), and let Mnemo seed an initial grammar concept list for that track.
2. **Curate grammar + vocab.** Per track, they accept/prune the suggested grammar factors and author vocab groups in plain English. Everything is stored per user/track so it’s easy to customize.
3. **Run translation drills.** Mnemo selects (grammar concept, vocab group) pairs with the highest need, asks the LLM generator for a prompt, and collects the learner’s translation.
4. **Judge + record attempts.** A judge agent grades the response (grammar + vocab), offers at most one retry, and the result updates SRS scores and the journal.
5. **Surface what’s next.** The dashboard shows track-level decay state and points the learner to the next drill. Data exports and deletions work from day one.

Everything else is secondary for now. Nice-to-have ideas (accent helpers, fancy hints, auto-shared decks, etc.) stay out of the MVP unless they directly support the loop above.

## Vision (longer term)

- **Richer grammar roadmap.** Visualize dependencies, streaks, and confidence bands.
- **LLM coach personality.** Tone-aware feedback, follow-up exercises, conversational practice.
- **Collaborative cohorts.** Shared vocab packs or classrooms once we solve auth + privacy at scale.

Keep reading for the user workflow, architecture, and journal that track how we’ll get there.
