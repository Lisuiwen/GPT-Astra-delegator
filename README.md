# codex-gpt6-astra-context

Use GPT-6 for judgment. Delegate routine coding work to cheaper models.

## What it does

This repository provides a small GPT-6-specific orchestration policy for Codex:

- **GPT-6 Astra** — architecture, ambiguity, hard debugging, final review
- **Sol** — straightforward implementation
- **Terra** — mechanical edits, tests, lint, docs
- **Luna** — search and repository exploration

The GPT-6 policy is intended to stay isolated from normal Codex sessions.

## Quick start

You do not need to configure Codex manually.

1. Clone or download this repository.
2. Open [`SETUP_WITH_AI.md`](./SETUP_WITH_AI.md).
3. Give that file to a coding agent and say:

> Install this for my local Codex environment. Inspect my current Codex version and configuration first, then adapt and verify it without breaking my normal setup.

The agent should inspect the installed Codex version, adapt the template to the local machine, back up existing settings, install the GPT-6-specific behavior, and verify delegation.

## Files

```text
config/gpt6.config.toml              example profile/config template
instructions/gpt6-delegation.md      single source of truth for delegation behavior
SETUP_WITH_AI.md                     AI-readable installation guide
```

## Design principle

Keep the always-loaded policy small.

The expensive model should spend tokens on decisions that benefit from stronger reasoning, while bounded low-risk work runs in cheaper isolated contexts.

`config/gpt6.config.toml` is intentionally a template because Codex configuration capabilities can change between versions. Let the setup agent inspect the user's installed version rather than blindly copying configuration fields.
