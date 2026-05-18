# 任务审核：闸口 A 收口（Gate A closeout）

## 元信息

| 项 | 内容 |
|----|------|
| **关联 task** | [`docs/harness/tasks/done/task_engineering_tech_graph_gate_a_closeout_v1.md`](../tasks/done/task_engineering_tech_graph_gate_a_closeout_v1.md)（审查时曾为 `active/`） |
| **轮次** | R1 |
| **审查日期** | 2026-05-15 |
| **invoke_snapshot** | 无（本轮用户未提供已落盘 Invoke §3 快照路径） |
| **对照规约** | `docs/harness/prompts/22-task-audit.md`、`docs/harness/HARNESS_V2_PLAN.md` §5 |

---

## 审查结论摘要

本 task 为 **工作区级 Harness** 跨仓收口清单：`test_strategy: recommended` 与 `test_strategy_note` 已对齐 HARNESS §5.1；`freeze_id` 与父文档一致；**验收标准**可勾选且与 `gate_a_scheme1_backend.md` 现有「结论」「§3.2 N/A」「§6 交付物清单」叙事 **一致**；**failure_paths** 能约束文档与 PR 留痕类风险，但未覆盖 HARNESS §5.3 建议的「可重试 / 用户可见」字段（对本 task 以流程退回为主，**不视为拒开工硬阻塞**）。

**结论**：**无阻塞**；**建议执行帽**按 task **§5 执行顺序**开工；跨仓须 **分步 cwd / 分 PR**，勿以单仓 `VERIFY_COMMAND` 替代全文验收。

---

## 阻塞 / 非阻塞

| 类型 | 说明 |
|------|------|
| **阻塞** | 无 |
| **非阻塞（可选增强，交任务帽）** | （1）在 task 增补 **「必读（执行前）」** 3～5 条 bullets，与 `30-execute-code.md`「必读列表」措辞对齐，降低执行帽歧义。（2）`failure_paths` 每条可补 **可重试**（例：补声明/补 PR 描述后可再审）。（3）头部 `状态` 自 `draft` 升为 `active` 后再大规模分发执行（纪律项）。 |

---

## 需任务帽回填清单（若有）

本轮 **无必须回填项**。上表「非阻塞」为 **可选**；若采纳，由任务帽小改 task 后触发 **R2** 再审。

---

## 是否建议执行帽开工

**建议开工**。执行时请注意：

1. **主 task** 为工作区路径 `docs/harness/tasks/active/task_engineering_tech_graph_gate_a_closeout_v1.md`，勿仅执行子仓 graph task 而遗漏 **父文档 §6** 与 **归档** 条件。  
2. **§0 / 父文档**：`gate_a_scheme1_backend.md` 已在「结论」中写明 **Agent/LLM 主口径** 与 **§3.2 N/A**；执行侧仍需在 **§6** 勾选与 **实现备忘** 中 **显式 (B)** 留痕并与验收项对齐（满足 task §3 第一项）。  
3. **`TEMPLATE-execute-invoke.md` 仅单 `SUBPROJECT_ROOT`**：本 task 跨两子仓 → **每一子仓 PR** 各用一次执行 Invoke（或同会话内明确切换 cwd），VERIFY 分别对齐 `quality` / `pytest` 与 task 正文。

---

## 签收 / 关闭

- **本轮（R1）**：**不声明 task 可结束**。父文档 §6 勾选、前后端 task 对齐与归档、实现备忘回填等 **尚未在仓库内完成**（属执行帽工作范围）。  
- **任务正式关闭条件（供终轮引用）**：task §3 验收清单 **全勾**；`gate_a_scheme1_backend.md` §6 / 结论与 §0 策略无矛盾；实现备忘表填齐；task 头部状态与 Harness **done** 流程一致后，由 **终轮任务审核** 在 **签收 / 关闭** 节声明可关闭。

---

## 下一棒可复制 Prompt

以下与 **对话回复** 中「下一棒」块 **逐字一致**（`text` 围栏内为 `TEMPLATE-execute-invoke.md` §3 全文占位符已替换；**当前步**为 task §5 第 2 步 **前端仓**）。

```text
你正在扮演工作区 Harness「执行编码帽」，严格遵循：
- docs/harness/prompts/30-execute-code.md（身份、只做什么、禁止什么、拒开工、输出形状、交接物）
- docs/harness/prompts/40-self-check.md（验证命令、回填 task「### 自检结论（执行者）」）
- docs/harness/HARNESS_V2_PLAN.md §5（test_strategy、failure_paths、gates_before_code）
- 子仓 AGENTS.md、task 内「给执行帽的必读列表」、根 AGENTS.md §8（合并前必绿命令真值，若与本条 VERIFY 冲突以 task + 子仓 workflow 为准）

输入（已由人工替换占位符；若你仍看到 {{…}} 或「待填」，须先追问用户，不得开工写业务代码）：
- 主 task 路径（相对工作区根 Projects/）：
docs/harness/tasks/active/task_engineering_tech_graph_gate_a_closeout_v1.md
- 子仓根（相对 Projects/；所有 git/pytest/pnpm 默认 cwd）：
ai-ink-brain
- 合并前须跑通的验证命令（与 CI / task 一致）：
pnpm install --frozen-lockfile && pnpm lint && pnpm test && pnpm build
- 关联任务审核书面结论路径（无则「无」）：
docs/harness/reviews/task_engineering_tech_graph_gate_a_closeout_v1_audit_R1_20260515.md
- 关联 SPEC / 总规（无则「无」）：
docs/tech_graph/改进方向.md
ai-ink-brain-api-python/docs/tech_graph/gate_a_scheme1_backend.md

你必须完成：
0. **Invoke 快照（开帽起点）**：在输出下列第 1 条起的实质性结果之前，先将 **本用户消息全文**（= 本模板 §3、占位符已全部替换）按 `docs/harness/invokes/README.md` 落盘到 `Projects/docs/harness/invokes/`（含元数据表 + 快照 fenced code）。同一会话内追问 **不** 再新增快照文件。
1. 通读 task 全文：头部 `gates_before_code`、`test_strategy` / `test_strategy_note`、`freeze_id`、`failure_paths`、拒开工条件、验收标准、必读列表、非范围。
2. 若 task 明示拒开工条件未满足（缺 failure_paths 可操作性、缺验收命令、必读未覆盖等）→ **仅输出 Markdown 阻塞清单**（缺什么、建议回填的小节标题、推荐下一棒角色），**不写**业务实现代码。
3. `test_strategy: required` 时：先增加或调整 **可失败** 的自动化测试（或与实现同 PR 且满足 task 所述 red-green / 可复现失败语义），再改实现；禁止「只写实现、后补测」绕过 task 约定。
4. 在 `ai-ink-brain` 内按 task 范围改代码/配置；禁止静默扩大 scope；SPEC/task 矛盾走变更请求或交回需求帽，不擅自调和为代码假设。
5. 在子仓根执行 `pnpm install --frozen-lockfile && pnpm lint && pnpm test && pnpm build`（及 task 另行要求的命令），保留可核对输出要点；修复直至通过或记录环境阻塞并停止扩写。
6. 按 `40-self-check.md` 将结论与命令摘要 **回填** 至 task 正文 **`### 自检结论（执行者）`**（无则新增该小节）。
7. 对话回复：生成可以完整复制的 Prompt，用于直接交给下一棒执行；须兼顾打回、二次审查等情形，下一棒也可能是上一棒（由其修复问题）。

禁止：在未读完必读与 failure_paths 的情况下改路由/契约；删除与 task 无关的大段重构；口头宣称「已测过」而无命令输出。
```

**说明（不计入模板正文）**：完成 **前端仓** PR 后，对 **后端仓** 步骤请再次使用同一模板，将 **主 task 路径** 保持不变，将 **子仓根** 改为 `ai-ink-brain-api-python`，**VERIFY** 改为与 `ai-ink-brain-api-python/.github/workflows/pytest.yml` 及 task 一致之 `pytest tests -m "not intent_eval and not intent_benchmark"`（及 task 要求的 graph 子集若有）；**父文档**更新可在任一侧仓 PR 内完成，但须满足 task **FP-2**（PR / run 留痕）。

---

## 给下一棒

下一棒：**执行编码帽**；请先粘贴上文 **「下一棒可复制 Prompt」** 围栏内全文开会话；前端 PR 完成后按 **说明** 切换子仓再跑一轮 Invoke。

---

## 修订记录

| 日期 | 摘要 |
|------|------|
| 2026-05-15 | R1：零阻塞；建议执行；签收待执行与终轮 |
