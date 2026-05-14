# docs/harness/reviews（任务审核产出）

> **用途**：存放 **任务审核帽** 的**书面审查结果**（每轮必产出）；与 `prompts/22-task-audit.md` 配套。  
> **真值**：单条 task 是否可关闭，以 **审查文档「签收 / 关闭」** 节为准，并与 task 头部 `状态` 一致；**不得以聊天结论替代落盘**。  
> **子仓落盘**：任务单落在 **`ai-ink-brain-api-python/docs/tasks/`** 的后端 task，其 **任务审核全文** 归档在 **`ai-ink-brain-api-python/docs/harness/reviews/`**（命名规则与本节一致）；本目录可仅存 **指针 md** 链向子仓，避免双份漂移。  
> **对话发起模板**：[`../prompts/TEMPLATE-task-audit-invoke.md`](../prompts/TEMPLATE-task-audit-invoke.md)（占位符未替换时 **Agent 须追问**，不得落盘；与 `22` 双向关联）。

---

## 命名建议

| 场景 | 建议文件名 |
|------|------------|
| 首轮审查 | `task_<slug>_audit_R1_YYYYMMDD.md` |
| 任务帽回填后复审 | 递增 `R2`、`R3`… 或新日期后缀；**须在文首「关联」** 链回上一轮文件 |

路径：**工作区根** 下为 `docs/harness/reviews/<文件名>.md`；**后端仓** 下为 `ai-ink-brain-api-python/docs/harness/reviews/<文件名>.md`（见上「子仓落盘」）。

---

## 闭环流程（审核 → 回填 → 再审）

1. **任务审核帽** 产出本目录下的 **审查文档**（**无阻塞亦须产出**，可为「零阻塞记录」模板）。  
2. 若有 **需改动项**：交由 **任务帽**（`prompts/10-requirements.md`）按审查文档的 **回填清单** 更新 **task 正文**（含 `docs/harness/tasks/` 或子仓 task）。  
3. **再次** 由任务审核帽产出 **新一轮** 审查文档（`R2`…），直至审查文档中声明 **可关闭** 或 **仍阻塞**（阻塞须写清）。  
4. **任务正式结束点**：在 **最终一轮** 审查文档的 **「签收 / 关闭」** 节写明结论；task 头部 `done` **须与此节一致**。  
5. **自检结论**：执行闭环中 **`### 自检结论（执行者）`** 由 **自检帽** 写入 task（见 `../prompts/40-self-check.md`）；与 **审查签收** 分列，复检可同时核对二者。

---

## 修订记录

| 日期 | 摘要 |
|------|------|
| 2026-05-13 | v1：目录说明、命名、闭环与终点点约定 |
| 2026-05-13 | v1.1：闭环第 5 步链 **自检结论** 回填 task（`40-self-check`） |
| 2026-05-14 | v1.2：链 **任务审核调用模板** `../prompts/TEMPLATE-task-audit-invoke.md`（占位符追问规则） |
| 2026-05-14 | v1.3：**子仓落盘**：`ai-ink-brain-api-python` 的 `docs/harness/reviews/` 为后端 task 审核全文真值；本目录可存指针 |

---

## 给 Cursor

`Harness`、`reviews`、`任务审核`、`审计`、`R1`、`签收`、`闭环`、`docs/harness/tasks`、`自检结论`、`TEMPLATE-task-audit-invoke`
