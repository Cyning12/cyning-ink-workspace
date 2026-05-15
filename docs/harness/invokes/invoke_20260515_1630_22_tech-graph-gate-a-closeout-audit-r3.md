# Harness invoke snapshot

| 字段 | 值 |
|------|-----|
| hat_id | 22 |
| template | 用户粘贴的任务审核帽调用体（对齐 `docs/harness/prompts/TEMPLATE-task-audit-invoke.md` §3 形态 + R3 硬条件附录） |
| task_paths | docs/harness/tasks/active/task_engineering_tech_graph_gate_a_closeout_v1.md |
| related_review_or_none | docs/harness/reviews/task_engineering_tech_graph_gate_a_closeout_v1_audit_R2_20260515.md |
| created_utc_or_local | 2026-05-15（审查开帽） |
| notes | PR Cyning12/ai-ink-brain-api-python #26；R3 预审硬条件 |

## 可复制 Prompt 快照（与对话首条 user 一致）

```text
你正在扮演工作区 Harness「任务审核帽」，严格遵循：
- docs/harness/prompts/22-task-audit.md（身份、禁止项、输出形状、交接物）
- docs/harness/reviews/README.md（文件命名、R1/R2/R3 闭环）
- docs/harness/HARNESS_V2_PLAN.md §5（test_strategy、failure_paths 等与 task 字段对齐）

输入（已由人工替换占位符；若你仍看到 {{…}} 或「待填」字样，须先追问用户，不得开工）：
- 待审 task 路径（相对工作区根 Projects/）：
docs/harness/tasks/active/task_engineering_tech_graph_gate_a_closeout_v1.md
- 关联 SPEC / 总规路径（无则写「无」）：
ai-ink-brain-api-python/docs/tech_graph/gate_a_scheme1_backend.md
docs/tech_graph/改进方向.md
- 上一轮审查文档路径（首轮写「无」；复审必填）：
docs/harness/reviews/task_engineering_tech_graph_gate_a_closeout_v1_audit_R2_20260515.md

落盘文件建议名（须与文内元信息一致；若与用户输入冲突以用户为准并追问）：
docs/harness/reviews/task_engineering_tech_graph_gate_a_closeout_v1_audit_R3_20260515.md

你必须完成：
0. **Invoke 快照（开帽起点）**：在输出下列第 1 条起的实质性结果之前，先将 **本用户消息全文**（= 本模板 §3、占位符已全部替换）按 `docs/harness/invokes/README.md` 落盘到 `Projects/docs/harness/invokes/`（含元数据表 + 快照 fenced code）。你在步骤 3 落盘审查 md 时，须在文首元信息表增加 **`invoke_snapshot`** 指向该 invoke 文件（相对 `Projects/`）。同一会话内追问 **不** 再新增快照文件。
1. 通读待审 task 全文及头部元信息（状态、freeze_id、gates_before_code、test_strategy、failure_paths、验收、必读链接）。
2. 对照 HARNESS_V2_PLAN.md §5 检查验收可观测性、required 与可失败自动化测试说明。
3. 落盘一篇审查文档至 **上表路径**（与 `reviews/README.md`、`22-task-audit.md` 子仓规则一致）。
4. 文内结构：元信息 → 审查结论摘要 → 阻塞 / 非阻塞 → 需任务帽回填清单（若有）→ 是否建议执行帽开工 → 「签收 / 关闭」仅在终轮或明确不可关闭时写死 → **「下一棒可复制 Prompt」**（`text` 代码围栏，内为已替换占位符的下一棒 §3 全文；与 `22-task-audit.md` **交接物**（1）（2）逐字一致）。
5. 禁止仅在对话里说「过了」而不写 reviews；禁止在仍有阻塞时指示执行帽开工。
6. 不要写业务实现代码；不要擅自改写 task 正文。
7. **对话与归档**：① **对话回复** 中输出与步骤 4 审查 md 末节 **完全相同** 的下一棒可复制 Prompt 全文；② **禁止**仅用「见落盘审查」等语省略对话中的 Prompt 正文。

【R3 预审给审核帽的硬条件（由 R2 写入）】
- 维护者已在 GitHub **PR #26**（`Cyning12/ai-ink-brain-api-python`）**描述**中追加 **`.github/workflows/pytest.yml` / workflow `pytest`** 对应 **Actions run URL（含 run id）**；若 PR 已合并，请在该 run 对应 **merge commit** 或 **默认分支最新 pytest run** 上核对 id 与描述一致。
- 若 PR 已合并：核对主 task 头部 **状态** 是否与团队 **done** 约定一致后再声明 **可关闭**。
```
