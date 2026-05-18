# docs/harness/reviews（任务审核产出）

> **用途**：存放 **任务审核帽** 的**书面审查结果**（每轮必产出）；与 `prompts/22-task-audit.md` 配套。  
> **真值**：单条 task 是否可关闭，以 **审查文档「签收 / 关闭」** 节为准，并与 task 头部 `状态` 一致；**不得以聊天结论替代落盘**。  
> **子仓落盘**：任务单落在 **`ai-ink-brain-api-python/docs/tasks/`** 的后端 task，其 **任务审核全文** 归档在 **`ai-ink-brain-api-python/docs/harness/reviews/`**（命名规则与本节一致）；本目录可仅存 **指针 md** 链向子仓，避免双份漂移。  
> **对话发起模板**：[`../prompts/TEMPLATE-task-audit-invoke.md`](../prompts/TEMPLATE-task-audit-invoke.md)（占位符未替换时 **Agent 须追问**，不得落盘；与 `22` 双向关联）。  
> **新帽节 Invoke 快照**（每帽 **首次** 粘贴已替换 §3 时的可追溯锚点，**非**审查结论本身）：[`../invokes/README.md`](../invokes/README.md)；审查 md 元信息可增 **`invoke_snapshot`** 列链回对应文件。

---

## 命名建议

| 场景 | 建议文件名 |
|------|------------|
| 首轮审查 | `task_<slug>_audit_R1_YYYYMMDD.md` |
| 任务帽回填后复审 | 递增 `R2`、`R3`… 或新日期后缀；**须在文首「关联」** 链回上一轮文件 |

路径：**工作区根** 下为 `docs/harness/reviews/<文件名>.md`；**后端仓** 下为 `ai-ink-brain-api-python/docs/harness/reviews/<文件名>.md`（见上「子仓落盘」）。

### 本目录指针索引（工作区 · 链向子仓真值）

| 指针文件 | 子仓 task（当前路径） |
|----------|------------------------|
| [`pointer_…_graph_query_v1_audit_R1_20260517.md`](pointer_task_engineering_tech_graph_v2_graph_query_v1_audit_R1_20260517.md) | `ai-ink-brain-api-python/docs/tasks/done/task_engineering_tech_graph_v2_graph_query_v1.md` |
| [`pointer_…_graph_query_v1_audit_R2_20260517.md`](pointer_task_engineering_tech_graph_v2_graph_query_v1_audit_R2_20260517.md) | 同上 |
| [`pointer_…_p4_extended_v1_audit_CLOSE_20260517.md`](pointer_task_engineering_tech_graph_v2_p4_extended_v1_audit_CLOSE_20260517.md) | `…/done/task_engineering_tech_graph_v2_p4_extended_v1.md` |
| [`pointer_…_p4_bc_followup_v1_audit_CLOSE_20260517.md`](pointer_task_engineering_tech_graph_v2_p4_bc_followup_v1_audit_CLOSE_20260517.md) | `…/done/task_engineering_tech_graph_v2_p4_bc_followup_v1.md` |
| [`pointer_…_gate_a_perf_compare_v1_audit_R2_20260515.md`](pointer_task_engineering_tech_graph_gate_a_perf_compare_v1_audit_R2_20260515.md) | `…/done/task_engineering_tech_graph_gate_a_perf_compare_v1.md` |
| ChatBI 系列 `task_chatbi_*_audit_*.md`（本目录） | 正文在 `ai-ink-brain-api-python/docs/harness/reviews/` |

**工作区 Harness task**（非子仓）：[`task_engineering_tech_graph_gate_a_closeout_v1_audit_R*.md`](task_engineering_tech_graph_gate_a_closeout_v1_audit_R4_20260515.md) → [`../tasks/done/task_engineering_tech_graph_gate_a_closeout_v1.md`](../tasks/done/task_engineering_tech_graph_gate_a_closeout_v1.md)。

> 已归档子仓 task 一律链 **`docs/tasks/done/`**；勿再写 `active/`（历史审查正文中的流程叙述除外）。

---

## 闭环流程（审核 → 回填 → 再审）

1. **任务审核帽** 产出本目录下的 **审查文档**（**无阻塞亦须产出**，可为「零阻塞记录」模板）。  
2. 若有 **需改动项**：交由 **任务帽**（`prompts/10-requirements.md`）按审查文档的 **回填清单** 更新 **task 正文**（含 `docs/harness/tasks/` 或子仓 task）。  
3. **再次** 由任务审核帽产出 **新一轮** 审查文档（`R2`…），直至审查文档中声明 **可关闭** 或 **仍阻塞**（阻塞须写清）。  
4. **任务正式结束点**：在 **最终一轮** 审查文档的 **「签收 / 关闭」** 节写明结论；task 头部 `done` **须与此节一致**。终轮可设 **`human_gate: HG-AUDIT-CLOSE`**（`pending` → 人改 `approved` 后方可合并，见 [`../prompts/HANDOFF_SEMI_AUTO.md`](../prompts/HANDOFF_SEMI_AUTO.md)）。  
5. **自检结论**：执行闭环中 **`### 自检结论（执行者）`** 由 **自检帽** 写入 task（见 `../prompts/40-self-check.md`）；与 **审查签收** 分列，复检可同时核对二者。  
6. **Invoke 快照**（建议）：每顶帽子 **新开局** 时落盘 §3 调用体（见 [`../invokes/README.md`](../invokes/README.md)）；在审查 md 元信息记 **`invoke_snapshot`**，与第 1 步产出的审查路径形成 **指令 → 结论** 双锚点。

---

## 修订记录

| 日期 | 摘要 |
|------|------|
| 2026-05-13 | v1：目录说明、命名、闭环与终点点约定 |
| 2026-05-13 | v1.1：闭环第 5 步链 **自检结论** 回填 task（`40-self-check`） |
| 2026-05-14 | v1.2：链 **任务审核调用模板** `../prompts/TEMPLATE-task-audit-invoke.md`（占位符追问规则） |
| 2026-05-14 | v1.3：**子仓落盘**：`ai-ink-brain-api-python` 的 `docs/harness/reviews/` 为后端 task 审核全文真值；本目录可存指针 |
| 2026-05-14 | v1.4：链 **Invoke 快照** 总规 [`../invokes/README.md`](../invokes/README.md)；审查元信息可记 `invoke_snapshot` |
| 2026-05-14 | v1.5：闭环第 6 步 **Invoke 快照** 与审查双锚点 |
| 2026-05-18 | v1.6：指针索引；子仓 task 链 `done/`；补 P2-4 CLOSE 指针 |

---

## 给 Cursor

`Harness`、`reviews`、`任务审核`、`审计`、`R1`、`签收`、`闭环`、`docs/harness/tasks`、`自检结论`、`TEMPLATE-task-audit-invoke`、`invokes`、`invoke_snapshot`
