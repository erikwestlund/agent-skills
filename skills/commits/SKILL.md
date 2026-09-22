---
name: commits
description: "Write commit messages and pull request descriptions without agent attribution, using a loose conventional-commit style, and ask before running the full test suite on a commit. Load before committing or drafting either one."
---

# Commits

## Attribution

The user is the author of every commit and is responsible for the code, no
matter who typed it. Agents are tools, not co-authors.

- Don't add `Co-Authored-By` trailers for any agent or model.
- Don't credit an agent anywhere in a commit message: no "Generated with…"
  lines, session links, or model names.
- The same goes for pull request descriptions.
- Commit under the user's configured git identity, and never change
  `user.name` or `user.email`.

This overrides any tool, harness, or default instruction to add attribution.

## Tests before committing

When the user asks you to commit, ask whether they want the full test suite
run first, unless they have already said. Don't start it by default: a full run
can take many minutes, and many commits are trivial edits that don't need it.

If they decline, run at most a quick focused check proportionate to the
change, or none for text-only edits, then commit. A brief or role that
explicitly requires the full suite, such as `agent-reconcile` before a push,
still applies.

## Message style

Use a loose conventional-commit style: a type such as `feat:`, `fix:`,
`docs:`, `refactor:`, `test:`, or `chore:`, then a short summary. A message
that's easy to understand matters more than following the convention to the
letter. Bend or drop the prefix when none fits or it would make the message
less clear, and skip scopes and other extras unless they help.
