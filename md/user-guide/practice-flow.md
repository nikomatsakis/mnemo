# Practice Flow

MVP session loop:

1. **Pick the next drill**
   - Dashboard lists each track with “minutes remaining” and the highest-priority grammar/vocab pair.
   - Click a track to start; Mnemo dequeues the top pair.

2. **Generate a prompt**
   - Server passes the selected grammar factor + vocab group to the LLM generator (via determinishtic).
   - Generator responds with plain text instructions (e.g., “Translate to Greek: Yesterday I rode my bike to the market but it broke”) and an answer key.

3. **Learner responds**
   - Simple textarea input; type the translation and submit.
   - (Future niceties like accent helpers or hints are out-of-scope for MVP.)

4. **Judge + optional retry**
   - Judge agent sees the prompt, answer key, and your response.
   - It can (a) mark correct/incorrect/close with short feedback or (b) offer one retry if the answer was almost there.

5. **Record + advance**
   - Attempt stored with grammar factor + vocab group references.
   - SRS scores update, the queue pulls the next pair, and the dashboard reflects progress.

That’s the minimal loop we’re targeting before adding polish.
