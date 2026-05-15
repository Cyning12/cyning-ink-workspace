# Harness invoke snapshot

| 字段 | 值 |
|------|-----|
| hat_id | 30 |
| template | 工作区执行编码帽用户消息（对齐 `docs/harness/prompts/30-execute-code.md`） |
| task_paths | ai-ink-brain-api-python/docs/tasks/active/task_chatbi_v3_prompt_injection_guard_poc_v1.md |
| related_review_or_none | ai-ink-brain-api-python/docs/harness/reviews/task_chatbi_v3_sql_ast_and_prompt_injection_audit_R3_20260515.md |
| created_utc_or_local | 2026-05-14（会话锚点） |
| notes | VERIFY：`pytest tests -m "not intent_eval and not intent_benchmark"` cwd `ai-ink-brain-api-python` |

## 可复制 Prompt 快照（与对话首条 user 一致）

```text
你正在扮演工作区 Harness「执行编码帽」，严格遵循：
- docs/harness/prompts/30-execute-code.md（身份、只做什么、禁止什么、拒开工、输出形状、交接物）
- docs/harness/prompts/40-self-check.md（验证命令、回填 task「### 自检结论（执行者）」）
- docs/harness/HARNESS_V2_PLAN.md §5（test_strategy、failure_paths、gates_before_code）
- 子仓 ai-ink-brain-api-python/AGENTS.md、task 内「给执行帽的必读列表」、工作区根 AGENTS.md §8（合并前必绿命令真值，若与本条 VERIFY 冲突以 task + 子仓 workflow 为准）

输入（已由人工替换占位符；若你仍看到 {{…}} 或「待填」，须先追问用户，不得开工写业务代码）：
- 主 task 路径（相对工作区根 Projects/）：
ai-ink-brain-api-python/docs/tasks/active/task_chatbi_v3_prompt_injection_guard_poc_v1.md
- 子仓根（相对 Projects/；所有 git/pytest 默认 cwd）：
ai-ink-brain-api-python
- 合并前须跑通的验证命令（与 CI / task 一致）：
pytest tests -m "not intent_eval and not intent_benchmark"
- 关联任务审核书面结论路径（无则「无」）：
ai-ink-brain-api-python/docs/harness/reviews/task_chatbi_v3_sql_ast_and_prompt_injection_audit_R3_20260515.md
- 关联 SPEC / 总规（无则「无」）：
ai-ink-brain-api-python/docs/spec/v3-agent/SPEC-ChatBI-V3-Security.md
ai-ink-brain-api-python/docs/spec/v3-agent/SPEC-ChatBI-V3-Overview.md
ai-ink-brain-api-python/docs/spec/v3-agent/SPEC-ChatBI-V3-Logging-Trace.md
ai-ink-brain-api-python/docs/spec/v3-agent/SPEC-ChatBI-V3-Identity-Access-OpenItems.md

你必须完成：
0. Invoke 快照（开帽起点）：在输出下列第 1 条起的实质性结果之前，先将本用户消息全文按 docs/harness/invokes/README.md 落盘到 Projects/docs/harness/invokes/（含元数据表 + 快照 fenced code）。同一会话内追问不再新增快照文件。
1. 通读 task 全文：gates_before_code、test_strategy / test_strategy_note、freeze_id、failure_paths、拒开工、验收、必读、非范围；对照 §5 实现备忘（含已写死的 FP-1 envelope 与 golden 路径）。
2. 若仍有拒开工条件未满足 → 仅输出 Markdown 阻塞清单，不写业务实现代码。
3. test_strategy: required：先保证/补充可失败 pytest，再改实现；禁止只写实现后补测。
4. 在 ai-ink-brain-api-python 内按 task 范围实现 Prompt guard PoC；遵守与 P1-1 SQL gate 的先后顺序（须在 §5 写死后再动 text2sql_core 主链）。
5. 在子仓根执行上述 VERIFY 命令，修复直至通过或记录环境阻塞。
6. 按 40-self-check.md 回填 task「### 自检结论（执行者）」。
7. 对话回复末尾给出：可交给下一棒（自检帽或任务审核帽 R4）的完整可复制 Prompt；若 task 与审查帽约定要求，自检/审查输出中下一棒 Prompt 须与对话逐字一致。

禁止：未读完必读与 failure_paths 即改路由/契约；无关大段重构；无命令输出却声称已测。
```
