# vault-status

Summarise the current state of the vault.

| | |
|---|---|
| **Command** | `/vault-status` |
| **Mode** | Read-only |
| **SKILL.md** | `skills/vault-status/SKILL.md` |

## Triggers

"vault status", "what's in my vault", "show pending", "what's open",
"where do things stand", "vault summary".

## Inputs

None.

## Reads / writes

- **Reads:** `projects/_INDEX.md`, `_logs/PENDING_REVIEW.md`, each
  project's `ISSUES.md` and `PROGRESS.md`, `ideas/*.md`.
- **Writes:** nothing.

## Output

- Projects table (status, phase, open-issue count).
- Pending-review counts by status.
- Active-idea counts by domain.

## Key rules

- Counts from actual files — no speculation.
- Read-only.
- Single-screen, scannable.
- Missing `current_phase` shows `—`, not "unknown".

## Related

Big-picture counterpart to [vault-find](vault-find.md) (locate something)
and [vault-read](vault-read.md) (read one thing in full).
