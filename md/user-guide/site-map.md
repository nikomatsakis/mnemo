# UI Site Map

This chapter sketches the MVP surfaces so you can visualize how Mnemo will feel before we cut any HTML. Each section shows the page layout as a text mockup plus a description of the actions available there.

## 1. Dashboard

```text
┌───────────────────────────────────────────────┐
│ Mnemo                                         │
│-----------------------------------------------│
│ Tracks                                         │
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
- Shows the current queue preview chosen by the scheduler so learners know what’s coming.
- Session length slider (or dropdown) feeds the scheduler before it generates the batch.
- Primary CTA is the bottom **Test Me** button (mirrors the track-level buttons).

## 2. Add / Edit Language Track

```text
┌───────────────────────────────────────────────┐
│ New Track                                     │
│-----------------------------------------------│
│ Language:   [Greek v ]                         │
│ Descriptor: ["basic travel"]                  │
│ Native lang: English (read-only)               │
│ Experience: [Beginner v]                       │
│                                               │
│ [Continue to Grammar ▶]                        │
└───────────────────────────────────────────────┘
```

- Lightweight wizard (one screen for MVP) invoked from “Add track” or `[⚙]`.
- Captures which curated language bundle to load and a freeform descriptor.
- Native language is shown for context (editable elsewhere in profile settings).
- Continue button jumps straight to the grammar checklist for that track.

## 3. Grammar Checklist

```text
┌───────────────────────────────────────────────┐
│ Greek Grammar Factors                         │
│-----------------------------------------------│
│ [✔] Alphabet basics             confident      │
│ [ ] Present tense -ω verbs      learning       │
│ [ ] Café ordering phrases       learning       │
│ [ ] Transit emergencies         to review      │
│-----------------------------------------------│
│ Legend: confident • learning • to review      │
│                                               │
│ [Save changes]              [Back to track]   │
└───────────────────────────────────────────────┘
```

- Shows the curated checklist shipped in code for the selected language.
- Every row is a toggle with one of three statuses (confident, learning, to review).
- Learners curate which factors appear in the scheduler by flipping statuses here.
- Save writes `track_factor_selection`; there’s no freeform editing of factors in MVP.

## 4. Vocabulary Area Builder

```text
┌───────────────────────────────────────────────┐
│ Vocabulary Areas (Greek)                      │
│-----------------------------------------------│
│ Area label        Words                       │
│ Ordering coffee   καφές, ελληνικός, ζάχαρη…   │
│ Transit pickups   ταξί, οδηγός, πινακίδα…     │
│                                               │
│ + Add new area                                │
│-----------------------------------------------│
│ Add Area                                        │
│  Description: ["Emergency room visit"]        │
│  Guidance:   (textarea for extra hints)        │
│  [Generate 15 words]                           │
│                                               │
│ Suggestions                                    │
│  νοσοκομείο, τραύμα, ασφάλιση, …               │
│                                               │
│ [Accept list]   [Regenerate]                   │
└───────────────────────────────────────────────┘
```

- Top section lists existing vocab areas (each linking to a detail modal if needed).
- Bottom panel lets the user describe a new area; clicking **Generate** calls the LLM and shows the 10–20 suggested words.
- MVP accepts the suggestions wholesale via **Accept list**; editing individual words comes later.

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
│ Verdict: ✖ Incorrect                           │
│ Model answer: «Θα ήθελα έναν γλυκό καφέ, παρακαλώ.»
│ Your answer:  «Θέλω γλυκό καφέ παρακαλώ»       │
│ Notes: difference highlighted (missing article)
│-----------------------------------------------│
│ [Next prompt ▶]                                │
│                                               │
│ Recent attempts                               │
│  ✔ #1021 Greek / coffee / present tense        │
│  ✖ #1020 Greek / transit / aorist              │
│                                               │
│ [Add journal reflection]                      │
└───────────────────────────────────────────────┘
```

- Immediately follows the prompt view after judge response.
- Shows verdict, canonical answer, learner answer, and a short textual comparison.
- “Next prompt” advances the queue until the requested session length is exhausted.
- Recent attempts sidebar offers quick navigation plus an optional “journal reflection” entry field (purely textual, stored separately).

## 7. Account & Admin Console

```text
┌───────────────────────────────────────────────┐
│ Settings                                       │
│-----------------------------------------------│
│ Profile                                        │
│  Display name   [Niko]                         │
│  Email          [nikomatsakis@…]              │
│  Native lang    [English v ]                   │
│  Password       [••••••] [Change]              │
│                                               │
│ Data                                             │
│  [Export my data]   [Delete my account]         │
│-----------------------------------------------│
│ Admin (password required)                       │
│  [Unlock console]                               │
│  Users: (table appears after unlock)           │
└───────────────────────────────────────────────┘
```

- Combines user profile edits, data export/delete actions, and the admin override switch.
- Admin unlock (via env-set password) reveals a simple table where the operator can reset passwords, remove users, or pause sign-ups; no multi-tenant tools yet.

---

With these mockups we can now trace an MVP user story end to end: land on the dashboard, tweak grammar & vocab, launch **Test Me**, and review results—all without guessing what UI we’re targeting. This chapter should stay in sync with future iterations so we keep the “docs from the future” promise before building screens.
