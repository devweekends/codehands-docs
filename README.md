# Code Hands AI

A local-first coding agent platform. It takes a repository-level task, plans it, implements it, tests it, reviews it, and hands a person a change to approve. Built over six months, Oct 19, 2026 to Apr 18, 2027.

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

| Repo | Owner | What |
| --- | --- | --- |
| [codehands-docs](https://github.com/devweekends/codehands-docs) | everyone | This repo: plan, roadmap, decisions, the design below |
| [codehands-contracts](https://github.com/devweekends/codehands-contracts) | Midhat, Tahira (every consumer approves changes) | Shared types: local DB schema, `Runner`, cloud API, session states |
| [codehands-desktop](https://github.com/devweekends/codehands-desktop) | Tania | The desktop app |
| codehands-daemon (to be created) | Midhat | The laptop daemon, the local DB and the `codehands` CLI, moved out of `codehands-backend` |
| [codehands-agent](https://github.com/devweekends/codehands-agent) | Tahira | The runner: agent CLIs, models, worktrees, memory |
| [codehands-backend](https://github.com/devweekends/codehands-backend) | Memoona | The cloud state API and the sync client |
| [codehands-web](https://github.com/devweekends/codehands-web) | none | Empty. No role in the current design |
