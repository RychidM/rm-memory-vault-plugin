# vault-edit

Make a direct, in-place edit to existing vault content.

| | |
|---|---|
| **Command** | `/vault-edit` |
| **Mode** | Write (gated, transform in place) |
| **SKILL.md** | `skills/vault-edit/SKILL.md` |

## Triggers

"fix the agentwatch overview", "update the style guide", "correct that
issue's description", "reword the brand profile".

## Inputs

What to change — resolved the same way as [vault-read](vault-read.md),
plus the desired change.

## Reads / writes

- **Reads:** the target file.
- **Writes:** a surgical, uniquely-anchored replacement; then appends a
  `[PROMOTED]` `context` record to `_logs/PENDING_REVIEW.md` for
  traceability (unless RM opts out).

## Key rules

- **Existing content only** — new knowledge goes through
  [vault-logger](vault-logger.md) so it gets reviewed.
- **Gated:** confirms a before → after before non-trivial writes
  (frontmatter, table headers, status fields, `AGENTS.md` / `_INDEX.md` /
  `brand/`).
- Surgical edits — never full-file rewrites for a small fix.
- Preserves frontmatter order, tables, headings, wikilinks, issue IDs.
- Never deletes a project, file, or entry.

## Related

This is the one write skill that bypasses the review loop — which is why
it's gated and self-logs. Read first with [vault-read](vault-read.md).
