# SPEC — 方案1：静态依赖矩阵（graph.json）

## 定位

- **前置依赖**：后端无。Ink 前端须先完成 **R1**（仓根 `_tech_graph/` → `docs/_tech_graph/` 迁移，见 [改进方向.md](../../改进方向.md)）。
- **核心产出**：各子仓 **一份** `graph.json`（机器可读依赖图），与同仓 `docs/_tech_graph/*.ai.md`（及协议 `99_mermaid_protocol.md`）对齐；与 `_contract_manifest.json` **并行互补**（契约 vs 架构依赖，见 [SPEC/README.md](../README.md)）。

## 路径（阶段顺序）

1. **输入约定**：锁定扫描目录、忽略规则（如 `99_*`）、边类型与 Mermaid 语法映射。
2. **导出管线**：遍历 `.ai.md` → 解析 flowchart / classDiagram 边 → 归一节点与边类型。
3. **落盘契约**：`graph.json` schema 版本字段、生成时间、与图谱目录的相对路径（按承接仓定稿）。
4. **CI 门禁**：再生或与仓库内文件 diff，不一致则失败；PR 须带更新后的 `graph.json`。
5. **消费约定**：规则 / 帽子中「影响分析前先读 `graph.json`」的引用方式（仅路径级，文案由需求方写）。

## 与下游方案的关系

- **方案2** 只消费本方案产物，不重复解析 Mermaid（除非备选路径另行规定）。
- **方案3** 导入脚本以本方案 `graph.json` 为权威输入之一。

## 已定稿（路径与并行关系）

- **输入根（后端）**：`ai-ink-brain-api-python/docs/_tech_graph/`（在该仓根执行脚本时参数为 `docs/_tech_graph`）。
- **输入根（前端）**：`ai-ink-brain/docs/_tech_graph/`（同上；**物理真值须先完成 R1 迁移**，见 [改进方向.md](../../改进方向.md)「架构决议」）。
- **输出**：与各输入根同目录的 `graph.json`（前后端各一份；跨仓合并策略若需要另开 SPEC，默认不合并）。
- **与契约**：`_contract_manifest.json`（当前主要见后端仓 `docs/_tech_graph/`）与 `tech_graph_contract_check.py` 与 `graph.json` 导出 **并行**，CI 可同 job 顺序跑、独立失败。
- **task 草案**：工作区 `docs/tech_graph/tasks/ai-ink-brain-api-python/`、`docs/tech_graph/tasks/ai-ink-brain/` 分目录落盘（见 [tasks/README.md](../../tasks/README.md)）。

## 仍待执行方补全

- Ink 前端 **R1** 迁移 task 的 PR 链接与完成日期（未完成前勿将前端 `graph.json` CI 标为必绿）。
- 脚本具体文件名、`--check` 语义、`test_strategy`、解析失败时的 stderr 格式等（见子仓 task）。
