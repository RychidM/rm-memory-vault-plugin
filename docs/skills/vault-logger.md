# vault-logger

Append a structured entry to the pending-review log.

| | |
|---|---|
| **Command** | `/vault-log` |
| **Mode** | Write (append-only) |
| **SKILL.md** | `skills/vault-logger/SKILL.md` |

## Triggers

"log this", "save this to my vault", "note this down", "remember this",
"capture this", "log it".

## Inputs

Inferred from the conversation (asks only if genuinely ambiguous):

- `type` — `idea` / `decision` / `issue` / `resolution` / `progress` / `context`
- `project` — exact vault project name, or `general`
- `domain` — only for `type: idea`: `technical` / `product` / `content` / `business`
- `summary` — one specific line

## Reads / writes

- **Writes:** appends one entry block to `_logs/PENDING_REVIEW.md`
  (creates the file with its header if missing).
- Every entry carries `status: [PENDING]`.

## Key rules

- Append only — never overwrites or deletes.
- One entry per distinct topic.
- `type: idea` requires `domain`; omit `domain` otherwise.
- `type: resolution` should name the issue ID (e.g. "Resolves [ISSUE-001]")
  so the promoter can match it.

## Related

[vault-review](vault-review.md) → [vault-promoter](vault-promoter.md) →
[vault-log-archive](vault-log-archive.md) — the rest of the loop.
For changing existing content instead of capturing new, use
[vault-edit](vault-edit.md).
