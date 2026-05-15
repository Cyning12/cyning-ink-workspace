# Harness invoke snapshot

| 字段 | 值 |
|------|-----|
| hat_id | 10 |
| template | 需求与任务分析帽（`docs/harness/prompts/10-requirements.md` + 用户给定 Harness 调用体） |
| task_paths | `ai-ink-brain-api-python/docs/tasks/active/task_engineering_tech_graph_gate_a_perf_compare_v1.md` |
| related_review_or_none | 无 |
| created_utc_or_local | 2026-05-15 CST |
| notes | 闸口 A 后端性能对比单；固定 `freeze_id`；§3.2 浏览器默认 N/A；书面证据与父文档结论/§6 对齐 |

## 可复制 Prompt 快照（与对话首条 user 一致）

```text
你正在扮演工作区 Harness「需求与任务分析帽」，严格遵循：
- docs/harness/prompts/10-requirements.md（身份、只做什么、禁止什么、输出形状、停止条件、交接物）
- docs/harness/HARNESS_V2_PLAN.md §5（与 task 字段对齐时可引用）

输入（已由人工替换占位符；若你仍看到 {{…}} 字样，须先追问用户，不得开工）：

【目标与上下文】
围绕闸口 A 后端性能对比单：在固定 freeze_id 与 §3.2 浏览器默认 N/A 的前提下，核对「书面证据 + 父文档 gate_a_scheme1_backend.md 结论与 §6」是否还可收紧验收、补充 failure_paths 或披露文档张力；产出可交给执行帽/审核帽的结构化缺口清单或 task 段落补丁建议。不写业务代码、不改 CI。

【已有材料路径或粘贴说明】
ai-ink-brain-api-python/docs/tasks/active/task_engineering_tech_graph_gate_a_perf_compare_v1.md
ai-ink-brain-api-python/docs/tech_graph/gate_a_scheme1_backend.md
docs/tech_graph/改进方向.md
docs/tech_graph/SPEC/json_graph/scheme_1_graph_json.md

【是否按任务审核文档回填】（无则写「无」；有则写相对路径）
无

你必须完成：
0. **Invoke 快照（开帽起点）**：在输出下列第 1 条起的实质性结果之前，先将 **本用户消息全文**（= 本模板 §3、占位符已全部替换）按 `docs/harness/invokes/README.md` 落盘到 `Projects/docs/harness/invokes/`（含元数据表 + 快照 fenced code）。同一会话内追问 **不** 再新增快照文件。
1. 输出结构化块：背景 / 范围 / 非范围 / 依赖链接 / 验收列表 / failure_paths / 给执行帽的必读列表；矛盾单独小节（若有）。
2. 注明建议 test_strategy（required | recommended | not_applicable）及 test_strategy_note（若 not_applicable 须附理由）。
3. 若 AUDIT 路径非「无」：按该审查文档的回填清单逐条映射到 task 小节建议，并在建议文末注明「按审查 R<n> 回填」应指向的文件名。
4. 禁止：写业务实现代码；改 CI；在 task 中写绝对本机路径；把未在依赖中声明的契约当真值。
5. 对话回复：生成可以完整复制的 Prompt，用于直接交给下一棒执行；须兼顾打回、二次审查等情形，下一棒也可能是上一棒（由其修复问题）。

不强制落盘；若用户要求写入某 task 文件，须由用户明确路径后再编辑（本模板不预置写文件占位符）。
```
