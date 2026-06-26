# Protocol: Capture Workflow

## Purpose

Detect the user's real English-learning needs without requiring the user to classify every word or error.

The user may read naturally, add brief notes, ask questions, or summarize needs during wrap-up. Infer candidates from that evidence, but do not ask about saving after each question.

## Workflow

Use this flow silently while helping the user understand a sentence, paragraph, or small unit:

```text
detect candidate
-> infer user need
-> classify as comprehension support, background note, reading obstacle, active expression, or error pattern
-> assign review level
-> propose review strategy
-> buffer until user-triggered wrap-up or save request
-> ask confirmation at wrap-up
-> save only confirmed review items
```

Do not require labels from the user. Use their natural signals.

## Candidate Sources

Look for candidates in:

- explicit memory requests: "I want to remember this", "I should save this"
- inline notes: "not clear", "first time", "completely don't know", "rarely use this"
- retelling errors or corrected output
- wrong guesses about meaning, word class, phrase boundary, or concept
- passive recognition signals: "I know this word but would not use it"
- background blockers: unfamiliar organizations, people, events, or terms

## Classification

Use these categories before deciding whether to save:

- `comprehension_support`: helps understand the current article or sentence locally; store in reading progress, not review queue.
- `background_note`: source context such as a person, organization, event, or institution; store in reading progress unless the user explicitly wants to review it.
- `reading_obstacle`: word or phrase that truly blocked comprehension or was guessed incorrectly in a reusable way.
- `active_expression`: word, phrase, collocation, or word-family pattern the user can partly recognize but cannot naturally produce.
- `error_pattern`: recurring grammar, word choice, collocation, word order, or register problem from the user's own English.

## User Signal Rules

Map user signals conservatively:

- "completely don't know", "first time seeing this word", "never seen this" -> `L4 new-word build`, usually `reading_obstacle`.
- "I know the words but not this expression", "why is this word here?", "first time seeing this saying" -> fixed expression or semantic chunk; usually `L1 one-time check` or `L3 short-term focus`.
- "I rarely use this as a verb/noun/adjective", "I recognize it but do not use it" -> `L2 passive-to-active`, usually `active_expression`.
- "What is this organization/person/event?" -> `background_note`; reading progress only unless user asks to remember it.
- Wrong concept guess, such as reading "the American right" as "American rights" -> `comprehension_support` plus possible `reading_obstacle`; correct the concept first and do not rush to review.
- Partly understood but unstable words such as "divisive?" -> `L3 short-term focus` if useful beyond the paragraph.

## Review Candidate Confirmation

Only when the user asks for wrap-up, saving, or review-candidate整理, list high-value candidates. Ask before saving.

Use this shape:

```text
Review Candidates:
1. querulous — L4 new-word build — completely unfamiliar; save?
2. opponent as noun / oppose as verb — L2 passive-to-active — you noted you rarely use the verb; save?
3. divisive — L3 short-term focus — partly understood but unstable; save?
4. heterogeneous — L4 new-word build — unfamiliar and useful in nonfiction; save?

Reading Progress Only:
- The American right = the American political right, not "American rights"
- Turning Point USA = background note
```

If the list is long, keep the strongest few and put the rest under reading progress only.

## Saving Rule

Save confirmed review items only.

Do not save:

- every explained phrase
- background notes unless requested
- local argument explanations
- one-off authorial wording
- items the user understood immediately and is unlikely to need again

When saving, include `Evidence Signal` so future review knows why the item exists.

Background notes should be saved to `background-notes.md`, not review queue.
