# GPT-6 Astra Context Saver

**Use GPT-6 Astra for the hard decisions. Let cheaper models do the routine work.**

GPT-6 Astra is excellent at architecture, difficult debugging, ambiguity, and final review. It is also expensive to keep busy with repository exploration, repetitive edits, lint fixes, documentation, and straightforward implementation.

This project gives Codex a small GPT-6-specific delegation policy so Astra behaves more like a tech lead than a worker.

## The value

Without delegation:

```text
GPT-6 Astra
  → search the repo
  → read dozens of files
  → make routine edits
  → write basic tests
  → fix lint
  → keep all that context around
```

With this setup:

```text
GPT-6 Astra
  → architecture
  → difficult reasoning
  → task decomposition
  → final review

Luna  → search and repository exploration
Terra → mechanical edits, lint, docs, fixed-spec tests
Sol   → straightforward implementation
```

The goal is simple:

> **Keep expensive reasoning small.**

In practical long-running Codex tasks, the difference is noticeable: Astra spends less time on routine execution and broad repository exploration, while its parent context stays smaller. Exact savings vary by workload, so this project intentionally avoids claiming a fixed percentage.

## Fastest setup

You do **not** need to clone the repository first.

### Recommended: one-file install

1. Download [`SETUP_WITH_AI.md`](./SETUP_WITH_AI.md).
2. Give that file to your coding agent.
3. Say:

> Install this for my local Codex environment. Preserve my normal Codex setup, make the delegation policy GPT-6-only, adapt it to my installed Codex version, and verify that it works.

`SETUP_WITH_AI.md` is self-contained. It includes the repository URL, the core delegation policy, and instructions for the agent to fetch or clone the repository automatically only when additional files are needed.

### Alternative: clone first

If you prefer to inspect everything before installation:

```bash
git clone https://github.com/Lisuiwen/codex-gpt6-astra-context.git
```

Then give `SETUP_WITH_AI.md` to your coding agent.

The setup agent should inspect the local Codex version and configuration, back up existing settings, adapt the template, and verify the result instead of blindly copying configuration fields.

## Manual setup

Prefer the AI-assisted setup above unless you already understand your Codex configuration. The exact syntax can change between Codex versions, so verify the fields supported by your installed version before applying them.

| What you need | Example / source | Purpose |
| --- | --- | --- |
| GPT-6-only launch path or profile | `config/gpt6.config.toml` | Keeps the delegation policy isolated from normal Codex sessions |
| Primary model | `gpt-6-astra` | Uses Astra only for high-value reasoning and final acceptance |
| Reasoning effort | `medium` | Good default balance for long-running tasks; raise only when needed |
| Delegation instructions | `instructions/gpt6-delegation.md` | Single source of truth for routing and context-isolation behavior |
| Subagent support | Enable the supported agent/subagent mechanism in your Codex version | Allows Astra to hand bounded work to cheaper models |
| Default worker | Terra is a reasonable default when supported | Handles mechanical edits and routine execution |
| Exploration worker | Luna when supported | Handles search, symbol lookup, call-chain discovery, and broad repo exploration |
| Implementation worker | Sol when supported | Handles straightforward implementation from a clear spec |
| Delegation depth | Keep it shallow | Avoids GPT-6 → Sol → Terra → Luna chains |
| Verification | Run one small repo-exploration task | Confirms that normal sessions stay untouched and GPT-6 delegates correctly |

A minimal manual flow is:

1. Back up your current Codex configuration.
2. Copy or reference `instructions/gpt6-delegation.md` from a GPT-6-only profile or launch path.
3. Adapt `config/gpt6.config.toml` to the fields actually supported by your installed Codex version.
4. Keep normal Codex sessions unchanged.
5. Start GPT-6 mode and verify that repository exploration is delegated while GPT-6 keeps the final reasoning and review.

Do **not** copy the example config blindly. If a field is unsupported in your installed Codex version, use the simplest officially supported equivalent or use `SETUP_WITH_AI.md` and let an agent adapt it for you.

## Why this saves more than model cost

The second problem is **context growth**.

A long Codex task often becomes expensive because the strongest model keeps reading more files into its own context.

Instead:

```text
Luna reads 30 files
        ↓
returns relevant paths + concise findings
        ↓
GPT-6 reads only the files that matter
```

So the cheaper model handles both the low-value work **and** the bulky exploration context.

## Design principles

- **GPT-6-only** — normal Codex sessions should not receive this policy.
- **Delegate low-risk work** — search, mechanical edits, routine tests, lint, docs, and straightforward implementation should move down when practical.
- **Keep context isolated** — broad repository exploration should happen in subagent contexts whenever useful.
- **No delegation chains** — the root GPT-6 agent owns decomposition and final acceptance.
- **No unnecessary spawning** — tiny tasks can still be done directly.
- **Version-aware setup** — let an AI adapt the configuration to the installed Codex version instead of relying on brittle copy-paste config.

## What is in this repository

```text
README.md                           project overview
SETUP_WITH_AI.md                    standalone AI-readable installer guide
config/gpt6.config.toml             example configuration template
instructions/gpt6-delegation.md     single source of truth for behavior
LICENSE                             MIT license
CONTRIBUTING.md                     contribution guide
```

The authoritative behavior policy is [`instructions/gpt6-delegation.md`](./instructions/gpt6-delegation.md).

`config/gpt6.config.toml` is intentionally only a template. Codex configuration capabilities can change, so the setup agent should choose the simplest supported mechanism available on the user's machine.

## What this project is not

This is not a full orchestration framework.

There are larger projects that provide workflow engines, verification stages, many routing modes, installers, and broader agent topologies.

This project deliberately solves one narrow problem:

> **Stop spending GPT-6 on work that does not need GPT-6.**

Minimal policy. Minimal setup. Easy to remove.

## License

MIT. See [`LICENSE`](./LICENSE).
