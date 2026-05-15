# Task：闸口 A 收口 — LLM 架构可读 vs 浏览器性能（跨仓执行清单）

> **状态**：`draft`  
> **类型**：工作区 Harness（`docs/harness/tasks/active/`）；**同时**涉及 `ai-ink-brain` 与 `ai-ink-brain-api-python` 文档/归档，执行 Agent 须按 §「执行顺序」分 PR 或单 PR 多路径说明。  
> **关联**：`ai-ink-brain-api-python/docs/tech_graph/gate_a_scheme1_backend.md`；`docs/tech_graph/改进方向.md` v1.1.3  
> **test_strategy**：`recommended`  
> **test_strategy_note**：以前端 `pnpm test` / `quality` 与后端 `pytest` 子集为主；闸口表部分为人工填数，须在 task「实现备忘」链 PR / run。  
> **freeze_id**：`TECH_GRAPH_S1_FREEZE_20260514_V1_1_3`

---

## 0. 概念澄清（给执行 Agent，避免过度做页面）

| 目标 | 是否必须做「前端页面渲染」对比 |
|------|----------------------------------|
| **方案1 + `graph.json`**：让 **LLM / Agent** 以 **低 token、确定性** 读懂 **依赖与架构**（见 `改进方向.md`） | **否**。文件在仓内、CI `--check` 即可；**不要求**为 LLM 专门做用户可见的 Mermaid/JSON **双渲染页**。 |
| **闸口 A §3.2「运行时」**：对比 **浏览器里** 消费 JSON vs 消费 Mermaid 的 **首屏 / 包体 / 冷解析** | **仅当你要写满闸口 §6「前端子表」或要引用 §5 阈值下结论时**才需要；否则可在 `gate_a_scheme1_backend.md` **显式声明**：「主结论以 **Agent 上下文口径**（token/体积/后端生成耗时）为准；**浏览器子表标为 N/A 或附录**」。 |

执行 Agent **默认路径**：以 **`gate_a_scheme1_backend.md`「结论」→ 主结论口径（2026-05-15）** 为准——**§3.2 浏览器子表 N/A**、主结论 **Agent/LLM**；优先完成 **P0–P1 + 后端归档 + 父文档 §6 勾选与一句书面结论**；**勿**在无产品需求时强行做 §3.2 全量浏览器对比。

---

## 1. 范围 / 非范围

**范围**

- **前端仓**：补齐 `ai-ink-brain/content/tasks/active/task_engineering_tech_graph_graph_json_export_v1.md` §4 / §8；确认 `docs/_tech_graph/graph.json` 已提交且 `quality` 含 graph `--check`；可选：`quality` 增加 `tech_graph_token_estimate.py --json`（与后端 CI 对称）。  
- **后端仓**：若 `task_engineering_tech_graph_graph_json_export_v1.md` 与 `task_engineering_tech_graph_gate_a_token_compare_v1.md` 已验收，按该仓 `docs/tasks/README.md` **`git mv` 至 `done/`** 并更新 `_views/done.md`。  
- **闸口父文档**：在 `gate_a_scheme1_backend.md` §6 勾选已具备证据的行；若不做浏览器子表，写一句 **N/A 理由** 链回本节 §0。

**非范围**

- 方案2 / Neo4j；跨仓合并一份 `graph.json`。  
- 为 LLM 单独开发「双轨可视化产品页」（除非产品需求单独立项）。

---

## 2. 依赖（相对工作区根 `Projects/`）

| 项 | 路径 |
|----|------|
| 闸口父文档 | `ai-ink-brain-api-python/docs/tech_graph/gate_a_scheme1_backend.md` |
| 前端 graph task | `ai-ink-brain/content/tasks/active/task_engineering_tech_graph_graph_json_export_v1.md` |
| 后端 graph / token task | `ai-ink-brain-api-python/docs/tasks/active/` 下对应 `task_engineering_tech_graph_*.md`（若已 `done/` 则改链） |

---

## 3. 验收标准（可勾选）

- [ ] **§0 策略已写明**：`gate_a_scheme1_backend.md` 或本 task「实现备忘」中二选一：**(A)** 补齐 §3.2 浏览器指标 **或** **(B)** 声明浏览器子表 N/A、主结论以 Agent 口径为准。  
- [ ] **前端** `task_engineering_tech_graph_graph_json_export_v1.md`：§4 与 §8 与仓库实际 `quality.yml` / `graph.json` 一致。  
- [ ] **后端** 相关 task 已归档或仍 `active` 的理由一行写在实现备忘。  
- [ ] `gate_a_scheme1_backend.md` §6 与「结论」段与 §0 策略一致，无空白矛盾。

---

## 4. failure_paths

| ID | 触发 | 行为 |
|----|------|------|
| FP-1 | 未声明 §3.2 又勾选「前端子表」 | 退回补声明或补数据 |
| FP-2 | 仅改父文档未链 PR / run | 父文档不得标「已验收」 |

---

## 5. 执行顺序（建议）

1. 读 `gate_a_scheme1_backend.md` §6 与 §0 表，**先定策略 (A)/(B)**。  
2. **前端仓** PR：task §4/§8、可选 token CI、`pnpm test` / `quality` 绿。  
3. **后端仓** PR：仅归档与索引（若未归档）。  
4. **父文档** PR（可在任一侧仓带工作区相对路径说明）：更新 §6、结论、快照引用。

---

## 6. 实现备忘（执行 Agent 回填）

| 项 | 内容 |
|----|------|
| §3.2 策略 | (A) 全量浏览器 / (B) N/A + 理由 |
| 前端 PR | |
| 后端归档 PR | |
| 父文档更新 PR | |

---

## 给 Cursor

`gate_a`、`graph.json`、`quality`、`LLM`、`§3.2`、`freeze_id`、`docs/harness/tasks`
