# docs/harness（工作区级 Harness 文档）

| 文件 | 说明 |
|------|------|
| [HARNESS_V2_PLAN.md](HARNESS_V2_PLAN.md) | Harness V2 初版规划：分层落盘、三支柱、`test_strategy` 等 task 字段、CI 批次 |
| [HARNESS_V2_P0_ACCEPTANCE.md](HARNESS_V2_P0_ACCEPTANCE.md) | **P0 验收单**：已落地 workflow、代码变更摘要、本地/ GitHub 勾选验收、与 Actions 关系说明 |
| [VERIFICATION_CI_PATTERN.md](VERIFICATION_CI_PATTERN.md) | **P2 可选 Verification**：`verify-fast` 与 `quality`/`pytest` 边界、形态 A/B、分支保护要点 |
| [tasks/README.md](tasks/README.md) | **工作区 Harness 任务**：`active/`、`done/`、`_views/` 规则与索引（跨子仓流程/CI/帽子等） |
| [prompts/README.md](prompts/README.md) | **角色帽子 Prompt**（`*.md`）：与 [`HARNESS_V2_PLAN.md`](HARNESS_V2_PLAN.md) **§3** 同步；**对话调用模板**见 [`prompts/TEMPLATE-requirements-invoke.md`](prompts/TEMPLATE-requirements-invoke.md)（`10`）、[`prompts/TEMPLATE-review-spec-task-invoke.md`](prompts/TEMPLATE-review-spec-task-invoke.md)（`20`）、[`prompts/TEMPLATE-task-audit-invoke.md`](prompts/TEMPLATE-task-audit-invoke.md)（`22`）、[`prompts/TEMPLATE-execute-invoke.md`](prompts/TEMPLATE-execute-invoke.md)（`30`）、[`prompts/TEMPLATE-self-check-invoke.md`](prompts/TEMPLATE-self-check-invoke.md)（`40`）、[`prompts/TEMPLATE-independent-reinspect-invoke.md`](prompts/TEMPLATE-independent-reinspect-invoke.md)（`50`） |
| [reviews/README.md](reviews/README.md) | **任务审核产出**：每轮审查必落盘；闭环 R1/R2…；**签收 / 关闭** 与 task 状态对齐 |
| [invokes/README.md](invokes/README.md) | **新帽节 Invoke 快照**：每帽首次发起时落盘已替换占位符的 §3 调用体；与 `reviews/`、task 自检并列可追溯 |
| [Harness工程测评-Desktop-Projects-ai-ink.md](Harness工程测评-Desktop-Projects-ai-ink.md) | Ink 全栈三方测评（Inform/Constrain/Verify）；**§8** 为 P0 CI 落地对照；**2026-05-14** 起含远端 PR 与任务收口补充 |

**入口**：根目录 [`README.md`](../../README.md)（**cyning-ink-workspace**）、[`AGENTS.md`](../../AGENTS.md) **§8**。

---

## 修订记录

| 日期 | 摘要 |
|------|------|
| 2026-05-13 | v1.1：索引增补 `reviews/README.md`（任务审核落盘与终点点） |
| 2026-05-13 | v1.2：入口链指向根目录 `README.md` / `AGENTS.md`（`../../`）；标注工作区名 **cyning-ink-workspace** |
| 2026-05-14 | v1.3：远端 PR 验收与运维结论落盘 — [`HARNESS_V2_P0_ACCEPTANCE.md`](HARNESS_V2_P0_ACCEPTANCE.md) §4/§6/§6.1；[`HARNESS_V2_PLAN.md`](HARNESS_V2_PLAN.md) §10；[`tasks/README.md`](tasks/README.md)「当前状态」；[`VERIFICATION_CI_PATTERN.md`](VERIFICATION_CI_PATTERN.md) §5.1 |
| 2026-05-14 | v1.4：任务审核对话模板 [`prompts/TEMPLATE-task-audit-invoke.md`](prompts/TEMPLATE-task-audit-invoke.md)（与 `22` / `reviews` 关联；占位符未替换则 Agent 追问） |
| 2026-05-14 | v1.5：`10` / `20` 调用模板 [`prompts/TEMPLATE-requirements-invoke.md`](prompts/TEMPLATE-requirements-invoke.md)、[`prompts/TEMPLATE-review-spec-task-invoke.md`](prompts/TEMPLATE-review-spec-task-invoke.md)；索引表链四模板 |
| 2026-05-14 | v1.6：`40` / `50` 调用模板 [`prompts/TEMPLATE-self-check-invoke.md`](prompts/TEMPLATE-self-check-invoke.md)、[`prompts/TEMPLATE-independent-reinspect-invoke.md`](prompts/TEMPLATE-independent-reinspect-invoke.md)；索引表链六模板 |
| 2026-05-14 | v1.7：[`invokes/README.md`](invokes/README.md)（新帽节 Prompt 快照约定与 `reviews` 互链） |
| 2026-05-15 | v1.8：Invoke 快照 **首份示例** 落盘（子仓 `ai-ink-brain-api-python/docs/harness/invokes/` + 工作区 [`invokes/pointer_invoke_chatbi_v3_task_audit_r2.md`](invokes/pointer_invoke_chatbi_v3_task_audit_r2.md) 指针） |
