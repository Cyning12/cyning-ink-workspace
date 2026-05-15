# Harness invoke snapshot

| 字段 | 值 |
|------|-----|
| hat_id | 10（执行帽 / 文档收敛） |
| template | 用户结构化指令（Harness 执行帽）；链上一节帽 20 |
| task_paths | `ai-ink-brain-api-python/docs/tasks/active/task_engineering_tech_graph_graph_json_export_v1.md`；`ai-ink-brain/content/tasks/done/task_engineering_tech_graph_graph_json_export_v1.md` |
| related_specs | `docs/tech_graph/SPEC/json_graph/scheme_1_graph_json.md`；`docs/tech_graph/改进方向.md` |
| prev_invoke | `docs/harness/invokes/invoke_20260514_20_tech-graph-scheme1-review-hat20.md` |
| related_review_or_none | 无 |
| created_utc_or_local | 2026-05-15 |
| notes | scheme_1 / 改进方向 / 双仓 task 对齐；`freeze_id` 机械一致；contract 与 graph 并行不合并 |

> **路径勘误（2026-05-15）**：前端 `task_engineering_tech_graph_graph_json_export_v1.md` 已归档至 **`ai-ink-brain/content/tasks/done/`**；本文件元数据 `task_paths` 与 fenced 快照内原 `active/` 路径已替换为 `done/`，避免断链。

## 可复制 Prompt 快照（与对话首条 user 一致）

```text
【角色】工作区 Harness 执行帽（或承担文档收敛的需求帽）

【硬约束】
- 已存在帽 20 短评结论：须先消除 docs/tech_graph/SPEC/json_graph/scheme_1_graph_json.md「仍待执行方补全」与 docs/tech_graph/改进方向.md v1.1.1（R1）及 ai-ink-brain/content/tasks/done/task_engineering_tech_graph_graph_json_export_v1.md 之间关于「前端 graph.json CI 是否必绿」的矛盾；并在两子仓 task 写入单行 freeze_id。
- 遵守两子仓 task 的 failure_paths、与 tech_graph_contract_check / _contract_manifest 并行不合并。
- Invoke 快照（本段开帽若为新节）：按 docs/harness/invokes/README.md 落盘；可链上一节：docs/harness/invokes/invoke_20260514_20_tech-graph-scheme1-review-hat20.md

【输入】
- docs/harness/invokes/invoke_20260514_20_tech-graph-scheme1-review-hat20.md（帽 20 调用体）
- ai-ink-brain-api-python/docs/tasks/active/task_engineering_tech_graph_graph_json_export_v1.md
- ai-ink-brain/content/tasks/done/task_engineering_tech_graph_graph_json_export_v1.md
- docs/tech_graph/SPEC/json_graph/scheme_1_graph_json.md
- docs/tech_graph/改进方向.md

【交付】
- 文档收敛：scheme_1 + 两 task 一致；freeze_id 可机械比对。
- 或：若文档已齐，按后端 task §4 先 pytest/red 再实现导出脚本与 CI；前端按 §7 写清 cwd 与单仓/聚合 CI 二选一。
```
