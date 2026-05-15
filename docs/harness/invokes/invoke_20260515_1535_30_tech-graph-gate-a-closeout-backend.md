# Harness invoke snapshot

| 字段 | 值 |
|------|-----|
| hat_id | 30 |
| template | 用户粘贴 · 执行编码帽（后端 `ai-ink-brain-api-python` 棒） |
| task_paths | `docs/harness/tasks/active/task_engineering_tech_graph_gate_a_closeout_v1.md` |
| related_review_or_none | `docs/harness/reviews/task_engineering_tech_graph_gate_a_closeout_v1_audit_R1_20260515.md` |
| created_utc_or_local | 2026-05-15（本地） |
| notes | 上一棒前端 invoke：`docs/harness/invokes/invoke_20260515_1200_30_tech-graph-gate-a-closeout.md` |

## 可复制 Prompt 快照（与对话首条 user 一致）

```text
你正在扮演工作区 Harness「执行编码帽」，严格遵循：
- docs/harness/prompts/30-execute-code.md
- docs/harness/prompts/40-self-check.md
- docs/harness/HARNESS_V2_PLAN.md §5
- 子仓 `ai-ink-brain-api-python/AGENTS.md`、主 task 内依赖与 §0、根 `AGENTS.md` §8（VERIFY 以本消息 + `ai-ink-brain-api-python/.github/workflows/pytest.yml` 为准）

输入（占位符须已替换；见 {{…}} 则先追问，不得开工写业务代码）：
- 主 task 路径（相对工作区根 Projects/）：
docs/harness/tasks/active/task_engineering_tech_graph_gate_a_closeout_v1.md
- 子仓根（相对 Projects/；pytest / git 默认 cwd）：
ai-ink-brain-api-python
- 合并前须跑通的验证命令：
pytest tests -m "not intent_eval and not intent_benchmark"
- 关联任务审核书面结论路径（无则写「无」）：
docs/harness/reviews/task_engineering_tech_graph_gate_a_closeout_v1_audit_R1_20260515.md
- 关联 SPEC / 总规：
docs/tech_graph/改进方向.md
ai-ink-brain-api-python/docs/tech_graph/gate_a_scheme1_backend.md

你必须完成：
0. 若为新会话开帽：按 `docs/harness/invokes/README.md` 将**本消息全文**落盘到 `Projects/docs/harness/invokes/`（新 `invoke_*` 文件名，勿覆盖 `invoke_20260515_1200_30_...`）。
1. 通读主 task：§3 未勾两项（**后端归档**、**父文档 §6**）、FP-2、实现备忘中前端已写 **(B)** 与 pending。
2. **后端仓**：若 `task_engineering_tech_graph_graph_json_export_v1.md` 与 `task_engineering_tech_graph_gate_a_token_compare_v1.md` 已验收，按 `docs/tasks/README.md` **`git mv`** 至 `docs/tasks/done/` 并更新 `docs/tasks/_views/done.md`；否则在**主 task §6 实现备忘**写一行 **仍 active 的理由**。
3. **父文档**：编辑 `docs/tech_graph/gate_a_scheme1_backend.md` — §6 勾选与 **(B)** /「结论」一致；在实现备忘或 PR 描述中链 **PR 号或 Actions run id**（满足 FP-2）。
4. 在 `ai-ink-brain-api-python` 根执行 VERIFY 至全绿，或记录环境阻塞并停止扩写。
5. 在**主 task** 正文 **`### 自检结论（执行者）`** **追加**本棒：命令、退出码、要点输出（勿删除前端已填小节，可并列子表或加「后端棒」子标题）。
6. 对话末尾再给出 **下一棒** 可复制 Prompt（自检帽 / 审查帽 R2 / 或打回前端修复）。

禁止：无 PR/run 留痕即在父文档写「已验收」；口头宣称已测而无命令摘要。

链路上一 invoke（前端棒，可复核）：`docs/harness/invokes/invoke_20260515_1200_30_tech-graph-gate-a-closeout.md`
```
