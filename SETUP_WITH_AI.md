# Setup with AI

Give this file to a coding agent and ask it to install the Astra tiered delegation setup for your local Codex environment.

You do not need to clone the repository first.

Repository: https://github.com/Lisuiwen/GPT-Astra-delegator

If you already have the repository locally, use the local copy. Otherwise, when repository files are needed, fetch or clone the repository yourself. Prefer a temporary or tool-managed location unless the user explicitly wants to keep a local clone.

If network access is unavailable, continue with the policy embedded below and clearly report what could not be verified.

## Objective

Create two isolated behaviors.

### Normal Codex

Keep the user's existing behavior unchanged.
Do not load the Astra tiered delegation policy.

### Astra Orchestrator

When Astra is the primary tier:

- keep architecture, ambiguity, hard debugging, cross-module reasoning, and final acceptance on Astra
- delegate bounded routine work to lower tiers
- keep broad repository exploration in cheaper isolated contexts when practical
- return concise findings to Astra instead of large raw file dumps

Preferred routing:

- Luna → search, symbol lookup, call-chain discovery, repository exploration
- Terra → mechanical edits, lint, docs, fixed-spec tests
- Sol → straightforward implementation from a clear spec
- Astra → hard reasoning, integration decisions, final review

Do not create unnecessary nested delegation chains.
For trivial work, direct execution is better than spawning an agent.

## Embedded delegation policy

Use this policy if the repository cannot be fetched. If the repository is available, prefer the latest instructions/astra-delegation.md from the repository as the source of truth.

~~~
You are the Astra-tier primary orchestrator.

Keep on Astra:
- architecture and trade-off decisions
- ambiguous requirements
- hard debugging and cross-module reasoning
- integration decisions
- final review and acceptance

Delegate when practical:
- search, symbol lookup, repository exploration → Luna
- mechanical edits, lint, docs, fixed-spec tests → Terra
- straightforward implementation from a clear spec → Sol

Rules:
- Delegate bounded, low-risk work aggressively.
- Run independent subtasks in parallel when useful.
- Keep broad exploration in cheaper isolated contexts.
- Subagents return relevant paths and concise findings, not raw logs or full-file dumps.
- Avoid unnecessary nested delegation.
- Astra owns integration and final acceptance.
- For trivial tasks, execute directly instead of spawning an agent.
~~~

## Installation procedure

Inspect the local environment before changing anything.

Check:

- operating system
- Codex CLI/Desktop version
- current Codex configuration
- supported profile and instruction syntax
- available models and subagents
- existing instructions, plugins, or skills
- whether the current host supports model-pinned subagents

Do not assume the example config in this repository matches the installed Codex version.

If the repository is available, use:

- instructions/astra-delegation.md as the source of truth for behavior
- config/astra.config.toml as the profile and role declaration
- config/astra.config.toml, config/sol.config.toml, config/terra.config.toml, and config/luna.config.toml as model-binding examples

Map the role names to model IDs actually available in the environment. Keep the role names stable even when model IDs change.

## Safety requirements

- preserve unrelated existing settings
- back up every file before modifying it
- do not modify project-level AGENTS.md just to install this policy
- keep the Astra policy isolated from ordinary model sessions
- do not copy machine-specific paths from another computer
- prefer the smallest officially supported mechanism available in the installed Codex version
- do not invent unsupported config fields
- do not leave a permanent repository clone unless it is actually useful or the user asked for one

If profile-specific instructions are supported, prefer them.

If they are not supported, create the smallest isolated Astra launch/configuration path that preserves normal Codex behavior.

## Context isolation

Prefer this:

~~~
Luna
  → reads many files
  → returns paths + concise findings

Astra
  → reads only the files that matter for the decision
~~~

Avoid this when unnecessary:

~~~
Astra
  → scans the whole repository
  → accumulates large file contents
  → carries that context through the rest of the task
~~~

Do not blindly paste full subagent logs or entire files into the parent thread.

## Verification

After installation, verify all of the following:

1. Normal Codex still works.
2. Normal model sessions do not receive the Astra delegation policy.
3. The Astra tier receives the policy in its dedicated mode.
4. Astra can use Sol, Terra, and Luna when those bindings are available.
5. Existing Codex configuration still works.
6. No hard-coded path points to the repository author's machine.
7. A repository exploration task can be delegated without flooding the Astra parent context.

If possible, run a small test:

- ask Astra to inspect a small repository
- delegate exploration to Luna
- have Luna return only relevant paths and a concise summary
- confirm Astra performs the final reasoning/review

## Final report

After setup, report only:

- files created or changed
- how to start normal Codex
- how to start Astra orchestrator mode
- which model IDs were bound to Astra, Sol, Terra, and Luna
- whether delegation was verified
- whether context-isolated exploration was verified
- any limitations in the installed Codex version
- how to uninstall or restore the previous configuration

Do not only explain how to install it if you have permission and tools to perform the setup directly.
