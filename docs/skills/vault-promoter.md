# vault-promoter

Move `[APPROVED]` entries from the log to their destination files.

| | |
|---|---|
| **Command** | `/vault-promote` |
| **Mode** | Write (transform in place) |
| **SKILL.md** | `skills/vault-promoter/SKILL.md` |

## Triggers

"promote approved entries", "process the log", "file these entries",
"promote", "run the promoter".

## Inputs

None — reads decisions from the log's `status:` fields.

## Reads / writes

- **Reads:** `_logs/PENDING_REVIEW.md`.
- **Writes:** for each `[APPROVED]` entry, appends/transforms the
  destination, then flips that entry to `[PROMOTED]`.

### Type → destination

| Type | Destination |
|------|-------------|
| `issue` | `projects/{project}/ISSUES.md` → Open Issues, next `[ISSUE-NNN]` |
| `resolution` | `ISSUES.md` → move matched issue to Resolved |
| `decision` | `projects/{project}/OVERVIEW.md` → Key Decisions table |
| `progress` | `projects/{project}/PROGRESS.md` → current phase |
| `context` | `OVERVIEW.md` → Notes |
| `idea` | `ideas/{domain}.md` → Active Ideas (prepended) |

Project resolves `projects/{project}/` then `projects/*/{project}/`.

## Key rules

- Processes only `[APPROVED]` entries.
- Flips `[APPROVED]` → `[PROMOTED]` immediately after each write (not
  batched), using the schema-preserving anchor.
- Issue IDs are sequential across Open + Resolved.
- Never deletes; missing destination folder → skip and report.

## Related

Consumes what [vault-review](vault-review.md) approves;
[vault-log-archive](vault-log-archive.md) later clears the `[PROMOTED]`
entries it leaves behind.
