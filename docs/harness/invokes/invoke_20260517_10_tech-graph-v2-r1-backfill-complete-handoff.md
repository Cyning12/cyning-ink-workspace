# Harness invoke snapshot

| 字段 | 值 |
|------|-----|
| hat_id | 10 |
| template | 需求与任务分析帽 · 交接确认（`docs/harness/prompts/10-requirements.md`） |
| task_paths | `ai-ink-brain-api-python/docs/tasks/active/task_engineering_tech_graph_v2_graph_query_v1.md` |
| task_version | **v0.2** · 按审查 R1 回填 |
| created | 2026-05-17 |
| next_hat | **22** 任务审核 R2 → 通过后 **执行帽** P2-0 |

## 10 帽确认摘要（已落盘，供下一棒只读）

| R1 要求 | task v0.2 落点 |
| --- | --- |
| P2-0 最小集 / P2-4 延后 | §2.1 A 两表；`graphs[]`/`ref` 仅 P2-4 |
| graph.json 升版默认 | §2.1 A「落盘策略（默认）」 |
| 产品抉择 | G-END-6 + 治理层应用文 §8.2～8.3 |
| 长期记忆非范围 | §2.2 |
| 论文禁止外推 | §7 |

## 可复制 Prompt（交给 R2 任务审核帽）

见 **`invoke_20260517_22_tech-graph-v2-task-audit-r2.md`** 全文 fenced 块（路径相对工作区根 `Projects/`）。

## 10 帽停止条件

- task 正文已更新至 v0.2；**不**再重复需求分析。  
- **下一棒 = 22 R2 审核**，非 10 帽二次回填（除非 R2 打回）。
