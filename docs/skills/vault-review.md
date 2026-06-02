# vault-review

Apply RM's review decisions to pending log entries from chat.

| | |
|---|---|
| **Command** | `/vault-review` |
| **Mode** | Write (status field only) |
| **SKILL.md** | `skills/vault-review/SKILL.md` |

## Triggers

"approve that entry", "approve all pending", "discard the last one",
"defer entry 3", "reject that idea", "review the log".

## Inputs

The decision and which entries it applies to, e.g. `approve all pending`,
`discard the agentwatch ones`, `defer the latest entry`.

## Reads / writes

- **Reads:** `_logs/PENDING_REVIEW.md`.
- **Writes:** flips the `status:` field on matched `[PENDING]` entries to
  `[APPROVED]` / `[DISCARDED]` / `[DEFER]`. Nothing else changes.

## Key rules

- Applies **only** decisions RM states — never approves on its own.
- Only `[PENDING]` entries are eligible (unless RM names an exception).
- Confirms before broad changes (>3 entries).
- Schema-preserving marker-flip: anchor on `summary:` + `status:`, one
  flip per edit.
- Doesn't promote — flipping to `[APPROVED]` is the end; the promoter
  moves it.

## Related

Sits between [vault-logger](vault-logger.md) and
[vault-promoter](vault-promoter.md) in the core loop. Chat-side
alternative to editing statuses manually in Obsidian.
