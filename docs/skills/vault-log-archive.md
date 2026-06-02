# vault-log-archive

Move promoted/discarded entries into monthly archive files.

| | |
|---|---|
| **Command** | `/vault-archive` |
| **Mode** | Write (relocate) |
| **SKILL.md** | `skills/vault-log-archive/SKILL.md` |

## Triggers

"archive the log", "clean up pending review", "archive promoted entries",
"compact the log".

## Inputs

None.

## Reads / writes

- **Reads:** `_logs/PENDING_REVIEW.md`.
- **Writes:** moves `[PROMOTED]` and `[DISCARDED]` entries into
  `_logs/archive/YYYY-MM.md` (grouped by each entry's `date:`), trimming
  them from the review log.

## Key rules

- Archives **only** `[PROMOTED]` and `[DISCARDED]` — never `[PENDING]`,
  `[APPROVED]`, or `[DEFER]`.
- Moves, never destroys; entry content preserved exactly.
- One archive file per month.
- Entry with no `date:` → ask RM, don't guess the month.
- Confirms before archiving large batches (>20).

## Related

The final step of the core loop after [vault-promoter](vault-promoter.md).
Keeps [vault-status](vault-status.md) counts meaningful.
