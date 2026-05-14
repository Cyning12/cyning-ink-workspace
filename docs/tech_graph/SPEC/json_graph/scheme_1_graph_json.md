# SPEC — 方案1：静态依赖矩阵（graph.json）

## 定位

- **前置依赖**：后端无。Ink 前端须满足 **R1**（图谱根 **仅** `docs/_tech_graph/`；历史仓根 `_tech_graph/` 迁移见 [改进方向.md](../../改进方向.md) **R1**；v1.1.1 / v1.1.3 起聚合仓可认定 **物理条件已满足**，与下文「仍待补全」不矛盾）。
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
- **输入根（前端）**：`ai-ink-brain/docs/_tech_graph/`（在该仓根执行脚本时参数为 `docs/_tech_graph`）；**物理真值**须符合 **R1**（见 [改进方向.md](../../改进方向.md)「架构决议」与 v1.1.3）。
- **输出**：与各输入根同目录的 `graph.json`（前后端各一份；跨仓合并策略若需要另开 SPEC，默认不合并）。
- **与契约**：`_contract_manifest.json`（当前主要见后端仓 `docs/_tech_graph/`）与 `tech_graph_contract_check.py` 与 `graph.json` 导出 **并行**，CI 可同 job 顺序跑、独立失败。
- **task 草案**：工作区 `docs/tech_graph/tasks/ai-ink-brain-api-python/`、`docs/tech_graph/tasks/ai-ink-brain/` 分目录落盘（见 [tasks/README.md](../../tasks/README.md)）。
- **承接仓规约片段（演进稿）**：`docs/tech_graph/spec/…`（与 `tasks/` 同型；见 [spec/README.md](../../spec/README.md)）。

## 仍待执行方补全

- **R1 与前端 graph CI 必绿（消歧，与 [`改进方向.md`](../../改进方向.md) v1.1.1 / v1.1.3 一致）**：工作区聚合仓复检认定 Ink 前端 **R1 物理条件已满足**（图谱仅在 `docs/_tech_graph/`、仓根无历史 `_tech_graph/`）。在此前提下，**允许且推荐**在子仓 task 落地后将 **前端** `graph.json` **再生成 / `--check`** 纳入 **PR 必绿**（与 **quality** 的先后由前端 task 约定）。若某 fork / 克隆 **仍**存在仓根 `_tech_graph/`，**该环境**须先按规划完成 **R1 迁移 task** 再绑定 graph 门禁，**不**与「已满足物理条件的仓库」混为一谈。
- Ink 前端 **R1** 迁移 task 的 **PR 链接与完成日期**（审计留痕；**不**再作为「禁止前端 graph CI 必绿」的前置）。
- 脚本具体文件名、`--check` 语义、`test_strategy`、解析失败时的 stderr 格式等（见子仓 task）。
