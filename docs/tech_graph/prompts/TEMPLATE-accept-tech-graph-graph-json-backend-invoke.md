# Invoke 模板 — 验收帽：后端 graph.json / scheme1 任务关闭

> **用途**：复制下方 **「整段可复制正文」** 到新对话的 **user**，发起 **任务关闭验收**（假定未参与实现）。调用前须替换 `{{PR_URL}}` 等占位符；若占位符未替换，验收帽须先追问，不得签发结论。  
> **行为对齐**：[`docs/harness/prompts/50-independent-reinspect.md`](../../harness/prompts/50-independent-reinspect.md) 第二节「全局验收」；**不**替代维护者签字。  
> **落盘位置**：本文件在 **`docs/tech_graph/prompts/`**（专题内）；**勿**复制到 `docs/harness/prompts/`。

---

## 调用前自检（人类）

- [ ] `{{PR_URL}}`、`{{TARGET_BRANCH}}` 已替换为真实值。  
- [ ] `{{MERGE_COMMIT_OR_RUN_ID}}` 已替换或整段删除（可选）。  
- [ ] 子仓 task 路径仍为：`ai-ink-brain-api-python/docs/tasks/active/task_engineering_tech_graph_graph_json_export_v1.md`。

---

## 整段可复制正文（从「你正在扮演」起粘贴到对话 user）

```text
你正在扮演 **任务关闭验收** 角色：假定未参与实现。目标是对 **子仓 ai-ink-brain-api-python** 的 task「技术图谱 — 方案1 静态 graph.json 导出与 CI 门禁」做 **书面签收**，决定是否可将 task **标为完成并归档**（归档路径以该仓 `docs/tasks/` 惯例为准，不写死）。

## 冻结与对齐

- 核对 task 内 **freeze_id** 与前端同源 task **必须为同一行**：`TECH_GRAPH_S1_FREEZE_20260514_V1_1_3`（**勿**把 commit hash 写进该行）。
- 关联规划 / SPEC（工作区相对路径，供抽查）：`docs/tech_graph/改进方向.md` v1.1.3；`docs/tech_graph/SPEC/json_graph/scheme_1_graph_json.md`。

## 必读真值（后端仓内）

- Task 全文：`ai-ink-brain-api-python/docs/tasks/active/task_engineering_tech_graph_graph_json_export_v1.md`（重点 §4 验收、§5 failure_paths、§8 实现备忘）。
- 实现备忘应已填：**导出脚本** `tools/tech_graph_graph_export.py`、**pytest** `tests/test_tech_graph_graph_export.py`、**CI** `.github/workflows/tech-graph.yml`（job 名仍为 `manifest_check`，内顺序为 `tech_graph_manifest_check.py` 再 `tech_graph_graph_export.py --check`）、**闸口 A** `docs/tech_graph/gate_a_scheme1_backend.md`。

## 证据来源（优先顺序）

1. 合并 PR 的 CI 全绿记录：`pytest`、`verify-fast`、`tech-graph`（含 graph drift step）、`tech-graph-contract`；可选 Vercel。  
   - PR：{{PR_URL}}  
   - 目标分支：{{TARGET_BRANCH}}  
   - 可选留痕：{{MERGE_COMMIT_OR_RUN_ID}}
2. PR 描述或评论是否写明 **contract 与 graph** 两条命令及建议顺序（与 task §4 最后一条一致）。
3. 目标分支上是否已提交：`docs/_tech_graph/graph.json`、上述脚本与单测、闸口 A 文档。

## 验收表（逐项 **pass / fail**，并写 **证据**：PR、workflow 名、路径或日志片段）

| 编号 | 验收项（对照 task §4 / §5 / §6 / §8） | pass/fail | 证据 |
| --- | --- | --- | --- |
| A1 | 本仓根可执行 `python tools/tech_graph_graph_export.py`，产出/更新 `docs/_tech_graph/graph.json` | | |
| A2 | `python tools/tech_graph_graph_export.py --check`：一致则退出码 0；漂移则非 0 且 stderr 有差异类型/摘要（FP-2） | | |
| A3 | pytest 覆盖解析失败、空图、golden（`tests/test_tech_graph_graph_export.py`） | | |
| A4 | `python tools/tech_graph_contract_check.py` 在 CI 中仍通过（与 graph **并行**、**未合并**脚本） | | |
| A5 | PR 说明含 **contract 与 graph** 命令及顺序 | | |
| B1 | task §5 **FP-1～FP-4** 与实现/文档一致（脚本头部或 PR 已说明退出码语义即可） | | |
| B2 | §6 **闸口 A**：`docs/tech_graph/gate_a_scheme1_backend.md` 已存在且结构齐全；结论段若仍为占位，须标明「可关任务 / 须后补结论」**二选一**及理由 | | |
| B3 | §8 **实现备忘** 与仓库实际路径一致 | | |

## 输出形状（须交付）

1. 上表填满 **pass/fail + 证据**。  
2. **汇总**：是否存在 **阻塞关闭** 项；若无，明示一句 **「建议关闭本 task」** 或 **「关闭任务、闸口结论后补」**（二选一须写明理由）。  
3. **维护者动作清单**（短列表）：如将 task **状态**由 `draft` 改为约定终态、勾选 §4 `- [ ]`、按该仓 README 归档至 `done/` 等。

## 禁止

- 证据不足时不得签发「已验收」；不替执行者改代码。  
- 不把 **commit hash** 写入 task 的 **freeze_id 那一行**。
```

---

## 修订记录

| 日期 | 摘要 |
| --- | --- |
| 2026-05-14 | v1：格式化落盘；与 `PROMPT-filled-*` 目录体例对齐 |

---

## 给 Cursor

`TEMPLATE`、`验收`、`graph.json`、`freeze_id`、`tech_graph`、`prompts`、`50-independent-reinspect`
