# vault-find

Ranked snippet search across the vault.

| | |
|---|---|
| **Command** | `/vault-find` |
| **Mode** | Read-only |
| **SKILL.md** | `skills/vault-find/SKILL.md` |

## Triggers

"find in vault", "search vault", "look up X in my notes", "what did I
note about X", "find issue", "do I have an idea about X".

## Inputs

The query. If ambiguous, asks what to search for.

## Reads / writes

- **Reads:** `projects/**/*.md`, `ideas/*.md`, `brand/*.md`,
  `_logs/PENDING_REVIEW.md`.
- **Writes:** nothing.

## Output

Matches grouped by section (Projects / Ideas / Brand / Pending Log) with
relative path, nearest heading, and a snippet. Capped at 10 unless asked
for more.

## Key rules

- Read-only; shows actual snippets, not paraphrase.
- Case-insensitive substring; filename match ranks above content match.
- Multi-word: AND matches first, then OR if AND is thin.
- Relative paths for clickable navigation.

## Related

Use [vault-read](vault-read.md) to pull the full content of a match;
[vault-status](vault-status.md) for the aggregate view.
