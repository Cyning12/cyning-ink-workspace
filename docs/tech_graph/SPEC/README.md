# tech_graph — 图依赖加速（SPEC 索引）

## 递进关系（总览）

```text
方案1  graph.json（静态、可 diff、CI 门禁）→ 闸口 A 对比实验
   │
   ├─→ 方案2  内存查询 + CLI/MCP + Harness 挂钩（依赖方案1）→ 闸口 B 对比实验
   │
   └─→ 方案3  Neo4j（**仅**在方案2与闸口 B 完成后 **R2** 单独立项；与方案2 并存时 **R3 DB 优先**；依赖方案1 作导入基线）
```

- **方案1**：基线；Ink 前端须先满足 **R1** 物理路径。
- **方案2**：在方案1 之上，降低 Agent 自行解析 JSON 的成本；交付后须完成 **闸口 B** 方可考虑方案3。
- **方案3**：可选；**不**取消方案1 的 `graph.json` 可 diff 基线；开启前见 `改进方向.md` **R2**；冲突语义见 **R3**。

详述与示例见上级文档：[改进方向.md](../改进方向.md)。

## 图谱真值路径（前后端分仓，已消歧）

| 承接仓 | 仓库目录（相对工作区根） | Mermaid / 协议 / 本专题 `graph.json` 落点 |
| --- | --- | --- |
| 后端 | `ai-ink-brain-api-python/` | `docs/_tech_graph/` |
| 前端 | `ai-ink-brain/` | `docs/_tech_graph/`（**R1**：须自仓根历史 `_tech_graph/` 迁入后方可作为物理真值，见 [改进方向.md](../改进方向.md)） |

脚本、CI、文档中的路径均指 **在该子仓根目录下** 的相对路径（勿与工作区根 `docs/tech_graph/` 规划 SPEC 混淆）。

## `contract_manifest` 与 `graph.json`（并行、互补）

二者 **非替代关系**，管线可 **并行** 执行（同一 PR 内可各自失败）：

| 维度 | `_contract_manifest.json`（及契约校验） | `graph.json`（依赖导出） |
| --- | --- | --- |
| 描述对象 | SSE 等 **接口层** 字段契约 | **架构层** 模块/组件调用、数据流依赖 |
| 节点类型 | 事件类型、字段名、枚举值等 | 模块（如 rag、fts）、数据概念、路由等（以图中 id 为准） |
| 边类型 | 事件 → 必需字段、payload 结构 | `depends_on`、`async_calls`、`condition`、元关系等 |
| 主要用途 | 生成/校验代码、前后端字段一致 | 影响分析、变更传播、任务规划 |
| 对 AI | 写对契约少读长文 | 「改 A 影响谁」少遍历代码 |

## 本专题 task 草案落盘（工作区级）

与工作区 `tech_graph` 规划配套的 **草案 / 指针** 按前后端分子目录：`docs/tech_graph/tasks/ai-ink-brain-api-python/`、`docs/tech_graph/tasks/ai-ink-brain/`（见 [tasks/README.md](../tasks/README.md)）。各子仓正式 task 路径不变。

## 目录约定（防混）

| 子目录 | 对应方案 | 放置内容 |
| --- | --- | --- |
| [json_graph/](./json_graph/) | 方案1 | `graph.json` 导出、CI、消费约定等**仅方案1**的执行说明与派生文档 |
| [query_graph/](./query_graph/) | 方案2 | 内存图、CLI/MCP、Harness 挂钩等**仅方案2**的执行说明与派生文档 |
| [neo4j/](./neo4j/) | 方案3 | Neo4j 导入、Cypher、运维等**仅方案3**的执行说明与派生文档 |

**规则**：跨方案引用在正文里写清依赖即可；**不要**把某一方案的实施记录、runbook、任务拆解放到另一方案的子目录。各方案可在自己的目录下再建子文件夹（如 `runbooks/`、`ci/`），命名由执行方自定。

## 各方案骨架入口

| 方案 | 骨架文件 |
| --- | --- |
| 1 | [json_graph/scheme_1_graph_json.md](./json_graph/scheme_1_graph_json.md) |
| 2 | [query_graph/scheme_2_graph_query.md](./query_graph/scheme_2_graph_query.md) |
| 3 | [neo4j/scheme_3_neo4j.md](./neo4j/scheme_3_neo4j.md) |

本索引与上述骨架仅保留**路径顺序与依赖关系**；字段级需求、接口表、验收清单由后续在对应子目录内补全。
