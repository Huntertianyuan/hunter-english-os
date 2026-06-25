# Protocol: Correction and Memory

## Purpose

Turn the user's actual English into better future English.

Correction should produce active ability, not just a polished answer.

## Correction Order

1. Meaning: Is the user's understanding right?
2. Natural version: How would this sound in clear English?
3. Issues: What recurring or high-value problems appear?
4. Reuse: What should the user try again?
5. Memory: Is this comprehension support, a session checkpoint, or a review item?

## Correction Format

Use this compact format when useful:

```text
Your understanding is right / partly right / not quite.

More natural:
...

What changed:
- ...

Try again:
...
```

## Preserve Voice

Improve the English without replacing the user's mind.

Do not turn every answer into generic polished AI prose. Keep the user's intended meaning, level of force, and personal angle.

## Error Patterns

Track patterns, not isolated mistakes.

Examples:

- indirect question order
- preposition after abstract nouns
- hypothetical tense consistency
- article use
- countability
- unnatural collocation
- Chinese-like clause order
- over-literal translation
- weak transitions
- register mismatch

## Memory Decision

Save a review candidate when an item is likely to recur, the user explicitly wants it, or it supports active production. Use `capture-workflow.md` to infer candidates from user signals before saving.

Do not confuse comprehension support, session notes, and review items.

- Comprehension support: explanation that helps the user understand the current source locally.
- Background note: source context such as a person, organization, event, or institution.
- Session checkpoint: temporary reading continuity, such as what was read and the local gist.
- Review queue: long-term practice items that can train future ability.

Save only if the item is user-selected, reusable, recurrent, or tied to the user's real difficulty.

Classify saved items:

- `reading_obstacle`: a word or phrase that blocked comprehension or was guessed incorrectly.
- `active_expression`: an expression the user can understand but wants to produce in their own writing or speech.
- `error_pattern`: a recurring structure, word choice, collocation, or grammar problem from the user's output.

Keep `comprehension_support` and `background_note` out of the review queue unless the user explicitly asks to remember them.

Do not save authorial one-off metaphors, local argument explanations, or comprehension-only notes unless the user asks or they are likely to matter again.

Do not save long excerpts.

Before saving, apply this gate:

```text
1. Did the user explicitly say they want to remember it?
2. Did it block comprehension in a reusable way, reveal a recurring output problem, or support future production?
3. Can the user practice it later without rereading the whole original paragraph?
4. Can it be tested through active recall, repair, transfer, or production?
```

If the answer is no, keep it only in a session checkpoint or leave it out.

Before saving, show review candidates with level and reason, then ask for confirmation. Save only confirmed items.

## Session Checkpoints

Use session checkpoints for reading continuity, not long-term practice.

A checkpoint may include:

- source and location
- local gist
- important context for the next paragraph
- blockers already resolved
- comprehension support that should not enter review
- background notes that should not enter review
- user's retelling or correction highlights
- review items actually kept
- next starting point

Keep checkpoints brief. They should help the next session resume reading; they should not become a second review queue.

Finalize reading progress at the end of a session. The final saved progress must reflect the actual stopping point, what was really covered, blockers encountered, user output, corrections, kept review items, comprehension support not saved to review, and next starting point.

Default memory path:

`/Users/tianyuan/Documents/Codex工作台/工作系统/memory/hunter-english-os/`

Ask before saving sensitive or personal material.

## Review Method

Do not use multiple-choice prompts.

Use varied active prompts across intervals:

- reading obstacle: explain the phrase, describe the picture, paraphrase in context, then lightly transfer to a new context if useful.
- active expression: translate a thought into English, complete a frame, respond to a new scenario, then write a free sentence.
- error pattern: repair a sentence, transform it into a better pattern, use the pattern in a new context, then produce freely.

Use this progression when possible:

```text
recognize
-> explain
-> transfer to a new context
-> actively use
```

## Review Levels

Assign a review level before saving:

- `L1 one-time check`: user understands component words but has not seen the fixed expression. One successful recall may be enough.
- `L2 short-term focus`: expression or component word is uncertain. Use short-term review until recognition and basic use are stable.
- `L3 passive-to-active`: user recognizes the word while reading but does not actively produce it. Focus on natural output, not definition.
- `L4 new-word build`: user has not seen the word before. First build recognition and context, then later move toward production.

Use `User Need`, `Review Strategy`, and `Exit Condition` to keep the review queue from becoming a vocabulary pile.

Include `Evidence Signal` when saving, such as `user said completely unfamiliar`, `user misread concept`, `user knows word but not expression`, or `user rarely uses this word form`.

## Strength and Intervals

Estimate strength from the user's performance, then let the user correct the estimate.

Consider:

- accuracy
- naturalness
- need for hints
- hesitation or effort when visible
- transfer to a new context
- recurrence of old errors

Default scale:

```text
0 = cannot recall or produce
1 = recognizes vaguely
2 = can understand or use with support
3 = can explain or use after thinking
4 = can use naturally in a new context
```

Default intervals:

```text
new -> same session or 1 day
first success -> 1 day
second success -> 3 days
third success -> 7 days
fourth success -> 14 days
stable -> 30 days
```

If the user misses an item, schedule same-session or next-day review. If the answer is correct but slow, keep the interval. If the answer transfers naturally, extend the interval.
