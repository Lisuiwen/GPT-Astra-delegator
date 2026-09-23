# Astra Delegator

Codex skill: **Astra orchestrator** with tiered delegation to **Luna** (explore) and **Sol** (mechanical work + implementation). Keeps **multimodal and hard reasoning on Astra**.

Use Astra for architecture, ambiguity, difficult debugging, high-precision multimodal work, integration, and final acceptance. Delegate bounded exploration and routine implementation to Luna and Sol so Astra's context and quota stay on work that needs them.

## Role routing

| Role | Agent | Responsibility |
| --- | --- | --- |
| **Astra** | primary orchestrator | architecture, ambiguity, hard debugging, integration, high-precision multimodal work, final acceptance |
| **Luna** | `luna_scout` | read-only exploration, search, symbol lookup, call-chain discovery |
| **Sol** | `sol_worker` | mechanical edits, lint, docs, fixed-spec tests |
| **Sol** | `sol_implementer` | straightforward implementation from a clear spec |

Astra does not delegate multimodal or vision-heavy tasks unless the needed facts are already extracted.

## Who this is for

- Codex users who want Astra quota spent on hard reasoning and vision-heavy work, not repo search and routine edits
- People who already have Luna and Sol available and want a small routing policy
- Anyone who sees Astra's parent context fill up with exploration and mechanical work

## Who this is not for

- Anyone looking for a full orchestration framework, workflow engine, or packaged installer
- Setups with no Codex, no Astra, or no Luna/Sol bindings to delegate to
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

Luna  → search and repository exploration
Sol   → mechanical edits and routine execution
Sol   → straightforward implementation
~~~

The goal is simple:

> **Keep expensive reasoning small.**

The role names are the stable contract. The model bindings in the TOML files can be updated for whatever IDs your Codex installation exposes for Astra, Luna, and Sol.

## Fastest setup

You do not need to clone the repository first.

### Recommended: one-file install

1. Download SETUP_WITH_AI.md.
2. Give that file to your coding agent.
3. Say:

> Install this tiered Astra delegation setup for my local Codex environment. Preserve my normal Codex setup, map Astra/Luna/Sol to the models actually available, adapt it to my installed Codex version, and verify that it works.

SETUP_WITH_AI.md is self-contained. It includes the repository URL, the core delegation policy, and instructions for the agent to fetch or clone the repository automatically only when additional files are needed.

### Alternative: clone first

~~~
git clone https://github.com/Lisuiwen/GPT-Astra-delegator.git
~~~

Then give SETUP_WITH_AI.md to your coding agent.

The setup agent should inspect the local Codex version and configuration, back up existing settings, adapt the template, and verify the result instead of blindly copying configuration fields.

## Manual setup

| What you need | Source | Purpose |
| --- | --- | --- |
| Astra profile | `config/astra.config.toml` | Orchestrator profile and delegation policy |
| Delegation policy | `instructions/delegation.md` | Single source of truth for routing and context isolation |
| Luna agent | `agents/luna-scout.toml` | Exploration, search, symbol lookup, call-chain discovery |
| Sol worker | `agents/sol-worker.toml` | Mechanical edits, lint, docs, fixed-spec tests |
| Sol implementer | `agents/sol-implementer.toml` | Straightforward implementation from a clear specification |
| Subagent support | Codex multi-agent / subagent mechanism | Lets Astra hand bounded work to Luna and Sol |
| Delegation depth | `max_depth = 1` | Avoids nested delegation chains |

Minimal flow:

1. Back up your current Codex configuration.
2. Copy `agents/*.toml` into your Codex agents directory.
3. Copy or merge `config/astra.config.toml` and `instructions/delegation.md` into your Codex profile or `config.toml`.
4. Keep normal Codex sessions unchanged unless you want orchestration by default.
5. Start Astra mode with `codex --profile astra` and verify delegation.

Do not copy the example config blindly. If a field or model binding is unsupported in your installed Codex version, use the simplest officially supported equivalent or use SETUP_WITH_AI.md and let an agent adapt it for you.

## Why this saves more than model cost

The second problem is context growth.

A long Codex task often becomes expensive because Astra keeps reading more files into its own context.

Instead:

~~~
Luna reads many files
        ↓
returns relevant paths + concise findings
        ↓
Astra reads only the files that matter for the decision
~~~

So Luna and Sol handle both the low-value work and the bulky exploration context.

## Design principles

- **Astra-first** — Astra owns architecture, multimodal analysis, integration, and final acceptance.
- **Tiered delegation** — Luna explores; Sol handles mechanical work and clear bounded implementation.
- **Delegate low-risk work** — search, mechanical edits, routine tests, lint, docs, and straightforward implementation should move down when practical.
- **Keep context isolated** — broad repository exploration should happen in subagent contexts whenever useful.
- **No delegation chains** — the root Astra agent owns decomposition and final acceptance.
- **No unnecessary spawning** — tiny tasks can still be done directly.

## Repository layout

~~~
README.md
SETUP_WITH_AI.md
config/astra.config.toml
agents/luna-scout.toml
agents/sol-worker.toml
agents/sol-implementer.toml
instructions/delegation.md
LICENSE
CONTRIBUTING.md
~~~

The authoritative behavior policy is `instructions/delegation.md`.

The TOML files are templates. Adapt them to the Codex capabilities and model bindings available on your machine.

## What this project is not

This is not a full orchestration framework.

This project deliberately solves one narrow problem:

> **Keep high-cost reasoning focused on work that needs it.**

Minimal policy. Minimal setup. Easy to remove.

## License

MIT. See LICENSE.
