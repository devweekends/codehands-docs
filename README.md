# Code Hands AI

A local-first coding agent platform. It takes a repository-level task, plans it, implements it, tests it in a sandbox, reviews it, and hands a person a change to approve. Five people build it over six months, Oct 19, 2026 to Apr 18, 2027.

This repo holds the plan, the roadmap, the weekly guides and the decisions. Code lives in one repo per part (see [decision 0001](decisions/0001-separate-repos.md)).

## Start here

| If you want | Read |
| --- | --- |
| The whole plan | [plan/six-month-sig-build-plan.md](plan/six-month-sig-build-plan.md) |
| What ships when | [roadmap/README.md](roadmap/README.md) |
| Your week | [weeks/](weeks/) |
| How repos depend on each other, how to change a contract | [CONTRIBUTING.md](CONTRIBUTING.md) |
| Why we decided something | [decisions/](decisions/) |
| The Linear import | [plan/linear-import.csv](plan/linear-import.csv) |

## Repos

One repo per part, each with a single owner. Repos marked *proposed* are created when their owner starts on them.

| Repo | Owner | What | From |
| --- | --- | --- | --- |
| `codehands-docs` | everyone | This repo: plan, roadmap, weekly guides, decisions | Week 1 |
| `codehands-contracts` | Tahira, Midhat (every consumer approves changes) | Shared types, event names, session states, the `Runner` interface | Week 1 |
| `codehands-runner` | Tahira | Runs Claude Code or Codex in a git worktree per task, turns output into events | Week 1 |
| `codehands-cli` | Midhat | The `codehands` command and the laptop daemon | Week 1 |
| `codehands-api` | Midhat | State API on the Linux server: sessions, events, commands | Week 1 |
| `codehands-desktop` | Tania | Tauri desktop app | Week 1 |
| `codehands-web` | Memoona | Phone web app on Vercel | Week 1 |
| `codehands-engine` | Tahira | Our own engine: steps, checkpoints, queue (*proposed*) | Week 2 |
| `codehands-runtime` | Tahira | Agent tools and the Docker sandbox (*proposed*) | Week 2 |
| `codehands-memory` | Tahira | Repo, task and user memory (*proposed*) | Month 1, week 2 |
| `codehands-gateway` | Tania | Our model code: providers, streaming, fallbacks (*proposed*) | Week 2 |
| `codehands-pricing` | Memoona | Price list, cost per call, model per step, budgets (*proposed*) | Week 1 |
| `codehands-evals` | Talha | Practice tasks, scoring, tracing, fixtures (*proposed*) | Week 1 |

Names other than Tahira's are suggestions. Each owner picks theirs and updates this table.
