# tech_graph — 图依赖加速（SPEC 索引）

## 递进关系（总览）

```text
方案1  graph.json（静态、可 diff、CI 门禁）
   │
   ├─→ 方案2  内存查询 + CLI/MCP + Harness 挂钩（依赖方案1）
   │
   └─→ 方案3  Neo4j（可选；依赖方案1；与方案2 并存或切换，由需求方定稿）
```

- **方案1**：基线；无前置。
- **方案2**：在方案1 之上，降低 Agent 自行解析 JSON 的成本。
- **方案3**：规模或图分析诉求上来时可选；**不**取消方案1 作为导出与契约对齐的合理基线（除非后续 SPEC 另有决策）。

详述与示例见上级文档：[改进方向.md](../改进方向.md)。

## 分路径 SPEC（骨架）

| 文件 | 内容重心 |
| --- | --- |
| [scheme_1_graph_json.md](./scheme_1_graph_json.md) | 导出路径、CI、消费约定占位 |
| [scheme_2_graph_query.md](./scheme_2_graph_query.md) | 加载、查询面、调用面、帽子挂钩 |
| [scheme_3_neo4j.md](./scheme_3_neo4j.md) | 导入、Cypher、运维与 CI 边界、与方案2 关系 |

本目录仅保留**路径顺序与依赖关系**；字段级需求、接口表、验收清单由后续需求文档补全。
