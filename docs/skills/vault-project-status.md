# vault-project-status

Set a project's lifecycle status, or archive a finished project.

| | |
|---|---|
| **Command** | `/vault-project-status` |
| **Mode** | Write (transform in place; archive = relocate) |
| **SKILL.md** | `skills/vault-project-status/SKILL.md` |

## Triggers

"mark agentwatch active", "set this project to paused", "agentwatch
shipped", "archive the foo project", "reactivate bar".

## Inputs

Which project, and its new state.

## Reads / writes

- **Reads:** the project folder, `_INDEX.md`, `AGENTS.md`.
- **Writes:** updates the status in `PROGRESS.md` frontmatter,
  `_INDEX.md`, and the `AGENTS.md` Active Projects table — keeping all
  three consistent.

## Status set (default; matches existing vocabulary first)

⚪ Planned · 🟢 Active · 🟡 Paused · ✅ Shipped · 📦 Archived

## Archiving

Relocation, never deletion: moves the folder to `projects/_archive/`,
updates the `_INDEX.md` row + link, removes the row from `AGENTS.md`
Active Projects, and flags synced repo files as stale.

## Key rules

- Keeps PROGRESS.md / _INDEX.md / AGENTS.md in sync; reports any it
  couldn't update.
- Confirms before archiving.
- Uniquely-anchored edits on the project name.

## Related

Lifecycle sibling of [vault-idea-status](vault-idea-status.md). After
archiving or any rename via [vault-move](vault-move.md), re-run
[vault-project-sync](vault-project-sync.md).
