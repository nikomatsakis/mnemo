# UI Site Map

This chapter sketches the MVP surfaces so you can visualize how Mnemo will feel before we cut any HTML. Each section shows the page layout as a text mockup plus a description of the actions available there.

## 1. Dashboard

```text
┌───────────────────────────────────────────────┐
│ Mnemo                                         │
│-----------------------------------------------│
│ Tracks                                [+ Add track]
│  [★] Greek — "basic travel"    [Test Me] [⚙]  │
│  [ ] German — "advanced"       [Test Me] [⚙]  │
│                                               │
│ Next up                                        │
│  Grammar: Present tense -ω verbs (due now)     │
│  Vocab: Ordering coffee in Athens              │
│                                               │
│ Session length                                 │
│  ( slider ▭▭▭▭▭ )  10 prompts                  │
│                                               │
│                         [ Test Me ]            │
└───────────────────────────────────────────────┘
```

- Landing page after login.
- Lists every language track with a quick “Test Me” button and a link to configure (`[⚙]`).
- Dedicated **+ Add track** button opens the track wizard without diving into settings.
- Shows the current queue preview chosen by the scheduler so learners know what’s coming.
- Session length slider (or dropdown) feeds the scheduler before it generates the batch.

## 2. Add / Edit Language Track

```text
┌───────────────────────────────────────────────┐
│ New Track                                     │
│-----------------------------------------------│
│ Language:   [Greek ▾]                          │
│ Descriptor: ["basic travel"]                  │
│ Native lang: English (read-only)               │
│ Experience: [Beginner ▾]                       │
│                                               │
│ [Continue to Grammar ▶]                        │
└───────────────────────────────────────────────┘
```

- Lightweight wizard (one screen for MVP) invoked from “Add track” or `[⚙]`.
- Language dropdown lists only the curated bundles we ship—no custom languages in the UI.
- Descriptor is the only freeform field so learners can remind themselves of the track’s intent.
- Native language is shown for context (editable elsewhere in profile settings).
- Continue button jumps straight to the grammar checklist for that track.

## 3. Grammar Checklist

```text
┌───────────────────────────────────────────────┐
│ Greek Grammar Factors                         │
│-----------------------------------------------│
│ [x] Alphabet basics        12 prompts · 92% ✔  │
│ [x] Present tense -ω verbs  7 prompts · 57% ✔  │
│ [ ] Café ordering phrases   0 prompts yet      │
│ [ ] Transit emergencies     0 prompts yet      │
│-----------------------------------------------│
│ Stats update automatically from your attempts │
│                                               │
│ [Save changes]              [Back to track]   │
└───────────────────────────────────────────────┘
```

- Shows the curated checklist shipped in code for the selected language.
- Each row is just a checkbox: enabled items feed the scheduler; disabled ones are ignored.
- Attempt counts + correctness summaries are read-only data pulled from recent practice history.
- Save writes `track_factor_selection`; there’s still no freeform editing of factors in MVP.

## 4. Vocabulary Area Builder

```text
┌───────────────────────────────────────────────┐
│ Vocabulary Areas (Greek)                      │
│-----------------------------------------------│
│ ▼ Ordering coffee   (12 words ready)           │
│   καφές ✖  ελληνικός ✖  ζάχαρη ✖               │
│   [ + More suggestions ]                       │
│ ▶ Transit pickups   (collapsed)                │
│                                               │
│ + Add new area                                │
│-----------------------------------------------│
│ Add Area                                        │
│  Description: ["Emergency room visit"]        │
│  Guidance:   (textarea for extra hints)        │
│  [Generate 15 words]                           │
│                                               │
│ Suggestions                                    │
│  νοσοκομείο ✖   τραύμα ✖   ασφάλιση ✖           │
│                                               │
│ [Accept list]   [Regenerate]  [ + More suggestions ]
└───────────────────────────────────────────────┘
```

- Existing vocab areas render as an accordion: collapsed rows show the label + word count, while expanded rows expose the words with per-word trash icons and a per-area “+ More suggestions” button.
- Bottom panel lets the user describe a new area; clicking **Generate** calls the LLM and shows the 10–20 suggested words.
- MVP lets you accept the current list, regenerate entirely, or ask for a few more words before saving.

## 5. Practice Session (Test Me)

```text
┌───────────────────────────────────────────────┐
│ Prompt 3 of 10                                │
│ Grammar focus: Present tense -ω verbs         │
│ Vocab focus: Ordering coffee                  │
│-----------------------------------------------│
│ Translate into Greek:                         │
│ "I would like a sweet coffee, please."       │
│                                               │
│ [ textarea for answer ]                       │
│                                               │
│              [ Submit answer ]                │
└───────────────────────────────────────────────┘
```

- Displays the single prompt currently under review with explicit grammar + vocab badges.
- Submit posts to the judge; there are no hints, retries, or partial credit UI in MVP.
- After submission we immediately show verdict + model answer inline (next section).

## 6. Attempt Verdict & History

```text
┌───────────────────────────────────────────────┐
│ Result                                         │
│-----------------------------------------------│
│ Focus item                     Verdict  Notes  │
│ Grammar • Present -ω verbs     ✖        Missing article
│ Word   • καφές                 ✔        Nailed it
│ Word   • ζάχαρη                ✖        Forgot accent
│-----------------------------------------------│
│ Model answer: «Θα ήθελα έναν γλυκό καφέ, παρακαλώ.»
│ Your answer:  «Θέλω γλυκό καφέ παρακαλώ»       │
│-----------------------------------------------│
│ [Next prompt ▶]                                │
│                                               │
│ Recent attempts                               │
│  ✔ #1021 Greek / coffee / present tense        │
│  ✖ #1020 Greek / transit / aorist              │
└───────────────────────────────────────────────┘
```

- Immediately follows the prompt view after judge response.
- Shows per-item verdicts for every grammar factor + vocab word that was targeted, mirroring what we log in the DB.
- Model vs learner answers stay visible for quick comparison.
- Recent attempts sidebar offers quick navigation across the session.

## 7. Account & Admin Console

```text
┌───────────────────────────────────────────────┐
│ Settings                                       │
│-----------------------------------------------│
│ Profile                                        │
│  Display name   [Niko]                         │
│  Email          [nikomatsakis@…]              │
│  Native lang    [English ▾]                    │
│  Password       [••••••] [Change]              │
│                                               │
│ Data                                             │
│  [Delete my account]                            │
│-----------------------------------------------│
│ Admin (password required)                       │
│  [Unlock console]                               │
│  Users: (table appears after unlock)           │
└───────────────────────────────────────────────┘
```

- Combines user profile edits, account deletion, and the admin override switch.
- Admin unlock (via env-set password) reveals a simple table where the operator can reset passwords, remove users, or pause sign-ups; no multi-tenant tools yet.
- Data export is intentionally deferred until after the MVP loop is live.

---

With these mockups we can now trace an MVP user story end to end: land on the dashboard, tweak grammar & vocab, launch **Test Me**, and review results—all without guessing what UI we’re targeting. This chapter should stay in sync with future iterations so we keep the “docs from the future” promise before building screens.
