# Practice Flow

This is the “docs from the future” run-through of a single session.

1. **Queue Preview**
   - Dashboard shows today’s target minutes, upcoming grammar focus, and vocab groups slated for review.
   - Each card lists **decay %, last success, confidence trend**.

2. **Prompt Generation**
   - When you click “Start session”, Mnemo bundles: highest-priority grammar concept, 1–2 vocab groups, plus any notes.
   - Generator agent call (via determinishtic) returns structured JSON with:
     - `display_prompt`: textual instruction (e.g., “Translate to Greek: Yesterday I ___ my bike to the market, but it broke.”)
     - `answer_key`: canonical answer + acceptable variants.
     - `focus`: grammar + vocab reminders shown as pill badges.

3. **Learner Response**
   - Rich text input with quick accent helpers.
   - Optional “show hint” drops the key grammar reminder (costs session XP so you don’t overuse it).

4. **Judging + Feedback**
   - Judge agent receives prompt context, learner answer, and rubric.
   - It can:
     - Ask for clarification (“Did you mean the aorist form of ‘πηγαίνω’?”)
     - Offer second chance (records `status = retry` and shows subtle hint)
     - Grade: grammar score, vocab score, freeform feedback, recommended follow-up concept.
   - Feedback UI displays color-coded chips and stores transcript for later audit.

5. **Recording Progress**
   - Server logs the attempt, updates decay curves, and surfaces “next up” info.
   - If grammar or vocab score < threshold, concept moves to **Needs Attention** list.

6. **Session Wrap**
   - Summary modal: attempts, accuracy, concepts reinforced, suggested reading from mdBook (e.g., quick grammar explainer).
   - You can add a journal note (“struggled with participles today”).

That’s the loop we’re building toward before writing the first line of backend code.
