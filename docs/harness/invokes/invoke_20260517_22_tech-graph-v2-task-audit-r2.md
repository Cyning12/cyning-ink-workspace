# Harness invoke snapshot

| 字段 | 值 |
|------|-----|
| hat_id | 22 |
| template | 任务审核帽（`docs/harness/prompts/22-task-audit.md`） |
| task_paths | `ai-ink-brain-api-python/docs/tasks/active/task_engineering_tech_graph_v2_graph_query_v1.md` |
| prev_review | `ai-ink-brain-api-python/docs/harness/reviews/task_engineering_tech_graph_v2_graph_query_v1_audit_R1_20260517.md` |
| requirements_backfill | v0.2 · 2026-05-17（10 帽 / 需求回填已完成） |
| created | 2026-05-17 |
| notes | R2：验证 R1 回填清单是否落盘；通过后建议执行帽从 P2-0 开工 |

## 可复制 Prompt 快照（交给任务审核帽 · R2）

```text
你正在扮演工作区 Harness「任务审核帽」，严格遵循：
- docs/harness/prompts/22-task-audit.md
- docs/harness/HARNESS_V2_PLAN.md §5

【审核对象】
ai-ink-brain-api-python/docs/tasks/active/task_engineering_tech_graph_v2_graph_query_v1.md
（task 元信息标注：v0.2 · 按审查 R1 回填 · 待 R2）

【上一轮审查】
ai-ink-brain-api-python/docs/harness/reviews/task_engineering_tech_graph_v2_graph_query_v1_audit_R1_20260517.md

【对照材料】
docs/diary/jsonPKmermaid/治理层三相塌缩_Ink技术图谱应用.md（§8.2 产品抉择、§8.3 JSON 替 ai.md、§8A 长期记忆）
docs/tech_graph/spec/ai-ink-brain-api-python/machine_track_architecture_draft_zh.md
docs/diary/jsonPKmermaid/reports/conclusion_gate_ctx_ab_final_zh.md

【R1 回填清单 — 须逐项勾选是否已在 task 正文满足】
1. §2.1：P2-0 最小集 vs P2-4 延后两表；P2-0 禁止 graphs[]、edges[].ref
2. §2.1：默认落盘 = 同路径 graph.json + schema_version graph_v2
3. §6：P2-0 交付物与最小 v2 一致；P2-4 含 graphs[]/ref/manifest 互引
4. G-END-6 / 治理层应用文链接；与闸口 A「不默认 v1 整包」一致
5. 非范围：跨会话长期记忆单独立项
6. §7：禁止外推论文 SBM ARI=1 到 Ink

【输出要求】
- 落盘：ai-ink-brain-api-python/docs/harness/reviews/task_engineering_tech_graph_v2_graph_query_v1_audit_R2_YYYYMMDD.md
- 结论：是否建议执行帽从 P2-0 开工；残留非阻塞项列表
- 若仍阻塞：标明 ID 与 task 应改章节

【禁止】
- 写业务实现代码；改 CI；扩 scope 到 Neo4j / 退役 .ai.md
```

## 给下一棒（审核通过后）

**执行帽** · 从 task **§6 P2-0** 开工：`graph_v2` 最小 schema + `tech_graph_graph_equivalence_check.py` 草案。
