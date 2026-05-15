# Task：闸口 A 收口 — LLM 架构可读 vs 浏览器性能（跨仓执行清单）

> **状态**：`done（2026-05-15 验收通过）`  
> **类型**：工作区 Harness（已归档至 `docs/harness/tasks/done/`）；**同时**涉及 `ai-ink-brain` 与 `ai-ink-brain-api-python` 文档/归档，执行 Agent 须按 §「执行顺序」分 PR 或单 PR 多路径说明。  
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

- **前端仓**：`graph.json` 任务真值已收敛至 **`ai-ink-brain/content/tasks/done/task_engineering_tech_graph_graph_json_export_v1.md`**（§4 / §9 与 `quality.yml`、`package.json` 一致）；已删除与 `done/` 重复的 **`content/tasks/active/`** 同名稿；确认 `docs/_tech_graph/graph.json` 已提交且 `quality` 含 graph `--check`；可选：`quality` 增加 `tech_graph_token_estimate.py --json`（与后端 CI 对称）。  
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
| 前端 graph task | `ai-ink-brain/content/tasks/done/task_engineering_tech_graph_graph_json_export_v1.md` |
| 后端 graph / token task | `ai-ink-brain-api-python/docs/tasks/done/task_engineering_tech_graph_graph_json_export_v1.md`、`ai-ink-brain-api-python/docs/tasks/done/task_engineering_tech_graph_gate_a_token_compare_v1.md` |

---

## 3. 验收标准（可勾选）

- [x] **§0 策略已写明**：`gate_a_scheme1_backend.md` 或本 task「实现备忘」中二选一：**(A)** 补齐 §3.2 浏览器指标 **或** **(B)** 声明浏览器子表 N/A、主结论以 Agent 口径为准。（**实现备忘**显式 **(B)**；**父文档 §6** 已由 **2026-05-15 后端棒** 在子仓 `gate_a_scheme1_backend.md` 逐项勾选并补 **FP-2** 链 PR #26 Actions run。）  
- [x] **前端** `task_engineering_tech_graph_graph_json_export_v1.md`（`content/tasks/done/`）：§4 与 §9 与仓库实际 `quality.yml` / `graph.json` / `package.json` 一致（2026-05-15 勘误）。  
- [x] **后端** 相关 task 已归档：`docs/tasks/done/` + `_views/done.md`（见 §6 实现备忘）；两单 §4 验收项此前已全勾。  
- [x] `gate_a_scheme1_backend.md` §6 与「结论」段与 §0 策略 **(B)** 一致；§6 末 **FP-2** 段链 **PR #26** run id（与「仓库或 CI 快照引用」一致）。

---

## 4. failure_paths

| ID | 触发 | 行为 |
|----|------|------|
| FP-1 | 未声明 §3.2 又勾选「前端子表」 | 退回补声明或补数据 |
| FP-2 | 仅改父文档未链 PR / run | 父文档不得标「已验收」 |

---

## 5. 执行顺序（建议）

1. 读 `gate_a_scheme1_backend.md` §6 与 §0 表，**先定策略 (A)/(B)**。  
2. **前端仓** PR：graph task §4 / §9（`content/tasks/done/`）与 `quality.yml` 一致、可选 token CI、`pnpm test` / `quality` 绿。  
3. **后端仓** PR：仅归档与索引（若未归档）。  
4. **父文档** PR（可在任一侧仓带工作区相对路径说明）：更新 §6、结论、快照引用。

---

## 6. 实现备忘（执行 Agent 回填）

| 项 | 内容 |
|----|------|
| §3.2 策略 | **(B)** 浏览器子表 **N/A**；主结论以 **Agent/LLM**（token / 体积 / 后端生成耗时）为准，与 `gate_a_scheme1_backend.md`「结论」及主 task §0 默认路径一致。 |
| 前端 PR | `ai-ink-brain`：勘误 `content/tasks/done/task_engineering_tech_graph_graph_json_export_v1.md`；删除 `active/` 重复稿；工作区 invoke：`docs/harness/invokes/invoke_20260515_1200_30_tech-graph-gate-a-closeout.md`。 |
| 后端归档（子仓 cwd） | `ai-ink-brain-api-python`：`git mv` 两单至 `docs/tasks/done/`；头部 **`done（2026-05-15 验收通过）`**；`docs/tasks/_views/done.md` 已追加索引；开帽 invoke：`docs/harness/invokes/invoke_20260515_1535_30_tech-graph-gate-a-closeout-backend.md`。 |
| 父文档 §6 + FP-2 | 同子仓 `docs/tech_graph/gate_a_scheme1_backend.md`：§6 五项 `[x]` 与 **(B)** /「结论」对齐；**FP-2** 段链 **PR #26** `tech-graph` run **`25905101651`**、`tech-graph-contract` run **`25905101628`**（与文内「仓库或 CI 快照引用」一致）。**PR #26 描述**已续链 **`pytest`**（`.github/workflows/pytest.yml`）run **`25905249428`**（`headSha` 与 PR head 对齐）；PR **已于 2026-05-15 合并**（merge commit `53bae076`）。**按审查 R3 回填**：`task_engineering_tech_graph_gate_a_closeout_v1_audit_R3_20260515.md`。 |

---

### 自检结论（执行者）

| 项 | 结果 |
|----|------|
| **cwd** | `ai-ink-brain`（子仓根） |
| **命令** | `pnpm install --frozen-lockfile && pnpm lint && pnpm test && pnpm build` |
| **退出码** | **0**（`pnpm install` / `lint` / `test` / `build` 均成功） |
| **验收（主 task §3）** | 前端 graph task 与 `quality.yml` 对齐：**pass**。§0 **(B)**：实现备忘已写明。**后端归档 + 父文档 §6**：已由 **后端棒**（本文件下一小节）完成；FP-2 见父文档 §6 末段 + 实现备忘。 |
| **Invoke** | `docs/harness/invokes/invoke_20260515_1200_30_tech-graph-gate-a-closeout.md` |

**命令输出要点**

- `pnpm install --frozen-lockfile`：Lockfile up to date，`Done`（本地 Node **v25.9.0**，`package.json` engines 期望 **24.x**，有 WARN，CI 使用 `setup-node` 24 不受影响）。  
- `pnpm lint`：`eslint` 无报错退出。  
- `pnpm test`：`vitest run` → **Test Files 3 passed (3)**，**Tests 8 passed (8)**。  
- `pnpm build`：`next build --webpack` → **Compiled successfully**，静态页生成完成，退出 **0**。

#### 后端棒（`ai-ink-brain-api-python`，2026-05-15）

| 项 | 结果 |
|----|------|
| **Invoke** | `docs/harness/invokes/invoke_20260515_1535_30_tech-graph-gate-a-closeout-backend.md` |
| **cwd** | `ai-ink-brain-api-python`（子仓根） |
| **命令** | `pytest tests -m "not intent_eval and not intent_benchmark"` |
| **退出码** | **0** |
| **要点输出** | `148 passed, 2 deselected`；`tests/test_tech_graph_graph_export.py` **6 passed**；`tests/test_tech_graph_token_estimate.py` **3 passed**；约 **26.7s**。 |
| **归档 / 父文档** | 两后端 task 已 `git mv` → `docs/tasks/done/`；`gate_a_scheme1_backend.md` §6 与 FP-2 留痕已改签（见 §6 实现备忘）。 |

#### 自检帽汇总（2026-05-15 · hat 40）

| 项 | 内容 |
|----|------|
| **Invoke** | `docs/harness/invokes/invoke_20260515_1600_40_tech-graph-gate-a-closeout-self-check.md` |
| **与实现备忘核对** | **前端棒** invoke / 命令与 §6「前端 PR」行一致；**后端棒** invoke / pytest 摘要与 §6「后端归档」「父文档 §6 + FP-2」行一致。 |
| **本棒命令** | `cd ai-ink-brain-api-python` → `pytest tests -m "not intent_eval and not intent_benchmark"` |
| **退出码** | **0** |
| **要点输出** | `148 passed, 2 deselected`；`test_tech_graph_graph_export.py` **6 passed**；`test_tech_graph_token_estimate.py` **3 passed**；约 **33.8s**（本地 Python 3.11.15）。 |
| **文档抽样** | `gate_a_scheme1_backend.md` §6 五项 `- [x]` + **FP-2** 段含 run **`25905101651`** / **`25905101628`**；`docs/tasks/_views/done.md` 含两后端 task 索引；`docs/tasks/done/` 下两单文件存在。 |
| **已知未测项** | 本棒**未**在 `ai-ink-brain` 根重跑 **pnpm quality 全链**；双仓全量证据以前端棒 invoke `invoke_20260515_1200_30_tech-graph-gate-a-closeout.md` 已填摘要为准。**PR #26** 描述已补 **`pytest`** run **`25905249428`** 并已 **merge**（见 §6 实现备忘「父文档 §6 + FP-2」行）。 |

---

### 修订记录

| 日期 | 摘要 |
|------|------|
| 2026-05-15 | **按审查 R4 回填**：`task_engineering_tech_graph_gate_a_closeout_v1_audit_R4_20260515.md`（零阻塞签收）；invoke：`docs/harness/invokes/invoke_20260515_1830_22_tech-graph-gate-a-closeout-audit-r4.md`。 |

---

## 给 Cursor

`gate_a`、`graph.json`、`quality`、`LLM`、`§3.2`、`freeze_id`、`docs/harness/tasks`
