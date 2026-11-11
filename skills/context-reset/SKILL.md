---
name: context-reset
description: "How to reset an agent's context without losing its place. Load when context is getting heavy, before a /clear, or when the user asks to reset, clear, or restart a session."
---

# Context reset

When your context gets heavy (a long transcript, a lot of tool output,
compaction warnings) or the user asks, reset it instead of pushing on.

1. **Write a resume note** to `docs/notes/yyyy-mm-dd-<topic>.md` in your
   checkout (see `project-docs`). A fresh agent must be able to act from it
   alone:
   - the goal, or the absolute paths of the plan that defines it
   - the skills to load
   - what's done, with commits
   - what's in progress, including uncommitted changes
   - the next step, specific enough to act on
   - decisions made and why, and open questions
   - absolute paths to everything else you need: key source files and preview
     URLs
2. **Give the user one copyable block** to paste after clearing. It names the
   skills to load and the note's absolute path:

   ```
   Load the project-docs skill. Read
   /absolute/path/to/checkout/docs/notes/2026-09-11-import-resume.md,
   then check git status and the log before continuing from the note's
   next step.
   ```

3. Ask the user to run `/clear` and paste the block.

## After the reset

1. Read the note.
2. Check the actual state: `git status` and the log. Trust the repo over the
   note where they disagree.
3. Continue from the next step.
