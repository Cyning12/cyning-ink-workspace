# SPEC — 方案2：内存图查询（工具可调用）

## 定位

- **前置依赖**：**方案1** 已产出稳定 `graph.json`（`schema_version: graph_v2`）；**闸口 A** 已归档（见 [改进方向.md](../../改进方向.md)）。
- **核心产出**：内存邻接结构 + 查询 API（CLI；MCP 为可选挂钩），供 Agent 确定性取「上下游 / 路径 / 影响描述」。
- **实现真值（后端子仓）**：`ai-ink-brain-api-python/tools/tech_graph_graph_query.py`（**非** `graph_query.py`）。

## 路径（阶段顺序）

1. **加载**：读入 `docs/_tech_graph/graph.json`，构建有向图（`ref` 边不参与 BFS）。
2. **查询面**：`query_downstream` / `query_upstream` / `query_neighbors` / `has_path` / `describe_impact`（见 §2 映射表）。
3. **调用面**：CLI（`execute_command`）；MCP 示例见子仓 `.cursor/mcp.json.example`（可选）。
4. **Harness 挂钩**：`docs/harness/prompts/TEMPLATE-task-audit-invoke.md` 含 **可选** 影响分析步骤（非硬阻塞）。
5. **降级**：未装 Neo4j 时本方案独立可用（与方案3 解耦）。
6. **阶段门闸**：**闸口 B** 已归档 — `ai-ink-brain-api-python/docs/diary/jsonPKmermaid/reports/conclusion_gate_b_ctx_query_v1_zh.md`（**禁止**在本 SPEC 任务中重跑 `run_gate_b_batch` 全 arms）。

## 规划别名 → 实现符号

| 规划（`改进方向.md` §2.3） | 实现 | 说明 |
| --- | --- | --- |
| `get_downstream(node, depth)` | `query_downstream(store, node_id, depth)` | JSON 子图 |
| `get_upstream(node, depth)` | `query_upstream(store, node_id, depth)` | JSON 子图 |
| — | `query_neighbors(store, node_id)` | 一跳邻域 |
| `has_path(from, to)` | `has_path(store, from_id, to_id)` | `bool` |
| `describe_impact(node)` | `describe_impact(store, node_id, depth=2)` | 人类可读 `str` |
| `get_all_affected(nodes[], depth)` | `tools/tech_graph_gate_b_query_union.py` 等 | **非**本模块 |

## CLI 真值

默认图路径：`docs/_tech_graph/graph.json`（可用 `--graph` 覆盖）。

```text
python tools/tech_graph_graph_query.py downstream <node_id> <depth>
python tools/tech_graph_graph_query.py upstream <node_id> <depth>
python tools/tech_graph_graph_query.py neighbors <node_id>
python tools/tech_graph_graph_query.py has-path <from_id> <to_id>
python tools/tech_graph_graph_query.py describe-impact <node_id> [depth]
```

退出码：`0` 成功；`2` 输入/解析；`4` FP-4 未知节点；`5` FP-5 非 graph_v2。

## 与上下游的关系

- **上游**：仅依赖方案1 导出的 **graph_v2** JSON。
- **下游**：方案3 **仅**在闸口 B 与 **R2** 后启用；并存冲突时 **以 Neo4j 为准**（**R3**）。

## 修订记录

| 版本 | 日期 | 说明 |
| --- | --- | --- |
| v0.1 | 2026-05-14 | 初稿占位 |
| v0.2 | 2026-05-18 | 对齐 `tech_graph_graph_query.py`；闸口 B 链出；补 has-path / describe-impact |
