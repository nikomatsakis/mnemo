# User Guide Overview

Mnemo is designed for self-directed learners who want tight feedback loops without micromanaging flashcards. A typical learner journey looks like this:

1. **Create study tracks.** Add as many languages as you like (Greek, German, etc.), describe the flavor (“basic German”), and Mnemo loads the curated grammar factor list for that language before suggesting a subset that fits your goal.
2. **Describe grammar priorities.** Per track, accept or tweak the suggested factors (cases, aspect, agreement, prefixes) and jot nuanced notes when needed.
3. **Author vocab groups in plain English.** For example: “daily routine verbs”, “phrases for ordering coffee”, “Athenian street directions”. Mnemo lets the LLM fill in exemplars per track.
4. **Start a practice session.** Mnemo chooses the track you want to study, mixes grammar + vocab based on decay, then hands the baton to the generator agent.
5. **Respond + iterate.** You type your translation. The judge agent can offer one retry if you were close, then records a verdict.
6. **Review insights.** Every attempt updates your decay curves (scoped to the current track) and surfaces next-step recommendations. The journal keeps lightweight notes.

The rest of the User Guide drills into configuration and the live practice flow.
