# Setup with AI

Give this file to your coding agent and ask it to install the repository for your local Codex environment.

## Goal

Create two isolated behaviors:

### Normal Codex
Keep the user's current behavior unchanged.
Do not load the GPT-6 delegation policy.

### GPT-6 Orchestrator
When GPT-6 Astra is the primary agent:
- GPT-6 handles architecture, ambiguity, difficult debugging, cross-module reasoning, and final review.
- Routine work is delegated to cheaper available agents.

Preferred routing:
- Luna → search, symbol lookup, repository exploration
- Terra → mechanical edits, lint, docs, fixed-spec tests
- Sol → straightforward implementation from a clear spec
- GPT-6 → hard reasoning and final acceptance

Do not create unnecessary nested delegation chains.
For very small tasks, GPT-6 may execute directly.

## Installation task

Inspect the local environment before changing anything.

Check:
- operating system
- Codex version
- existing Codex configuration
- supported profile and instruction syntax
- available models and subagents
- existing instructions or skills

Do not assume the example config in this repository matches the installed Codex version.
Treat `config/gpt6.config.toml` as a template.
Treat `instructions/gpt6-delegation.md` as the source of truth for behavior.

Requirements:
- preserve unrelated existing settings
- back up files before modifying them
- do not modify project-level `AGENTS.md`
- keep the GPT-6 policy isolated from normal models
- remove or adapt machine-specific paths
- prefer the simplest officially supported mechanism in the installed Codex version

If profile-specific instructions are supported, use them.
Otherwise create an isolated GPT-6 configuration or launch entry without changing normal Codex behavior.

## Verification

After installation verify:
1. Normal Codex still works.
2. Normal models do not receive the GPT-6 delegation policy.
3. GPT-6 loads the delegation policy.
4. GPT-6 can delegate to available cheaper agents.
5. Existing Codex settings still work.

If possible, run a small delegation test: ask GPT-6 to inspect a small codebase and delegate repository exploration to a cheaper agent, then return only the summarized result.

## Final report

After setup, report only:
- files created or changed
- how to start normal Codex
- how to start GPT-6 orchestrator mode
- whether delegation was verified
- any limitations in the installed Codex version
- how to uninstall or restore the previous configuration

If you have filesystem and terminal access, perform the setup and verification directly instead of only explaining the steps.
