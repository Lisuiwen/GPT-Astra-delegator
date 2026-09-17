---
name: gpt6-delegation
description: GPT-6 Astra orchestrator delegation policy. Use only when GPT-6 is the primary agent in the gpt6 profile; delegate routine work to Luna/Terra/Sol subagents.
disable-model-invocation: true
---

# GPT-6 委派策略

本 Skill 仅在 `codex --profile gpt6` / `codex-gpt6` 下通过 profile 显式启用。普通 `codex`（Sol）不会加载。

完整规则见 `~/.codex-LSW/instructions/gpt6-delegation.md`。核心要点：

## 你（GPT-6）保留

- 架构与 trade-off 决策
- 需求歧义澄清
- 疑难调试、跨模块/跨系统推理
- 最终 review 与验收

## 积极委派

| 任务 | 子代理 |
| --- | --- |
| 搜代码、查引用、摸调用链 | `luna_scout` / `explorer` / Luna |
| 机械性批量修改 | `terra_worker` / `worker` / Terra |
| 规格明确的普通实现 | `sol_implementer` / Sol |
| 按固定 spec 写测试 | Terra |
| 格式化 / 文档 / lint | Luna 或 Terra |

## 约束

- 独立子任务并行 spawn
- 子代理只回传摘要，不堆原始日志
- 禁止无意义的嵌套委派
- 简单机械活不要占用 GPT-6
