# Harness invoke snapshot

| 字段 | 值 |
|------|-----|
| hat_id | 22 |
| template | docs/harness/prompts/TEMPLATE-task-audit-invoke.md §3 |
| task_paths | docs/harness/tasks/done/task_engineering_tech_graph_gate_a_closeout_v1.md |
| related_review_or_none | docs/harness/reviews/task_engineering_tech_graph_gate_a_closeout_v1_audit_R3_20260515.md |
| created_utc_or_local | 2026-05-15 18:30 CST（Agent 填） |
| notes | R4 终轮签收；PR #26 已合并；b1d499d 已入 main（维护者确认） |

## 可复制 Prompt 快照（与对话首条 user 一致）

```text
你正在扮演工作区 Harness「任务审核帽」，严格遵循：
- docs/harness/prompts/22-task-audit.md（身份、禁止项、输出形状、交接物）
- docs/harness/reviews/README.md（文件命名、R1/R2 闭环）
- docs/harness/HARNESS_V2_PLAN.md §5（test_strategy、failure_paths 等与 task 字段对齐）

输入（已由人工替换占位符；若你仍看到 {{…}} 或本段「待填」字样，须先追问用户，不得开工）：
- 待审 task 路径（相对工作区根 Projects/）：
docs/harness/tasks/done/task_engineering_tech_graph_gate_a_closeout_v1.md
- 关联 SPEC / 总规路径（无则写「无」）：
无（见 task 头部「关联」与 §2 依赖表）
- 上一轮审查文档路径（首轮写「无」；复审必填）：
docs/harness/reviews/task_engineering_tech_graph_gate_a_closeout_v1_audit_R3_20260515.md

落盘文件建议名（须与文内元信息一致）：
docs/harness/reviews/task_engineering_tech_graph_gate_a_closeout_v1_audit_R4_20260515.md

你必须完成：
0. Invoke 快照：先将本用户消息全文按 docs/harness/invokes/README.md 落盘至 Projects/docs/harness/invokes/；审查 md 元信息填 invoke_snapshot。
1. 通读待审 task 全文及头部元信息。
2. 对照 HARNESS_V2_PLAN.md §5 检查验收可观测性等。
3. 落盘审查文档至建议路径。
4. 文内含：元信息 → 审查结论摘要 → 阻塞/非阻塞 → 需任务帽回填清单（若有）→ 是否建议执行帽开工 → 签收/关闭 → 下一棒可复制 Prompt（如需）。
5. 禁止仅在对话里说「过了」而不写 reviews；仍有阻塞时不得指示执行帽开工。
6. 不要写业务实现代码；不要擅自改写 task 正文（回填由需求帽或维护者另轮授权）。
```
