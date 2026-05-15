# Invoke 模板 — 验收帽：前端 graph.json / scheme1 任务关闭

> **用途**：复制下方 **「整段可复制正文」** 到新对话的 **user**，发起 **任务关闭验收**（假定未参与实现）。调用前须替换 `{{PR_URL}}` 等占位符；若占位符未替换，验收帽须先追问，不得签发结论。  
> **行为对齐**：[`docs/harness/prompts/50-independent-reinspect.md`](../../harness/prompts/50-independent-reinspect.md) 第二节「全局验收」；**不**替代维护者签字。  
> **落盘位置**：本文件在 **`docs/tech_graph/prompts/`**（专题内）；**勿**复制到 `docs/harness/prompts/`。

---

## 调用前自检（人类）

- [ ] `{{PR_URL}}`、`{{TARGET_BRANCH}}` 已替换为真实值。  
- [ ] `{{MERGE_COMMIT_OR_RUN_ID}}` 已替换或整段删除（可选）。  
- [ ] 子仓 task 路径仍为：`ai-ink-brain/content/tasks/done/task_engineering_tech_graph_graph_json_export_v1.md`。

---

## 整段可复制正文（从「你正在扮演」起粘贴到对话 user）

```text
你正在扮演 **任务关闭验收** 角色：假定未参与实现。目标是对 **子仓 ai-ink-brain** 的 task「技术图谱 — 方案1 静态 graph.json 导出与 CI 门禁」做 **书面签收**，决定是否可将 task **标为完成并归档**（归档路径以该仓 `content/tasks/` 惯例为准，不写死）。

## 冻结与对齐

- 核对 task 内 **freeze_id** 与后端同源 task **必须为同一行**：`TECH_GRAPH_S1_FREEZE_20260514_V1_1_3`（**勿**把 commit hash 写进该行）。
- 关联规划 / SPEC（工作区相对路径，供抽查）：`docs/tech_graph/改进方向.md` v1.1.3；`docs/tech_graph/SPEC/json_graph/scheme_1_graph_json.md`。

## 必读真值（前端仓内）

- Task 全文：`ai-ink-brain/content/tasks/done/task_engineering_tech_graph_graph_json_export_v1.md`（重点 §4 验收、§5 failure_paths、§9 实现备忘）。
- 实现备忘应已填：**脚本** `tools/export_graph_json.py`；**CI** `.github/workflows/quality.yml`（job `lint-and-build`：`pnpm install` 之后、`pnpm lint` 之前含 `actions/setup-python@v5` 与 `python3 tools/export_graph_json.py --input docs/_tech_graph --output docs/_tech_graph/graph.json --check`；**cwd** = 仓根）；**一键检查** `pnpm tech-graph:graph-check`；**闸口 A** 指针见 task §9（规划「对比实验门闸」节或独立 md，以备忘为准）。
- **非范围（勿按后端验收）**：本仓 **不**验收 `_contract_manifest` / `tech_graph_contract_check`（task 已声明）。

## 证据来源（优先顺序）

1. 合并 PR 的 CI 全绿记录：**`quality`**（含 **Tech graph graph.json (--check)**、`pnpm lint`、`pnpm test`、`pnpm build`）。  
   - PR：{{PR_URL}}  
   - 目标分支：{{TARGET_BRANCH}}  
   - 可选留痕：{{MERGE_COMMIT_OR_RUN_ID}}
2. 目标分支上是否已提交：`docs/_tech_graph/graph.json`、`tools/export_graph_json.py`、对 `quality.yml` / `package.json` 的接入与 task §9 一致。

## 验收表（逐项 **pass / fail**，并写 **证据**：PR、workflow 名、路径或日志片段）

| 编号 | 验收项（对照 task §4 / §5 / §9） | pass/fail | 证据 |
| --- | --- | --- | --- |
| A1 | `docs/_tech_graph/graph.json` 已提交且与解析器语义一致（可由 CI `--check` 绿推断） | | |
| A2 | `quality` 中 **graph** 步在 **install 后、lint 前**，且命令为 `python3 tools/export_graph_json.py --input docs/_tech_graph --output docs/_tech_graph/graph.json --check`（cwd 为仓根；Python 3.11） | | |
| A3 | `pnpm lint` / `pnpm test` / `pnpm build` 与 graph 步同 PR 必绿 | | |
| A4 | `test_strategy=required`：备忘已写明 **CI 必跑 `--check`** 为真（未另加 Vitest 的理由成立） | | |
| B1 | §5 **FP-1～FP-3** 与脚本/CI 行为一致；本实现若选 **(A) 仅前端 checkout**，FP-3 须标明「不适用 / 文档化」及理由 | | |
| B2 | §6 **闸口 A**：备忘指针或独立文档是否满足「可关任务 / 须后补」**二选一**及理由 | | |
| B3 | §9 **实现备忘** 与仓库实际路径、脚本名、Python 版本一致 | | |

## 输出形状（须交付）

1. 上表填满 **pass/fail + 证据**。  
2. **汇总**：是否存在 **阻塞关闭** 项；若无，明示一句 **「建议关闭本 task」** 或 **「关闭任务、闸口结论后补」**（二选一须写明理由）。  
3. **维护者动作清单**（短列表）：如将 task **状态**由 `draft` 改为约定终态、按需勾选 §4、按 `content/tasks/README.md` 归档至 `done/` 等。

## 禁止

- 证据不足时不得签发「已验收」；不替执行者改代码。  
- 不把 **commit hash** 写入 task 的 **freeze_id 那一行**。  
- 不把 **契约 manifest 门禁** 当作本前端 task 的验收项。
```

---

## 修订记录

| 日期 | 摘要 |
| --- | --- |
| 2026-05-14 | v1：前端 scheme1 验收帽模板落盘；与后端 TEMPLATE 对称 |

---

## 给 Cursor

`TEMPLATE`、`验收`、`graph.json`、`freeze_id`、`tech_graph`、`prompts`、`50-independent-reinspect`、`ai-ink-brain`、`quality`
