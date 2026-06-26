# Protocol: Wrap-up and Retrieval

## Purpose

Turn reading sessions into long-term retrievable checkpoints.

The user may read in a general Reading Room or in a dedicated book chat. A wrap-up is a user-triggered checkpoint, not necessarily the end of an article, chapter, or session.

## Wrap-up Trigger

Run this protocol when the user says things like:

- "wrap-up"
- "做个 wrap-up"
- "整理一下刚才读的"
- "把刚才的新词分级"
- "保存这次阅读"

Do not run a full wrap-up after every question. Do not ask to save after every explanation.

## Wrap-up Output

For each wrap-up, produce:

```text
Content Wrap-up:
- covered range
- local summary
- how this section connects to the previous section
- user's key understanding
- next starting point

Language Wrap-up:
- review candidates since the previous wrap-up
- L1-L4 level
- evidence signal
- review strategy
- confirmation before saving

Background Notes:
- people, organizations, political/cultural terms, events, or factions
- save to background notes, not review queue
```

## Review Routing

When the user asks for review without a clear scope, ask which scope to use:

```text
Review which scope?
- last wrap-up
- the last two wrap-ups for this article or book
- a specific article or book
- a specific date, such as last Wednesday's wrap-up
- a topic, such as Trump, MAGA, or American politics
- long-unreviewed items
```

If the user already specifies the scope, use it directly.

## Retrieval Rules

Use local memory in this order:

1. `source-index.md` to find articles, books, topics, and wrap-up IDs.
2. `wrap-up-log.md` to find covered ranges and confirmed review items.
3. `review-queue.md` to find item details, levels, history, and due items.
4. `background-notes.md` to recover cultural or political context.

For older records that lack IDs, infer from `Source`, `Location`, title, date, and topic words.

## Masked Review

Default review should not show the target expression first.

Use mixed prompt types:

- context blank
- meaning recall
- Chinese or user-thought to English
- natural rewrite
- original-context recall

If the user cannot answer, use progressive hints:

```text
Hint 1: word class
Hint 2: first letter or phrase shape
Hint 3: meaning/domain
Answer: target expression
```

## Review Completion

During review, record performance silently. Do not ask after every item whether to downgrade.

When the review ends, the user stops, or the user requests a wrap-up, list downgrade or archive candidates:

- one correct answer -> eligible for downgrade
- correct with only a minor spelling error -> eligible for downgrade or spelling-only note
- correct but slow or hint-dependent -> keep current level
- core meaning, usage, or naturalness wrong -> keep level or increase difficulty

Use the level path:

```text
L4 -> L3 -> L2 -> L1 -> stable/archive
```

Ask before downgrading or archiving.

## Level Definitions

Use levels from lightest to heaviest:

- `L1 one-time check`: understood after explanation; one successful recall may be enough.
- `L2 passive-to-active`: recognized in reading but not yet available for speaking or writing.
- `L3 short-term focus`: partly understood or unstable; needs short-term repetition.
- `L4 new-word build`: completely unfamiliar; build recognition, meaning, tone, and context first.
