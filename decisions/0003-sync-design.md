# 0003: Sync design, one records table and push/pull by cursor

**Status:** proposed, Oct 29, 2026 · **Owner:** Memoona · **Issue:** COD-313

## Context

Signing in on a second laptop should bring your sessions, memory and preferences with it. Tasks always run on a laptop, so the cloud only stores state. The risk is the cloud ending up holding things it should never have: repo files, credentials, local paths or raw agent output.

## Decision

- All synced data lives in one `records` table in Postgres, keyed by user, kind and id. Each record has a version, a deleted flag, a JSON `data` field and a `seq` number from a database sequence. `seq` goes up every time a record is created or changed.
- The laptop makes every record id, so a resend never creates a copy. Events use `<sessionId>:<seq>`. Projects use the hash of the origin URL, never the folder path.
- Push sends a batch of changes (at most 500). Pull sends a cursor and gets everything with a higher `seq`, at most 500 at a time, plus a `hasMore` flag.
- Conflicts: for projects, sessions, memory and preferences the higher version wins, and a lower one is rejected as stale. Events are append only, so a duplicate is ignored.
- What syncs: account and devices, projects, sessions, events, memory, preferences, and small diffs.
- What never syncs: repo files and worktrees, Claude and Codex logins and API keys, the app token, raw agent output and big logs, and local folder paths.
- The server checks every pushed record and rejects it if it has a forbidden field name (path, stdout, apiKey and similar), a value that looks like a local path or a secret, or a size over 64 KB. Unit tests cover this.
- Sign-in is GitHub only. Each laptop gets its own random device token, only a hash of it is stored, and logout revokes only that laptop. Every sync request filters by the signed-in user.
- Hosting: Neon for Postgres, with the API host in the same region, because each request makes several database calls.
- Size caps (proposed): 64 KB per record and 500 records per batch are enforced. A 1 MB cap per diff is not enforced yet.

## Consequences

| Good | Cost, and how we handle it |
| --- | --- |
| One table and two routes are easy to review, and a resend is harmless | `data` is loose JSON, so a bad field shape is only caught by the contract types. Add per-kind checks later |
| The safety check runs on every record, so one bad record doesn't block a batch | A name-based check can miss odd cases. It is a safety net, and the never-sync rule still lives in what the daemon chooses to push |
| Each laptop has its own token, so logout can't lock out the others | Each sign-in creates a new device row. Open question below |
| The higher version wins, so there is no merge logic | Two laptops editing the same preference offline lose the older edit |

## Open questions

- Should the same laptop reuse its device row by name?
- Should the server enforce the legal session moves (C5), or leave that to the daemon?
- Should events and diffs sync in week 2, or only sessions, memory and preferences?

