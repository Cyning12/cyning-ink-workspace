# Harness invoke snapshot

| 字段 | 值 |
|------|-----|
| hat_id | 10 |
| template | docs/tech_graph/prompts/PROMPT-filled-requirements-tech-graph-phase1-v1.md §A（已填需求帽 · tech_graph 方案1） |
| task_paths | `ai-ink-brain-api-python/docs/tasks/active/task_engineering_tech_graph_graph_json_export_v1.md` · `ai-ink-brain/content/tasks/active/task_engineering_tech_graph_graph_json_export_v1.md` |
| related_review_or_none | 无 |
| created_utc_or_local | 2026-05-14（会话锚点） |
| notes | 用户通过 @ 引用专题已填 Prompt；执行 Agent 按 §A 输出双仓 task 初稿与下一棒 Prompt |

## 可复制 Prompt 快照（与发起体一致）

```text
你正在扮演工作区 Harness「需求与任务分析帽」，严格遵循：
- docs/harness/prompts/10-requirements.md（身份、只做什么、禁止什么、输出形状、停止条件、交接物）
- docs/harness/HARNESS_V2_PLAN.md 第 5 节（test_strategy、failure_paths、freeze_id 等）

输入（占位符已全部替换；若你仍看到 {{…}} 字样，须先追问用户，不得开工）：

【目标与上下文】
根据工作区规划，为 **方案1（静态 graph.json 导出 + CI 门禁）** 分别起草 **两条** 可落盘的 **子仓正式 task 初稿**（Markdown 正文块，不要写业务实现代码）：
1. **后端**：`ai-ink-brain-api-python` — 脚本落点、`pytest` 或 CI 步骤、`--check` 与 `git diff` 语义、与现有 `tools/tech_graph_contract_check.py` / `_contract_manifest.json` **并行**关系写清。
2. **前端**：`ai-ink-brain` — 图谱真值目录 **`docs/_tech_graph/`**（R1：当前聚合仓复检为仓根已无 `_tech_graph/`，若你检出不同则先单列 **迁移** task 再写导出）；导出脚本若复用后端脚本需在 task 中写 **cwd** 与 checkout/调用方式。

每条 task 初稿须显式包含：**背景与目标**、**范围 / 非范围**、**依赖链接**（相对 `Projects/`）、**验收标准**（可勾选或可命令断言）、**failure_paths**（触发 → HTTP/退出码/日志 → 可重试 → 用户可见类型）、**建议 test_strategy**（方案1 核心解析与 CI 建议 `required` 并附理由）、**freeze_id 建议**（锚定 `docs/tech_graph/改进方向.md` v1.1 + 对应 SPEC 路径）、**闸口 A** 交付说明（方案1 完成后须有何种对比实验文档的最低结构）、**给执行帽的必读列表**。

若发现规划与某子仓 `AGENTS.md` / 现网目录矛盾：**单独列「矛盾」小节**，不做调和叙事。

【已有材料路径】
docs/tech_graph/改进方向.md
docs/tech_graph/SPEC/README.md
docs/tech_graph/SPEC/json_graph/scheme_1_graph_json.md
docs/tech_graph/tasks/README.md
AGENTS.md

【是否按任务审核文档回填】
无

你必须完成：
0. **Invoke 快照（开帽起点）**：在输出下列第 1 条起的实质性结果之前，先将 **本用户消息全文** 按 `docs/tech_graph/invokes/README.md` 落盘到 `Projects/docs/tech_graph/invokes/`（含元数据表 + 快照 fenced code）。同一会话内追问不再新增快照文件。
1. 输出两条 task 的结构化初稿（前端一条、后端一条），每条约含：建议文件名、元信息表草案、各 Harness 字段。
2. 在文末给出 **建议落盘路径**：后端 `ai-ink-brain-api-python/docs/tasks/active/`；前端 `ai-ink-brain/content/tasks/active/`（与各自 README 一致）。
3. 文末再给一段 **下一棒可复制 Prompt**（执行帽或帽 20 复审），含本 invoke 快照路径占位，便于打回闭环。
4. 禁止：写业务实现代码；改 CI YAML 正文；在 task 中写绝对本机路径。

不强制你直接写文件；若用户随后明确要求落盘，再按第 2 步路径编辑。
```
