# Contributing

Contributions are welcome, but keep the project deliberately small.

## Project principles

Changes should support at least one of these goals:

- keep Astra focused on high-value reasoning
- route bounded routine work to the right lower tier
- reduce unnecessary growth of the Astra parent context
- keep setup simple and reversible
- avoid coupling the project to one machine or one transient Codex config shape

## Before opening a pull request

Please check that your change:

1. does not duplicate the delegation policy across multiple files
2. does not add machine-specific absolute paths
3. preserves normal Codex behavior outside the Astra setup
4. does not assume unsupported Codex configuration fields without verification
5. keeps user-facing instructions in English
6. keeps the setup process understandable by another coding agent
7. preserves the Astra/Sol/Terra/Luna role contract

## Scope

This project is intentionally not trying to become a large orchestration framework.

Features such as complex routing engines, dashboards, benchmarks, workflow modes, or deep task lifecycle management should only be added if they clearly support the core goal without making installation or maintenance substantially harder.

## Pull requests

Keep pull requests focused. Explain:

- the problem being solved
- why the change belongs in this repository
- how it affects normal Codex sessions
- how it affects Astra, Sol, Terra, and Luna routing
- how it was tested

If the change depends on a specific Codex version or host capability, state that explicitly.
