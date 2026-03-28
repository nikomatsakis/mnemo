# Mnemo

Mnemo is a language-learning co-pilot that blends human-curated goals with adaptive LLM-driven practice. These docs describe the experience we’re aiming for so we can stay aligned before writing code.

## MVP Scope

1. **Define study tracks.** A learner can add multiple target languages, set a level/descriptor (“basic German”), and load the curated grammar-factor list for that track.
2. **Curate grammar + vocab.** Per track, they accept/prune the suggested grammar factors and author vocab groups in plain English. Everything is stored per user/track so it’s easy to customize.
3. **Run translation drills.** Mnemo selects (grammar factor, vocab group) pairs with the highest need, asks the LLM generator for a prompt, and collects the learner’s translation.
4. **Judge + record attempts.** A judge agent grades the response (grammar + vocab) and the result updates SRS scores and the journal.
5. **Surface what’s next.** The dashboard shows track-level decay state and points the learner to the next drill. Data exports and deletions work from day one.

The rest of the mdBook dives into user workflow, architecture, and the build journal.
