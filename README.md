# GPT-6 Astra Context Saver

Use GPT-6 Astra for high-value reasoning. Push routine work and bulky repository exploration into cheaper, isolated subagent contexts.

This repository is intentionally small. It is not a full orchestration framework. It provides a lightweight policy and an AI-readable setup guide for users who want GPT-6 Astra to act more like a tech lead than a worker.

## Why

Long Codex tasks get expensive for two reasons:

1. **Model routing** — GPT-6 spends effort on work that cheaper models can handle.
2. **Context growth** — GPT-6 reads too many files directly, making later turns increasingly expensive.

The goal is to keep the expensive context small.

```text
GPT-6 Astra
  ├─ architecture / ambiguity / hard debugging / final review
  ├─ Luna  → search and repository exploration
  ├─ Terra → mechanical edits, lint, docs, fixed-spec tests
  └─ Sol   → straightforward implementation
```

Subagents should return concise findings instead of dumping raw file contents back into the parent context.

## Quick start

You do not need to understand Codex profiles or configuration files.

1. Clone or download this repository.
2. Give [`SETUP_WITH_AI.md`](./SETUP_WITH_AI.md) to your coding agent.
3. Tell it:

> Install this for my local Codex environment. Inspect my current Codex version and configuration first, adapt the setup to my machine, preserve my normal Codex behavior, and verify the result.

The setup agent should inspect the local Codex version and supported configuration mechanisms instead of blindly copying this repository's example config.

## Design goals

- **GPT-6-only policy** — ordinary Codex sessions should not receive these instructions.
- **Small parent context** — exploration belongs in cheaper isolated contexts when practical.
- **No unnecessary delegation** — trivial work can stay on the parent.
- **No delegation chains** — the root orchestrator owns decomposition and acceptance.
- **Version-aware setup** — configuration is adapted to the installed Codex version.
- **Minimal surface area** — one behavior file, one setup guide, one config example.

## Files

```text
README.md                           project overview
SETUP_WITH_AI.md                    AI-readable installation guide
config/gpt6.config.toml             example configuration template
instructions/gpt6-delegation.md     single source of truth for behavior
LICENSE                             MIT license
CONTRIBUTING.md                     contribution guide
```

## Important note

`config/gpt6.config.toml` is a **template**, not a guaranteed drop-in file. Codex capabilities and configuration syntax can change between versions. The setup agent should inspect the user's installed environment and choose the simplest officially supported mechanism available there.

The authoritative behavior policy is [`instructions/gpt6-delegation.md`](./instructions/gpt6-delegation.md).

## How this differs from larger orchestrators

Projects such as `codex-astra-luna-orchestrator`, `codex-orchestrator`, and `astral-orchestrator` provide broader routing, verification, modes, installers, and workflow logic.

This project deliberately focuses on one narrow problem:

> Keep expensive reasoning small.

It aims to be easy to understand, easy to remove, and easy for another coding agent to install.

## License

MIT. See [`LICENSE`](./LICENSE).
