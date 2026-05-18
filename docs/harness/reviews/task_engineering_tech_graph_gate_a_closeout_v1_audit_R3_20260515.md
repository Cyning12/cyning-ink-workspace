# 任务审核：闸口 A 收口（Gate A closeout）— R3

## 元信息

| 项 | 内容 |
|----|------|
| **关联 task** | [`docs/harness/tasks/done/task_engineering_tech_graph_gate_a_closeout_v1.md`](../tasks/done/task_engineering_tech_graph_gate_a_closeout_v1.md)（审查时曾为 `active/`） |
| **轮次** | R3（链回 [`task_engineering_tech_graph_gate_a_closeout_v1_audit_R2_20260515.md`](./task_engineering_tech_graph_gate_a_closeout_v1_audit_R2_20260515.md)） |
| **审查日期** | 2026-05-15 |
| **invoke_snapshot** | `docs/harness/invokes/invoke_20260515_1630_22_tech-graph-gate-a-closeout-audit-r3.md`（本轮任务审核帽 22 开帽） |
| | `docs/harness/invokes/invoke_20260515_1200_30_tech-graph-gate-a-closeout.md`（前端执行 30） |
| | `docs/harness/invokes/invoke_20260515_1535_30_tech-graph-gate-a-closeout-backend.md`（后端执行 30） |
| | `docs/harness/invokes/invoke_20260515_1600_40_tech-graph-gate-a-closeout-self-check.md`（自检帽 40） |
| **对照规约** | `docs/harness/prompts/22-task-audit.md`、`docs/harness/reviews/README.md`、`docs/harness/HARNESS_V2_PLAN.md` §5 |

---

## 审查结论摘要

本轮执行 **R3 预审硬条件**：以 **`gh pr view 26 --repo Cyning12/ai-ink-brain-api-python --json state,mergedAt,body`**（审查时拉取）核对 **PR #26** 与主 task 头部 **`状态`**。

- **R3 硬条件 1（pytest Actions 续链）**：**未满足**。PR **body** 已含 **`tech-graph`**、**`tech-graph-contract`** 之 Actions run URL（与 task / 父文档 FP-2 已写 id 一致），但 **未**出现 **`.github/workflows/pytest.yml` / workflow `pytest`** 对应 **GitHub Actions run 的独立 URL（含数字 run id）** 续链；与 R2 阻塞项及主 task **§6 实现备忘**末句要求 **仍不一致**。  
- **R3 硬条件 2（合并后核对）**：**不适用本轮结论主链**。`mergedAt` 为 **`null`**，**`state`：`OPEN`**，故 **不**进入「在 merge commit 或默认分支最新 pytest run 上核对 id」分支。  
- **与 HARNESS_V2_PLAN §5 对齐**：`test_strategy: recommended` 合法；已配 **`test_strategy_note`**；`failure_paths` 表可操作化；头部未写 **`gates_before_code`** 不构成本 task 缺口（§5.4 为可选）。`failure_paths` 未列「可重试」属 **Harness 建议增强**，**非**本轮签收阻塞。

---

## 阻塞 / 非阻塞

| 类型 | 说明 |
|------|------|
| **阻塞（R3 硬条件 / 远程留痕）** | 在 **https://github.com/Cyning12/ai-ink-brain-api-python/pull/26** 的 **PR 描述正文**中追加一行（与现有 Actions 小节并列）：指向 **`.github/workflows/pytest.yml`**（展示名 **`pytest`**）的 **GitHub Actions run 完整 URL**，且 URL 中含 **数字 run id**（可与 `tech-graph` 同 PR 上触发的某次 run 对应，但须在描述中 **显式** 标为 pytest workflow，避免仅靠本地 Test plan 文字替代）。 |
| **阻塞（Harness 归档硬规则前置）** | 主 task 仍为 **`> **状态**：`draft`** 且文件在 **`docs/harness/tasks/active/`**；按 `docs/harness/tasks/README.md`，**禁止**仅改头部为 `done` 而不 **`git mv` 至 `done/`** 及更新 **`_views/done.md`**。在 PR #26 **未合并**、远程 pytest 链 **未闭合** 前，**不**建议宣布 Harness 主 task **正式关闭**。 |
| **非阻塞** | 父文档 `gate_a_scheme1_backend.md` §6 / FP-2 仓内链 **tech-graph** / **contract** run 与 task 实现备忘一致；§3 验收勾选与自检链在 **文档层** 与 R2 一致，**未被本轮 GitHub 核验推翻**。 |

---

## 需任务帽回填清单（若有）

| # | 项 | 建议位置 / 动作 |
|---|-----|----------------|
| 1 | **维护者**：在 PR #26 **描述**追加 **pytest** workflow **Actions run URL（含 run id）**（满足 FP-2 / R3 硬条件）。 | GitHub PR #26 **body** |
| 2 | **PR #26 合并后**：主 task 头部 **`状态`** 改为 **`done（YYYY-MM-DD 验收通过）`**；`git mv` **`docs/harness/tasks/active/task_engineering_tech_graph_gate_a_closeout_v1.md`** → **`docs/harness/tasks/done/`**；在 **`docs/harness/tasks/_views/done.md`** 追加链接；若曾列入 **`in_progress.md`** 则同步更新。 | `docs/harness/tasks/README.md` 归档流程 |
| 3 | （可选）若合并后默认分支上 **pytest** 有新 run id 与描述不一致：在 PR 描述或顶帖评论 **更正** 为默认分支上 **真值 run**。 | GitHub / 与父文档「快照引用」二选一策略 |

---

## 是否建议执行帽开工

**不建议**。在 **PR 描述 pytest Actions 续链** 与 **合入 + Harness 主 task 归档** 完成前，继续扩写业务代码 **无增量价值**；应先完成上表 **阻塞项**。

---

## 签收 / 关闭

- **本轮（R3）**：**声明主 task 尚不可正式关闭**。理由：**R3 预审硬条件未满足**（PR #26 **OPEN** 且 **描述缺 `pytest.yml` / `pytest` workflow 之 Actions run URL**）；主 task **仍为 `draft` 且位于 `active/`**，与 **`docs/harness/tasks/README.md`** 的 **done** 约定 **不一致**。  
- **任务正式关闭条件（供 R4 及以后）**：PR #26 **描述**含 **pytest** workflow **Actions run URL（含 id）**；PR **已合并**（或团队书面豁免）；主 task **状态 + 路径** 与 README **归档硬规则** 一致；下一轮任务审核 **R4** 可出具 **零阻塞签收**。

---

## 下一棒可复制 Prompt

以下与 **对话回复** 中同名字段 **逐字一致**（`text` 围栏内为已替换占位符正文；选用 **`docs/harness/prompts/TEMPLATE-requirements-invoke.md` §3**，与 `22-task-audit.md` **交接物**（1）（2）一致）。

```text
你正在扮演工作区 Harness「需求与任务分析帽」，严格遵循：
- docs/harness/prompts/10-requirements.md（身份、只做什么、禁止什么、输出形状、停止条件、交接物）
- docs/harness/HARNESS_V2_PLAN.md §5（与 task 字段对齐时可引用）

输入（已由人工替换占位符；若你仍看到 {{…}} 字样，须先追问用户，不得开工）：

【目标与上下文】
补齐 GitHub PR #26（Cyning12/ai-ink-brain-api-python）描述中缺失的 `.github/workflows/pytest.yml`（workflow 展示名一般为 `pytest`）对应 **GitHub Actions run 的完整 URL（含数字 run id）**，以满足闸口父文档 FP-2 与 Harness R3 审查硬条件；待 PR 合并后，按 `docs/harness/tasks/README.md` 将工作区主 task `docs/harness/tasks/active/task_engineering_tech_graph_gate_a_closeout_v1.md` 更新为 `done（YYYY-MM-DD 验收通过）` 并 `git mv` 至 `docs/harness/tasks/done/`，同步 `_views/done.md`，以便后续 **R4 任务审核** 零阻塞签收。

【已有材料路径或粘贴说明】
docs/harness/tasks/active/task_engineering_tech_graph_gate_a_closeout_v1.md
ai-ink-brain-api-python/docs/tech_graph/gate_a_scheme1_backend.md

【是否按任务审核文档回填】（无则写「无」；有则写相对路径）
docs/harness/reviews/task_engineering_tech_graph_gate_a_closeout_v1_audit_R3_20260515.md

你必须完成：
0. **Invoke 快照（开帽起点）**：在输出下列第 1 条起的实质性结果之前，先将 **本用户消息全文**（= 本模板 §3、占位符已全部替换）按 `docs/harness/invokes/README.md` 落盘到 `Projects/docs/harness/invokes/`（含元数据表 + 快照 fenced code）。同一会话内追问 **不** 再新增快照文件。
1. 输出结构化块：背景 / 范围 / 非范围 / 依赖链接 / 验收列表 / failure_paths / 给执行帽的必读列表；矛盾单独小节（若有）。
2. 注明建议 test_strategy（required | recommended | not_applicable）及 test_strategy_note（若 not_applicable 须附理由）。
3. 若 AUDIT 路径非「无」：按该审查文档的回填清单逐条映射到 task 小节建议，并在建议文末注明「按审查 R3 回填」应指向的文件名。
4. 禁止：写业务实现代码；改 CI；在 task 中写绝对本机路径；把未在依赖中声明的契约当真值。
5. 对话回复：生成可以完整复制的 Prompt，用于直接交给下一棒执行；须兼顾打回、二次审查等情形，下一棒也可能是上一棒（由其修复问题）。

不强制落盘；若用户要求写入某 task 文件，须由用户明确路径后再编辑（本模板不预置写文件占位符）。
```

---

## 给下一棒

（1）审查 md 相对工作区根路径：**`docs/harness/reviews/task_engineering_tech_graph_gate_a_closeout_v1_audit_R3_20260515.md`**；（2）请先完成 **GitHub PR #26 描述** 的 **pytest Actions 续链** 与（适用时）**合入 + 主 task 归档**；再粘贴上文 **「下一棒可复制 Prompt」** 内全文开 **需求帽**，或待闭环后改用 **`TEMPLATE-task-audit-invoke.md` §3** 发起 **R4 任务审核**。

---

## 修订记录

| 日期 | 摘要 |
|------|------|
| 2026-05-15 | R3：`gh pr view 26` 核验；R3 硬条件未满足；明确不可关闭；链 R2 |
