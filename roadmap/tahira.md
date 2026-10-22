# Tahira: Core (engine) and Memory

**Repos:** `codehands-runner` (week 1), `codehands-contracts` (shared with Midhat), `codehands-engine` and `codehands-runtime` (from week 2), `codehands-memory` (from month 1, week 2).

**The goal:** a task goes in, a reviewed change comes out, nothing the model does can touch the host, and the second run on a repo is better than the first.

## Month 1, week by week

| Week | Repo | Build | Friday demo |
| --- | --- | --- | --- |
| 1 · Oct 19 to 23 | runner, contracts | Run Claude Code and Codex in a worktree per task. Events, stop, resume, approve, reject. Repo notes. Contracts frozen Friday | From the phone, a task runs in its own copy of the repo, and approving it puts the change on a branch ([guide](../weeks/week-1/tahira.md)) |
| 2 · Oct 26 to 30 | runtime, engine, memory | The repo's commands run in a locked Docker box. The engine moves a task through analyze, plan, implement, test and review, saving each step, with the same events as the runner. `MemoryStore` contract and stand-in. Repo profile v1 | Pick "Code Hands engine" in the app and watch it go step by step |
| 3 · Nov 2 to 6 | runtime, engine, memory | Tools: list, read, search and patch, limited to the repo. Test step and a repair loop capped at 2. Memory: a tree-sitter symbol index and a repo map | Our engine fixes a small bug and the change shows on the phone |
| 4 · Nov 9 to 13 | engine, memory | Review step. Checkpoint after every step, resume after `kill -9`. Tests that try to trick it. The second task starts with what the first learned | **M1:** kill the daemon halfway and the task still finishes |

Plug-ins: daily in week 1 with Midhat. Oct 30: engine in both apps (Midhat), step recording (Talha). Nov 6: model per step (Memoona).

## Months 2 to 6

| Month | Core | Memory | Done when |
| --- | --- | --- | --- |
| 2 | YAML workflows, external agents as a step, approval gate, two runs at once in separate worktrees | Hybrid search (sqlite-vec plus BM25), user memory, recall in the plan step under a token budget | A three-step workflow with one external agent step resumes after a crash. A table of plan quality with memory on and off |
| 3 | Branch per run, PRs through a GitHub App, video verify, hardening | Context compaction, memory viewer data, memory as editable markdown | The team uses it daily for a week with no manual DB edits |
| 4 | Router hooks, parallel candidates, a queue with leases shared by two daemons | Learning from eval results, shared notes across models, sync protocol with vector clocks | A measured gain from memory on 50 tasks |
| 5 | Worker image, laptop to cloud handoff with a git bundle | Sync service, encryption with per-user keys | A remote worker uses memory written on the laptop an hour earlier |
| 6 | gVisor option, Firecracker spike, threat model, v0.1 | Self-hosted sync, retention and delete-everything controls | Self-hosted with privacy controls documented |

## Weekend reading, month 1

| Before week | Watch or read | Spike |
| --- | --- | --- |
| 1 | Claude Code headless mode, CLI reference, `git worktree`, `codex exec` | `claude -p` on the fixture repo, save the JSONL |
| 2 | Docker in 100 Seconds (Fireship), the Docker getting started guide, XState concepts, the Drizzle SQLite quickstart | `npm test` in a container: 1 GB, no network, 60 s |
| 3 | A 10-minute SWE-agent or OpenHands demo, the `git apply` man page, the tree-sitter playground | Apply a patch from Node that refuses `../secret` |
| 4 | Stripe on idempotent requests, the Letta quickstart | `kill -9` a run mid-step, restart, see what it takes to continue |

The deeper learning kits for months 2 to 6 are in the plan, under *SIG Core* and *SIG Memory*.
