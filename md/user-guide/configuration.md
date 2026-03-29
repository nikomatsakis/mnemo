# Configuration

## Native Language
- Set once (editable). We use it to decide translation direction and to localize UI copy later.

## Target Languages
For each target language you add:
- **Goal + proficiency:** freeform descriptor plus a dropdown (beginner / intermediate / advanced / expert).
- **Grammar checklist:** we show the full curated list for that language with checkboxes. Enabling/disabling a factor doesn’t delete its data—we still display last-seen time, accuracy, and next scheduled review so you can re-enable later.
- **Per-factor stats:** sparkline or simple text showing “last attempted”, “confidence”, and “next due”. Even disabled factors keep their history visible.

## Vocabulary Areas
- Describe an area in plain English (“Berlin coffee order”, “Spanish emergency room”). Mnemo stores the description + tags and asks the LLM to propose concrete words/phrases.
- Each word entry tracks: spelling, meaning/notes, associated areas, accuracy, next due time. Because a word can belong to multiple areas we keep a `words` table and a join table for `(word_id, area_id)`.
- Actions per area: “add more words” (re-prompt the LLM), “delete word”, or “move word to another area”. Removing a word from one area doesn’t erase its history if it still belongs elsewhere.

## What You See on the Settings Page
- Native language summary.
- List of target languages with goal + quick stats.
- Within each language, the grammar table and vocabulary areas described above.
- Buttons for exporting/deleting your data.

That’s all the configuration we need for MVP; everything feeds the Test Me loop.
