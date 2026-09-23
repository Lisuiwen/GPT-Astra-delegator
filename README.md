# Astra Delegator — Codex skill for tiered delegation on Astra

**Use Astra for the hardest decisions and high-precision multimodal work. Delegate bounded exploration and routine implementation to Luna and Sol so Astra's context and quota stay on work that needs them.**

Astra is strongest at architecture, difficult debugging, ambiguity, multimodal analysis, and final review. It is expensive to keep busy with repository exploration, repetitive edits, lint fixes, documentation, and straightforward implementation.

Astra Delegator gives Codex a small, tiered delegation policy so Astra behaves more like a tech lead than a worker.

## Who this is for

- Codex users who want Astra quota spent on hard reasoning and vision-heavy work, not repo search and routine edits
- People who already have Luna and Sol available and want a small routing policy
- Anyone who sees Astra's parent context fill up with exploration and mechanical work

## Who this is not for

- Anyone looking for a full orchestration framework, workflow engine, or packaged installer
- Setups with no Codex, no Astra, or no lower-tier models to delegate to
- Anyone expecting a guaranteed savings percentage

## The value

Without delegation:

~~~
Astra
  → search the repo
  → read dozens of files
  → make routine edits
  → write basic tests
  → fix lint
  → keep all that context around
~~~

With this setup:

~~~
Astra
  → architecture
  → difficult reasoning
  → high-precision multimodal work
  → task decomposition
  → final review

Luna            → search and repository exploration (luna_scout)
Sol             → mechanical edits and routine execution (sol_worker)
Sol             → straightforward implementation (sol_implementer)
~~~

The goal is simple:

> **Keep expensive reasoning small.**

The role names are stable. The model IDs in the agent files are bindings that can be updated for the models available in the current Codex installation.

## Fastest setup

You do not need to clone the repository first.

### Recommended: one-file install

1. Download SETUP_WITH_AI.md.
2. Give that file to your coding agent.
3. Say:

> Install this tiered Astra delegation setup for my local Codex environment. Preserve my normal Codex setup, map Astra/Luna/Sol to the models actually available, adapt it to my installed Codex version, and verify that it works.

SETUP_WITH_AI.md is self-contained. It includes the repository URL, the core delegation policy, and instructions for the agent to fetch or clone the repository automatically only when additional files are needed.

### Alternative: clone first

If you prefer to inspect everything before installation:

~~~
git clone https://github.com/Lisuiwen/GPT-Astra-delegator.git
~~~

Then give SETUP_WITH_AI.md to your coding agent.

The setup agent should inspect the local Codex version and configuration, back up existing settings, adapt the template, and verify the result instead of blindly copying configuration fields.

## Manual setup

Prefer the AI-assisted setup above unless you already understand your Codex configuration.

| What you need | Example / source | Purpose |
| --- | --- | --- |
| Astra profile | config/astra.config.toml | Isolates the tiered delegation policy from normal Codex sessions |
| Primary tier | `model = "gpt-6-astra"` in the example | Binds the Astra tier; replace if another Astra model ID is available |
| Delegation instructions | instructions/delegation.md | Single source of truth for routing and context isolation |
| Luna agent | agents/luna-scout.toml | Exploration, search, symbol lookup, and call-chain discovery |
| Sol worker | agents/sol-worker.toml | Mechanical edits, lint, docs, and fixed-spec tests |
| Sol implementer | agents/sol-implementer.toml | Straightforward implementation from a clear specification |
| Subagent support | Enable the supported agent/subagent mechanism in your Codex version | Allows Astra to hand bounded work to lower tiers |
| Delegation depth | `max_depth = 1` | Avoids nested delegation chains |
| Verification | Run one small repo-exploration task | Confirms normal sessions stay untouched and tiered delegation works |

A minimal manual flow is:

1. Back up your current Codex configuration.
2. Copy `agents/*.toml` into your Codex agents directory.
3. Copy or merge `config/astra.config.toml` and `instructions/delegation.md` into your Codex profile or `config.toml`.
4. Keep normal Codex sessions unchanged unless you want orchestration by default.
5. Start the Astra profile with `codex --profile astra` and verify delegation.

Do not copy the example config blindly. If a field or model ID is unsupported in your installed Codex version, use the simplest officially supported equivalent or use SETUP_WITH_AI.md and let an agent adapt it for you.

## Why this saves more than model cost

The second problem is context growth.

A long Codex task often becomes expensive because the strongest model keeps reading more files into its own context.

Instead:

~~~
Luna reads 30 files
        ↓
returns relevant paths + concise findings
        ↓
Astra reads only the files that matter for the decision
~~~

So the lower tier handles both the low-value work and the bulky exploration context.

## Design principles

- Astra-first — Astra owns architecture, multimodal analysis, integration, and final acceptance.
- Tiered delegation — Luna explores; Sol handles mechanical work and clear bounded implementation.
- Delegate low-risk work — search, mechanical edits, routine tests, lint, docs, and straightforward implementation should move down when practical.
- Keep context isolated — broad repository exploration should happen in subagent contexts whenever useful.
- No delegation chains — the root Astra agent owns decomposition and final acceptance.
- No unnecessary spawning — tiny tasks can still be done directly.
- Version-aware setup — let an AI adapt the configuration and model bindings to the installed Codex catalog.

## What is in this repository

~~~
README.md                    project overview
SETUP_WITH_AI.md             standalone AI-readable installer guide
config/astra.config.toml     Astra orchestrator profile
agents/luna-scout.toml       Luna exploration agent
agents/sol-worker.toml       Sol mechanical-work agent
agents/sol-implementer.toml  Sol implementation agent
instructions/delegation.md   single source of truth for behavior
LICENSE                      MIT license
CONTRIBUTING.md              contribution guide
~~~

The authoritative behavior policy is instructions/delegation.md.

The TOML files are templates. Codex configuration capabilities and model IDs can change, so the setup agent should choose the simplest supported mechanism available on the user's machine.

## What this project is not

This is not a full orchestration framework.

There are larger projects that provide workflow engines, verification stages, many routing modes, installers, and broader agent topologies.

This project deliberately solves one narrow problem:

> **Keep high-cost reasoning focused on work that needs it.**

Minimal policy. Minimal setup. Easy to remove.

## License

MIT. See LICENSE.
