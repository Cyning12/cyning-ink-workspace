# Harness invoke snapshot

| 字段 | 值 |
|------|-----|
| hat_id | 40 |
| template | 用户粘贴 · 自检帽（执行者）`docs/harness/prompts/40-self-check.md` |
| task_paths | `docs/harness/tasks/active/task_engineering_tech_graph_gate_a_closeout_v1.md` |
| related_review_or_none | 链上一棒：`docs/harness/invokes/invoke_20260515_1535_30_tech-graph-gate-a-closeout-backend.md` |
| created_utc_or_local | 2026-05-15（本地） |
| notes | Gate A 收口自检；VERIFY cwd `ai-ink-brain-api-python` |

## 可复制 Prompt 快照（与对话首条 user 一致）

```text
你正在扮演工作区 Harness「自检帽（执行者）」，严格遵循：
- docs/harness/prompts/40-self-check.md
- docs/harness/HARNESS_V2_PLAN.md §5

输入（占位符须已替换；若仍见 {{…}} 须先追问，不得开工）：
- 主 task 路径（相对工作区根 Projects/）：
docs/harness/tasks/active/task_engineering_tech_graph_gate_a_closeout_v1.md
- 子仓根（相对 Projects/；本棒主 VERIFY cwd）：
ai-ink-brain-api-python
- 主验证命令（与 ai-ink-brain-api-python/.github/workflows/pytest.yml 一致）：
pytest tests -m "not intent_eval and not intent_benchmark"
- 变更范围说明（无则写「无」）：
Gate A 收口：子仓已 git mv 两后端 task 至 docs/tasks/done/ 并更新 gate_a_scheme1_backend.md §6 + FP-2；请复跑 pytest 并对照主 task §3 全四项给出 pass/fail 与证据；核对主 task「自检结论」中前端棒 + 后端棒与实现备忘一致。若需全量双仓证据，另在 ai-ink-brain 根重跑 pnpm quality 链并摘要回填。

你必须完成：
0. 按 docs/harness/invokes/README.md 将本消息全文落盘到 Projects/docs/harness/invokes/（新 invoke_*，勿覆盖 invoke_20260515_1535_30_tech-graph-gate-a-closeout-backend.md）。
1. 通读主 task 验收标准；在 ai-ink-brain-api-python 根执行上述 pytest，给出命令、退出码、要点输出。
2. 输出验收表（§3 每项 pass/fail + 证据）。
3. 视需要在主 task「### 自检结论（执行者）」增补「自检帽汇总」子表（勿删除已有前端棒/后端棒），写清命令列表、退出码、已知未测项。
4. 对话末尾给出下一棒可复制 Prompt（审查帽 R2 / 需求帽 / 或打回子仓补 PR 描述链 pytest.yml run id）。

上一棒 invoke（后端执行）：docs/harness/invokes/invoke_20260515_1535_30_tech-graph-gate-a-closeout-backend.md
```
