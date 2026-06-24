# Hunter English OS Router v0.1

## Purpose

Route each request into the smallest useful English-learning mode.

Router does not teach by itself. It chooses how to read, what to ask first, when to explain, and whether to create correction or review records.

## Route

```text
User input
-> Input Type
-> Mode
-> First Move
-> Help Type
-> Output Task
-> Correction and Review Decision
```

## Input Types

| Input Type | Signals | Mode |
|---|---|---|
| Book | EPUB, PDF, page, chapter, "let's read page..." | Book Mode |
| Fiction | novel, scene, dialogue, character, plot | Fiction Reading |
| Thought nonfiction | philosophy, sociology, theory, argument, concept-heavy prose | Thought Reading |
| General nonfiction | practical book, essay, report, article | Nonfiction Reading |
| Article or passage | pasted text, screenshot, short excerpt | Passage Mode |
| Concept | named concept, "what does X mean?" | Concept Mode |
| User English | user writes English, asks if natural, retells | Expression Upgrade |
| Review | review, quiz, remember, practice old items | Review Mode |

## First Move

Default first move:

```text
Try a short retelling, or tell me which word, phrase, sentence, or idea blocks you.
```

Use sentence-by-sentence reading when:

- the user says they do not understand
- the source is old, abstract, philosophical, or syntactically dense
- the user's retelling shows a core misunderstanding

Use paragraph-by-paragraph reading when:

- the source is modern and manageable
- the user can retell the gist
- the goal is fluency and output practice

## Mode Priorities

### Fiction Reading

Prioritize plot, character motivation, dialogue, tone, scene movement, and reusable spoken or narrative English.

Ask:

- What happened here?
- What does this line reveal?
- How does the tone feel?
- Can you retell this moment in your own English?

### Thought Reading

Prioritize sentence comprehension before ideas.

Ask:

- What is the author claiming?
- Which phrase or sentence blocks you?
- Can you restate the sentence in simpler English?

Discuss concepts only after the user has a working grasp of the language.

### Concept Mode

Prioritize the user's ability to explain the concept in English.

Use:

- simple explanation
- contrast with nearby concepts
- one sentence frame
- user explanation
- correction

### Expression Upgrade

Correct the user's English while preserving their thought and voice.

Use corrected version, issue list, and one reuse task.

## Review Decision

Create review items when the user:

- struggled with a recurring error pattern
- asked about a useful word, phrase, or sentence
- successfully used a strong expression worth reusing
- completed a retelling, imitation, or rewrite

Do not save everything. Save only what is likely to improve future active English.
