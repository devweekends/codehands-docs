# 0001: One repo per part instead of a monorepo

**Status:** accepted, Oct 19, 2026 · **Replaces:** "One monorepo" in the plan's *Architecture and repository structure* section

## Context

The plan put everything in one pnpm and Turborepo monorepo, with ownership through CODEOWNERS. The team has worked in one shared repo before and found that it couples people:

- One person's broken branch, dependency or pipeline blocks everyone else.
- A bad or compromised dependency in one part reaches every part.
- Owners can't install dependencies, branch, release or run CI on their own schedule.

The plan already gives every part a single owner and a typed contract with a stand-in. That is the setup that makes separate repos cheap.

## Decision

- One GitHub repo per part, named `codehands-<part>`, owned by one person (table in the [README](../README.md)).
- Shared shapes live in `codehands-contracts`, versioned with git tags. Consumers pin a tag: `"@codehands/contracts": "github:<org>/codehands-contracts#v0.1.0"`. While a pair is building against each other in week 1, `file:../codehands-contracts` with both repos cloned side by side is fine.
- A library one repo calls directly, like the runner the daemon calls, is a dependency pinned the same way.
- The plan, roadmap, weekly guides and decisions live in `codehands-docs`.
- A repo is created when its owner starts on it, not before.

## Consequences

| Good | Cost, and how we handle it |
| --- | --- |
| Each owner installs, branches, releases and runs CI alone | A change across repos takes several PRs. Contract changes batch into the Wednesday sync |
| A bad dependency or broken build stays in one repo | Versions can drift. Every repo pins the contracts tag, and bumping it is a deliberate PR |
| Clear ownership without CODEOWNERS | No single `pnpm dev --mock` for the whole product. Each repo ships its own stand-in (the fake runner, the fake daemon), and `codehands-cli --mock` wires them together |
| Smaller CI per repo | An end-to-end check needs several repos checked out. The Friday plug-in does this by hand in month 1, and a CI job in `codehands-cli` checks out the others from month 2 |

## To update

- The plan's *Architecture and repository structure* section still shows the monorepo tree. Read it as "one repo per folder".
- `imtahirabatool/codehands-ai` (the monorepo skeleton) is archived once the parts move out.
