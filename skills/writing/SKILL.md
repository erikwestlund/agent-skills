---
name: writing
description: "Apply the house prose style and writing conventions. Load before drafting or editing user-facing copy, UI text, documentation, plans, briefs, messages, commit messages, or other prose."
---

# Writing

These rules apply to all UI copy and prose. A project's style guide can add
rules for its own domain and deliverables.

## Governing Principle

Strip away the writer performing until the prose serves the reader. Write plain
declarative sentences. Let evidence and organization carry the argument. Do not
manage the reader with cleverness, drama, self-commentary, callbacks,
metaphors, overselling, over-defending, or emotional framing.

When a sentence is in doubt, ask whether the writer is performing or the
reader is using. Keep only the latter.

- Prefer information over cleverness.
- Don't manufacture rhythm, drama, or contrast.
- Be concrete enough that the copy could not describe any other product.
- Let interesting facts speak for themselves.
- Sound like a thoughtful person, not a marketing department.

## Register And Voice

- Prefer a clear, measured register over punchiness or marketing language. For
  academic and technical subjects, lean lightly academic.
- State the fact without performing it.
- Explain a concept before giving its example.
- Use short, terse, direct sentences with one useful claim each. Avoid
  compressed, slogan-like parallelism.
- Use bullets for enumerations with parallel stems. Use paragraphs for
  arguments.
- Use concrete subjects. Attach the explanation to the thing it describes.
- Name things instead of describing how they relate to something else. Use the
  tools' names or "companion tools" instead of "the tools it works with."
- Use American English spellings: `catalog`, `color`, `gray`, `artifact`, and
  `favor`.

## Headings And Labels

Use descriptive nouns or concise noun phrases for headings, section labels,
and field labels. Avoid conversational headings. Never start a heading with a
question word such as How, What, Why, Where, or When.

- Use "Architecture" or "Request flow" instead of "How it works."
- Use "Rationale" instead of "Why this matters."
- Use "Server administration" instead of "What you manage."
- Use "Server features" instead of "What a self-hosted server includes."
- Use "Artifact storage" instead of "Where published notebooks go."

Write headings like email subject lines, not movie trailers.

- **No eyebrow headings.** Don't put a category label above a heading.
- **No decorative numbering.** Number sections only when their order matters.
- **No rhythmic or contrasting titles.** Avoid formulas such as "Hard to
  describe. Easy to recognize."
- **No metaphorical headings.** Describe the content literally. Avoid
  personification and clever imagery.
- **No vague headings.** Replace "A closer look" or "Why it matters" with the
  specific subject.

Actions need clear verbs, such as "Save changes" and "Create project."

## Matter-Of-Fact UI Copy

UI copy states what a control does in the fewest plain words. It never sells,
charms, or chats.

- Label a field with the plain noun or verb for its value: "Show" next to a
  number, not "How many"; "Order", not "How should these be sorted?"
- Never use a question or a "What/How/Where" phrase as a label, heading, or
  section name: "Contents", not "What it shows"; "Visibility", not "Who can
  see this".
- No marketing words: "powerful", "seamless", "effortless", "beautiful",
  "simply", "just", "magic", "smart", "instantly", "supercharge".
- No exclamation points and no cheerful asides in labels, help text, toasts,
  or empty states.
- Help text says what happens and where, in one short sentence: "Lists your 6
  most recent projects. Updates when you publish."
- Prefer two short sentences to one sentence joined by a comma. Drop a comma
  the sentence reads correctly without.

## Oxford Comma

Always put a comma before the final `and` or `or` in a list of three or more.

- Yes: "The study, its team, and its findings are made up for this demo."
- No: "The study, its team and its findings are made up for this demo."
- Two items take no comma: "The course and its materials."

Do not add commas that grammar does not require.

- Yes: "Composer for the film's score."
- No: "Composer, for the film's score."

This applies to UI copy, documentation, plans, briefs, agent messages, and
commit messages.

When fixing existing text, change only the commas unless the task calls for a
broader edit. Do not sweep generated or seeded content unless the task includes
it.

## Banned LLM Patterns

Treat every pattern below as a firm ban.

- **`X, not Y` antithesis.** State the fact once. Do not add a contrast for
  rhythm.
- **Dramatic reversal.** Avoid constructions such as "It is not X. It is Y."
- **Callback narration.** Do not tell readers that the prose is returning to
  an earlier question. State the question or claim directly.
- **Self-approving narration.** Do not tell readers why the sentence they are
  reading matters or why the handling inspires trust.
- **Sloganized closers.** End when the information ends. Do not append a
  call-to-action rhythm line or punchy kicker.
- **Epigrams and coined metaphors.** Replace clever formulations with plain
  terms or remove them.
- **Throat-clearing openers.** Delete phrases such as "The first thing to know
  is," "The question worth answering is," "One point of care applies," and
  "The catch is."
- **Comma overuse.** Join short paired clauses with a bare `and`. Use fewer
  colons and semicolons.
- **Em dash overuse.** Prefer a second sentence or parentheses. Use an em dash
  occasionally.
- **Relationship or defensive framing toward the reader.** Describe the
  operation factually.
- **Metaphors for technical or statistical concepts.** Use the domain's actual
  terms.
- **Fragment-style drama.** Write complete sentences.
- **Slogans and clichés.** Delete phrases such as "Built for teams that ship"
  and "Unlock your potential."

## Sentence Construction

- Give a count its own short declarative sentence instead of appending it as a
  trailing aside.
- End a sentence when its information ends. Remove trailing flourishes.

## Final Check

Before returning a draft:

1. Search it for every banned pattern above.
2. Remove performance, throat-clearing, callbacks, and trailing flourishes.
3. Check American spelling and the Oxford comma.
4. Confirm that sentences are short and direct with one useful claim each.
5. Check that headings and labels use descriptive nouns or concise noun
   phrases and that actions use clear verbs. Remove eyebrows, decorative
   numbering, and rhythmic, metaphorical, or vague headings.
6. Check that each claim is specific to its subject. Rewrite any line that
   could describe a different product.
7. Read every label, help line, and toast as UI copy: plain nouns and verbs,
   no questions, no marketing words, and no comma it can do without.
