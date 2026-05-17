# docs/harness/prompts（Harness 角色帽子）

> **用途**：各 **帽子** 的短 system 前缀素材（Markdown）；与 [`../HARNESS_V2_PLAN.md`](../HARNESS_V2_PLAN.md) **§3** 硬规则摘要语义对齐，按需复制到对话。  
> **真值**：规划 §3、§5；本目录为 **Guides** 层，**不替代** CI 与 task 正文。  
> **专题已填 Prompt**：业务线（如 tech_graph）的 **已替换占位符** 长调用体 **不**放本目录，见 **`docs/tech_graph/prompts/`**（与 `TEMPLATE-*` 分工，避免污染 Harness 通模）。

---

## 使用方式

1. 按当前对话角色打开下表对应文件。  
2. 将全文或「身份 + 只做什么 + 禁止什么」段复制为 **system 前缀**（或粘贴到项目规则前的固定说明）。  
3. 将 **task / SPEC / diff / 日志** 作为 user 消息附上；复检帽 **不要** 附带执行过程长文（见 `50-independent-reinspect.md`）。  
4. **任务审核帽**（`22-task-audit.md`）每轮 **必须** 在 [`../reviews/README.md`](../reviews/README.md) 约定目录落盘；若有回填项 → **任务帽**（`10-requirements.md`）改 task → **再审** 产出 `R+1`；**任务签收** 以终轮审查文档 **「签收 / 关闭」** 为准（与 task 状态一致）。  
5. **新帽节 Invoke 快照（可追溯链环）**：每顶帽子 **首次** 把某 `TEMPLATE-*-invoke.md` **§3**（占位符已全部替换）粘贴进 **新对话** 时，将 **同一份正文** 落盘至 [`../invokes/README.md`](../invokes/README.md) 约定路径；**同一帽**内多轮追问 **不** 重复落盘。审查 md 元信息可增 **`invoke_snapshot`**；task 可选 **`### Invoke 快照（可选）`**。  
6. **快速发起任务审核（`22`）**：复制 [`TEMPLATE-task-audit-invoke.md`](TEMPLATE-task-audit-invoke.md) **§3** 正文并替换 **§2** 占位符；若占位符未替换，**Agent 须追问**，不得代填或落盘（见模板 **§1** 与 `22-task-audit.md` **关联模板**）。  
7. **快速发起需求分析（`10`）**：复制 [`TEMPLATE-requirements-invoke.md`](TEMPLATE-requirements-invoke.md) **§3** 并替换 **§2**；占位符未替换则 **Agent 须追问**（见模板 **§1** 与 `10-requirements.md` **关联模板**）。  
8. **快速发起规格短评（`20`）**：复制 [`TEMPLATE-review-spec-task-invoke.md`](TEMPLATE-review-spec-task-invoke.md) **§3** 并替换 **§2**；占位符未替换则 **Agent 须追问**（见模板 **§1** 与 `20-review-spec-task.md` **关联模板**）；须 **书面签收** 时改用第 6 步 **`22` 模板**。  
9. **快速发起执行（`30`）**：复制 [`TEMPLATE-execute-invoke.md`](TEMPLATE-execute-invoke.md) **§3** 正文并替换 **§2** 占位符；若占位符未替换，**Agent 须追问**，不得开工写业务代码（见模板 **§1** 与 `30-execute-code.md`）。  
10. **快速发起自检（`40`）**：复制 [`TEMPLATE-self-check-invoke.md`](TEMPLATE-self-check-invoke.md) **§3** 并替换 **§2**；占位符未替换则 **Agent 须追问**（见模板 **§1** 与 `40-self-check.md` **关联模板**）；须在 task 中落 **`### 自检结论（执行者）`**。  
11. **快速发起独立复检 / 全局验收（`50`）**：复制 [`TEMPLATE-independent-reinspect-invoke.md`](TEMPLATE-independent-reinspect-invoke.md) **§3**（**短版 · 默认**）并替换 **§2**；**`{{REINSPECT_MODE}}`** 须为 **`独立复检`** / **`全局验收`** / **`两者`** 之一；占位符未替换则 **Agent 须追问**（见模板 **§1** 与 `50-independent-reinspect.md`）。**全量升级（可选）**：[`TEMPLATE-independent-reinspect-invoke-full.md`](TEMPLATE-independent-reinspect-invoke-full.md) **§3**（结构化输出、`failure_paths` / `test_strategy` 专节、子仓 checklist、可选 `PR_OR_CI`）。**已填示例**：[`EXAMPLE-invoke-independent-reinspect-both-chatbi-p1-1.md`](EXAMPLE-invoke-independent-reinspect-both-chatbi-p1-1.md)。
12. **下一棒 Prompt 后自动 commit（全帽强制）**：凡本轮输出 **「下一棒可复制 Prompt」** 且已落盘工件，Agent **须在本轮对话结束前** 按 [`HANDOFF_AUTO_COMMIT.md`](HANDOFF_AUTO_COMMIT.md) 在**相关 git 根**分别 `commit`（仅本轮路径；对话末尾报 short-hash）。用户写明 **「本轮不要 commit」** 时可豁免。

---

## 文件列表与 §3 对照

| §3 帽子 | 本目录文件 | 说明 |
|--------|------------|------|
| 需求 / 任务分析 | [`10-requirements.md`](10-requirements.md) | 验收可观测、`failure_paths`、非范围、依赖链接；承接 **任务审核** 回填清单 |
| 规格 / 任务审查 | [`20-review-spec-task.md`](20-review-spec-task.md) | 对话内缺口短评；契约变更标 **冻结点升级**；**不要求**每次写 `reviews/` |
| **规格短评 · 调用模板** | [`TEMPLATE-review-spec-task-invoke.md`](TEMPLATE-review-spec-task-invoke.md) | 可复制 Prompt；占位符未替换则 **Agent 追问**；与 `20` 双向关联；书面审改用 `22` 模板 |
| **任务审核** | [`22-task-audit.md`](22-task-audit.md) | **强制** [`../reviews/`](../reviews/README.md) 落盘；R1/R2… 闭环；**签收 / 关闭** = 任务终点点 |
| **任务审核 · 调用模板** | [`TEMPLATE-task-audit-invoke.md`](TEMPLATE-task-audit-invoke.md) | 可复制 Prompt；占位符未替换则 **Agent 追问**、不得开工；与 `22` 双向关联 |
| **执行编码 · 调用模板** | [`TEMPLATE-execute-invoke.md`](TEMPLATE-execute-invoke.md) | 可复制 Prompt；占位符未替换则 **Agent 追问**；链 `30` + `40` + 验证命令 |
| 执行编码 | [`30-execute-code.md`](30-execute-code.md) | 必读路径、`test_strategy`、**拒开工**、TDD 衔接 |
| **自检 · 调用模板** | [`TEMPLATE-self-check-invoke.md`](TEMPLATE-self-check-invoke.md) | 可复制 Prompt；占位符未替换则 **Agent 追问**；与 `40` 双向关联；回填 `### 自检结论` |
| 自检（执行者） | [`40-self-check.md`](40-self-check.md) | 运行 task 所列命令；**回填** `### 自检结论（执行者）` |
| **独立复检 / 全局验收 · 调用模板** | [`TEMPLATE-independent-reinspect-invoke.md`](TEMPLATE-independent-reinspect-invoke.md) | 可复制 Prompt；MODE 三选一；占位符未替换则 **Agent 追问**；与 `50` 双向关联 |
| **独立复检 / 全局验收 · 全量调用模板（升级）** | [`TEMPLATE-independent-reinspect-invoke-full.md`](TEMPLATE-independent-reinspect-invoke-full.md) | 短版之上 v2；A～D 输出节、`PR_OR_CI` 可选；与短模板 **§4 关系表** 互链 |
| **独立复检 + 全局验收 · 已填示例** | [`EXAMPLE-invoke-independent-reinspect-both-chatbi-p1-1.md`](EXAMPLE-invoke-independent-reinspect-both-chatbi-p1-1.md) | ChatBI P1-1；由全量模板复制后替换占位符 |
| 独立复检 | [`50-independent-reinspect.md`](50-independent-reinspect.md)（前半） | diff + 日志 + 验收表；pass/fail + 证据 |
| 全局验收 | [`50-independent-reinspect.md`](50-independent-reinspect.md)（后半节） | `freeze_id` + 人签 checklist |
| **新帽节 Invoke 快照（工件目录）** | [`../invokes/README.md`](../invokes/README.md) | 每帽 **首次** 粘贴已替换 §3 时落盘；命名与元数据见该 README；与 `reviews`、task **`### Invoke 快照（可选）`** 互链 |
| **下一棒后自动 commit（通则）** | [`HANDOFF_AUTO_COMMIT.md`](HANDOFF_AUTO_COMMIT.md) | 产出下一棒 Prompt + 落盘后 **分仓 commit**；对话报 hash |

**与 §3 差异**：无实质规则冲突；本目录将表格摘要 **细化为可复制的角色指令**（含输入裁剪与输出形状）；**任务审核** 与 **审查短评** 拆分为 `22` / `20` 两顶帽子。§5 字段细则仍以规划正文为准。

---

## 修订记录

| 日期 | 摘要 |
|------|------|
| 2026-05-13 | v1：README + 5 顶帽子文件；与 `HARNESS_V2_PLAN` §3 对照表落盘 |
| 2026-05-13 | v1.1：增补 **任务审核** `22-task-audit.md`、`reviews/` 闭环与 §3 对照；使用方式第 4 步 |
| 2026-05-14 | v1.2：增补 [`TEMPLATE-task-audit-invoke.md`](TEMPLATE-task-audit-invoke.md)；使用方式第 5 步（占位符追问） |
| 2026-05-14 | v1.3：增补 [`TEMPLATE-execute-invoke.md`](TEMPLATE-execute-invoke.md）；使用方式第 6 步 |
| 2026-05-14 | v1.4：增补 [`TEMPLATE-requirements-invoke.md`](TEMPLATE-requirements-invoke.md)、[`TEMPLATE-review-spec-task-invoke.md`](TEMPLATE-review-spec-task-invoke.md)；使用方式第 6～8 步 |
| 2026-05-14 | v1.5：增补 [`TEMPLATE-self-check-invoke.md`](TEMPLATE-self-check-invoke.md)、[`TEMPLATE-independent-reinspect-invoke.md`](TEMPLATE-independent-reinspect-invoke.md)；使用方式第 9～10 步 |
| 2026-05-14 | v1.6：增补 [`EXAMPLE-invoke-independent-reinspect-both-chatbi-p1-1.md`](EXAMPLE-invoke-independent-reinspect-both-chatbi-p1-1.md)；README 表与第 10 步链入 |
| 2026-05-14 | v1.7：增补 [`TEMPLATE-independent-reinspect-invoke-full.md`](TEMPLATE-independent-reinspect-invoke-full.md)；第 10 步区分短版 / 全量 / EXAMPLE |
| 2026-05-14 | v1.11：声明专题已填 Prompt 放 `docs/tech_graph/prompts/`；撤除误增的 tech_graph 行与 v1.10 修订行 |
| 2026-05-17 | v1.12：增补 [`HANDOFF_AUTO_COMMIT.md`](HANDOFF_AUTO_COMMIT.md)；使用方式第 12 条 |

## 给 Cursor

`Harness`、`prompts`、`帽子`、`HARNESS_V2_PLAN` §3、`HANDOFF_AUTO_COMMIT`、`自动 commit`、`下一棒可复制 Prompt`、`拒开工`、`test_strategy`、`failure_paths`、`freeze_id`、`docs/harness/tasks`、`22-task-audit`、`reviews`、`invokes`、`invoke 快照`、`invoke_snapshot`、`签收`、`自检结论`、`TEMPLATE-task-audit-invoke`、`TEMPLATE-requirements-invoke`、`TEMPLATE-review-spec-task-invoke`、`TEMPLATE-execute-invoke`、`TEMPLATE-self-check-invoke`、`TEMPLATE-independent-reinspect-invoke`、`TEMPLATE-independent-reinspect-invoke-full`、`EXAMPLE-invoke-independent-reinspect-both-chatbi-p1-1`、`占位符`
