# Setup with AI

Give this file to your coding agent and ask it to install this repository for your local Codex environment.

The agent should perform the setup directly when it has filesystem and terminal access.

## Objective

Create two isolated behaviors.

### Normal Codex

Keep the user's existing behavior unchanged.

Do not load the GPT-6 delegation policy.

### GPT-6 Astra Orchestrator

When GPT-6 Astra is the primary agent:

- keep architecture, ambiguity, hard debugging, cross-module reasoning, and final acceptance on GPT-6
- delegate bounded routine work to cheaper available agents
- keep repository exploration in cheaper isolated contexts when practical
- return concise findings to GPT-6 instead of large raw file dumps

Preferred routing:

- Luna → search, symbol lookup, call-chain discovery, repository exploration
- Terra → mechanical edits, lint, docs, fixed-spec tests
- Sol → straightforward implementation from a clear spec
- GPT-6 Astra → hard reasoning, integration decisions, final review

Do not create unnecessary nested delegation chains.
For trivial work, direct execution is better than spawning an agent.

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

Use:

- `instructions/gpt6-delegation.md` as the source of truth for behavior
- `config/gpt6.config.toml` only as an example template

## Safety requirements

- preserve unrelated existing settings
- back up every file before modifying it
- do not modify project-level `AGENTS.md` just to install this policy
- keep the GPT-6 policy isolated from ordinary model sessions
- do not copy machine-specific paths from another computer
- prefer the smallest officially supported mechanism available in the installed Codex version
- do not invent unsupported config fields

If profile-specific instructions are supported, prefer them.

If they are not supported, create the smallest isolated GPT-6 launch/configuration path that preserves normal Codex behavior.

## Context isolation

The purpose is not only to route cheaper work to cheaper models. It is also to keep the GPT-6 parent context compact.

Prefer this:

```text
cheap explorer
  → reads many files
  → returns paths + concise findings

GPT-6 Astra
  → reads only the files that matter for the decision
```

Avoid this when unnecessary:

```text
GPT-6 Astra
  → scans the whole repository
  → accumulates large file contents
  → carries that context through the rest of the task
```

Do not blindly paste full subagent logs or entire files into the parent thread.

## Verification

After installation, verify all of the following:

1. Normal Codex still works.
2. Normal model sessions do not receive the GPT-6 delegation policy.
3. GPT-6 Astra receives the policy in its dedicated mode.
4. GPT-6 can use the cheaper agents actually available in this environment.
5. Existing Codex configuration still works.
6. No hard-coded path points to the original repository author's machine.
7. A repository exploration task can be delegated without flooding the GPT-6 parent context.

If possible, run a small test:

- ask GPT-6 to inspect a small repository
- delegate exploration to a cheaper agent
- have the subagent return only relevant paths and a concise summary
- confirm GPT-6 performs the final reasoning/review

## Final report

After setup, report only:

- files created or changed
- how to start normal Codex
- how to start GPT-6 Astra orchestrator mode
- which models/subagents were actually available
- whether delegation was verified
- whether context-isolated exploration was verified
- any limitations in the installed Codex version
- how to uninstall or restore the previous configuration

Do not only explain how to install it if you have permission and tools to perform the setup directly.
