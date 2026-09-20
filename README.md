# Astra Delegator — Codex skill to save GPT-6 Astra quota by tiered delegation

**Use GPT-6 Astra for the hardest decisions. Let Codex delegate bounded work to Sol, Terra, and Luna so Astra's context and quota stay on work that needs them.**

Astra is strongest at architecture, difficult debugging, ambiguity, and final review. It is expensive to keep busy with repository exploration, repetitive edits, lint fixes, documentation, and straightforward implementation.

Astra Delegator gives Codex a small, tiered delegation policy so Astra behaves more like a tech lead than a worker.

## Who this is for

- Codex users who want GPT-6 Astra quota spent on hard reasoning, not repo search and routine edits
- People who already have cheaper models (Sol, Terra, Luna, or equivalents) and want a small routing policy
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
  → task decomposition
  → final review

Luna  → search and repository exploration
Terra → mechanical edits, lint, docs, fixed-spec tests
Sol   → straightforward implementation
~~~

The goal is simple:

> **Keep expensive reasoning small.**

The role names are stable, while the model IDs are bindings that can be updated for the models available in the current Codex installation. Exact savings vary by workload, so this project intentionally avoids claiming a fixed percentage.

## Fastest setup

You do not need to clone the repository first.

### Recommended: one-file install

1. Download SETUP_WITH_AI.md.
2. Give that file to your coding agent.
3. Say:

> Install this tiered Astra delegation setup for my local Codex environment. Preserve my normal Codex setup, map Astra/Sol/Terra/Luna to the models actually available, adapt it to my installed Codex version, and verify that it works.

SETUP_WITH_AI.md is self-contained. It includes the repository URL, the core delegation policy, and instructions for the agent to fetch or clone the repository automatically only when additional files are needed.

### Alternative: clone first

If you prefer to inspect everything before installation:

~~~
git clone https://github.com/Lisuiwen/GPT-Astra-delegator.git
~~~

Then give SETUP_WITH_AI.md to your coding agent.

The setup agent should inspect the local Codex version and configuration, back up existing settings, adapt the template, and verify the result instead of blindly copying configuration fields.

## Manual setup

Prefer the AI-assisted setup above unless you already understand your Codex configuration. The exact syntax can change between Codex versions, so verify the fields supported by your installed version before applying them.

| What you need | Example / source | Purpose |
| --- | --- | --- |
| Astra profile | config/astra.config.toml | Isolates the tiered delegation policy from normal Codex sessions |
| Primary tier | model = "gpt-6-astra" in the example | Binds the Astra tier; replace it if another Astra model ID is available |
| Delegation instructions | instructions/astra-delegation.md | Single source of truth for routing and context isolation |
| Luna binding | config/luna.config.toml | Exploration, search, symbol lookup, and call-chain discovery |
| Terra binding | config/terra.config.toml | Mechanical edits, lint, docs, and fixed-spec tests |
| Sol binding | config/sol.config.toml | Straightforward implementation from a clear specification |
| Subagent support | Enable the supported agent/subagent mechanism in your Codex version | Allows Astra to hand bounded work to lower tiers |
| Delegation depth | Keep it shallow | Avoids Astra → Sol → Terra → Luna chains |
| Verification | Run one small repo-exploration task | Confirms normal sessions stay untouched and tiered delegation works |

The role names are the policy contract. The model IDs in the TOML files are only environment-specific bindings and should be changed when the installed catalog uses different IDs.

A minimal manual flow is:

1. Back up your current Codex configuration.
2. Copy or reference instructions/astra-delegation.md from an Astra profile or launch path.
3. Adapt config/astra.config.toml and the three role config files to fields and model IDs actually supported by your installed Codex version.
4. Keep normal Codex sessions unchanged.
5. Start the Astra profile and verify that exploration is delegated while Astra keeps final reasoning and review.

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

- Astra-first — Astra owns architecture, integration, and final acceptance.
- Tiered delegation — Luna explores, Terra executes routine work, and Sol implements clear bounded changes.
- Delegate low-risk work — search, mechanical edits, routine tests, lint, docs, and straightforward implementation should move down when practical.
- Keep context isolated — broad repository exploration should happen in subagent contexts whenever useful.
- No delegation chains — the root Astra agent owns decomposition and final acceptance.
- No unnecessary spawning — tiny tasks can still be done directly.
- Version-aware setup — let an AI adapt the configuration and model bindings to the installed Codex version.

## What is in this repository

~~~
README.md                           project overview
SETUP_WITH_AI.md                    standalone AI-readable installer guide
config/astra.config.toml             Astra profile and tier declarations
config/luna.config.toml              Luna model binding
config/terra.config.toml             Terra model binding
config/sol.config.toml               Sol model binding
instructions/astra-delegation.md     single source of truth for behavior
LICENSE                             MIT license
CONTRIBUTING.md                     contribution guide
~~~

The authoritative behavior policy is instructions/astra-delegation.md.

The TOML files are templates. Codex configuration capabilities and model IDs can change, so the setup agent should choose the simplest supported mechanism available on the user's machine.

## What this project is not

This is not a full orchestration framework.

There are larger projects that provide workflow engines, verification stages, many routing modes, installers, and broader agent topologies.

This project deliberately solves one narrow problem:

> **Keep high-cost reasoning focused on work that needs it.**

Minimal policy. Minimal setup. Easy to remove.

## License

MIT. See LICENSE.
