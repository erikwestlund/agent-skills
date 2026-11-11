# Agent Skills

Cross-project skills for Claude Code and Codex. OpenCode reads
`~/.claude/skills` as well.

| Skill | For |
|---|---|
| `context-reset` | Reset a long session: a resume note and a block to paste back in. |
| `commits` | No agent attribution in commits and PRs; loose conventional-commit style; ask before running the full test suite on a commit. |
| `commit-sync` | After a commit, check the branch against `origin` and report how to synchronize it. |
| `codex-adversarial-review` | Use Codex to independently review work from non-flagship models. |
| `php-testing` | Run PHP tests with installed PAO support and parallel execution where supported. |
| `writing` | House prose style and writing conventions. |
| `file-delivery` | Serve stored files from storage's CDN, never through the app server. |
| `project-docs` | Dated work logs in `docs/work/`, pickup notes in `docs/notes/`. |
| `system-config` | Change the Mac only through `~/System`, never by hand. |
| `project-tunnels` | Prepare project and worktree previews and share HTTPS tunnel links during web application work. |
| `r-stats` | Statistical work in R: framework, readability, notebooks, scripts, plots. |

## Install

```bash
./install.sh
```

This links each `skills/<name>` into `~/.claude/skills/` and `~/.codex/skills/`.
Edit the files here and the links pick up the changes. Re-run it after adding a
skill.

## Adding a skill

Create `skills/<name>/SKILL.md` with `name` and `description` frontmatter, and
keep it short. Skills about a single project belong in that project's
`.claude/skills/` instead.
