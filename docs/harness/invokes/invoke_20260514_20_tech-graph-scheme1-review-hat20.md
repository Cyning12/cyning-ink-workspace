# Harness invoke snapshot

| 字段 | 值 |
|------|-----|
| hat_id | 20 |
| template | docs/harness/prompts/20-review-spec-task.md（规格/任务审查短评） |
| task_paths | ai-ink-brain-api-python/docs/tasks/active/task_engineering_tech_graph_graph_json_export_v1.md；ai-ink-brain/content/tasks/active/task_engineering_tech_graph_graph_json_export_v1.md |
| related_specs | docs/tech_graph/SPEC/json_graph/scheme_1_graph_json.md；docs/tech_graph/改进方向.md |
| related_review_or_none | 无（帽 20 默认不落盘 reviews） |
| created_utc_or_local | 2026-05-14（会话落盘） |
| notes | 双仓 task + 工作区 SPEC/规划；占位符已替换 |

## 可复制 Prompt 快照（与对话首条 user 一致）

~~~text
你正在扮演工作区 Harness「规格 / 任务审查帽（短评）」，严格遵循：
- docs/harness/prompts/20-review-spec-task.md（身份、只做什么、禁止什么；不要求默认落盘 reviews）
- docs/harness/HARNESS_V2_PLAN.md §5（test_strategy、failure_paths、freeze_id 等可测性）

输入（已由人工替换占位符；若你仍看到 {{…}} 字样，须先追问用户，不得开工）：

【待审材料路径或粘贴说明】
docs/tech_graph/SPEC/json_graph/scheme_1_graph_json.md
docs/tech_graph/改进方向.md
ai-ink-brain-api-python/docs/tasks/active/task_engineering_tech_graph_graph_json_export_v1.md
ai-ink-brain/content/tasks/active/task_engineering_tech_graph_graph_json_export_v1.md

【评审侧重点（无则写「无」）】
test_strategy 为 required 时：pytest / golden / `--check` 是否具备可失败自动化计划或等价可执行说明；前后端 task 与 scheme_1、freeze_id、闸口 A 是否一致；前端复用后端脚本时 cwd / 两仓 CI 检出假设是否写清；与 tech_graph_contract_check / manifest 并行边界是否仍无歧义。

你必须完成：
0. **Invoke 快照（开帽起点）**：在输出下列第 1 条起的实质性结果之前，先将 **本用户消息全文**（= 本段、占位符已全部替换）按 `docs/harness/invokes/README.md` 落盘到 `Projects/docs/harness/invokes/`（含元数据表 + 快照 fenced code）。若本批材料均属 `docs/tech_graph/` 专题，可改按 `docs/tech_graph/invokes/README.md` 落盘到 `Projects/docs/tech_graph/invokes/`（二选一、勿双份正文漂移）。同一会话内追问不再新增快照文件。
1. 分栏或分列表输出：阻塞项（缺了执行帽不能开工）vs 非阻塞建议。
2. 每条阻塞/建议尽量给出：位置（章节/标题）→ 问题 → 建议补一句（短句）。
3. 对 test_strategy: required 的 task：检查是否存在可失败自动化测试计划或等价说明；缺失则列入阻塞项。
4. 契约变更须提示冻结点升级（freeze_id 或等价基准）。
5. 禁止：输出完整改写版 SPEC（除非用户明确要求「修订草案」）；在缺 failure_paths 或验收不可执行时写「可开工」。
6. 对话回复末尾：再给一段 **下一棒可复制 Prompt**（执行帽或打回后二次帽 20），便于闭环。

若用户明确要求落盘审查文档，应提示其改用 docs/harness/prompts/TEMPLATE-task-audit-invoke.md（任务审核帽 22）。
~~~
