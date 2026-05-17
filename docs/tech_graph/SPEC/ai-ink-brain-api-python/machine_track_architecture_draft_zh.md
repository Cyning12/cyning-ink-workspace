# SPEC 草案 — Ink 后端技术图谱「机器轨」分层与 v2+query 终局

> **状态**：`draft`  
> **承接仓**：`ai-ink-brain-api-python`  
> **正式 task**：`ai-ink-brain-api-python/docs/tasks/active/task_engineering_tech_graph_v2_graph_query_v1.md`  
> **版本**：v0.1 · 2026-05-17  
> **上级**：[`改进方向.md`](../../改进方向.md) v1.1.3 · [`SPEC/README.md`](../README.md)

---

## 1. 目的

统一叙述 **人读轨 / 协议维护轨 / 机器轨 / 规范层** 职责，避免将方案1 误解为「给人加第三轨」或「用 v1 JSON 替换 `.ai.md`」。

**终局（G-END）**：优化 **机器轨消费**（manifest + contract + graph + query），而非取消人读 `*.md`。

---

## 2. 轨道定义

| 轨道 | 路径模式 | 读者 | 维护 | 备注 |
| --- | --- | --- | --- | --- |
| **人读轨** | `*.md`（`00_main`、`10_flow_*` 等） | 人 | 人 + Agent | 可裸边、审查友好 |
| **协议维护轨** | `*.ai.md` | Agent、导出器 | 人 + Agent | 非日常人扫读；**短期拓扑维护真值** |
| **机器轨 · 清单** | `_manifest.json` | Agent、CI | 人 + 脚本 | 端点/RPC/表/env/anchors |
| **机器轨 · 契约** | `_contract_manifest.json` | Agent、CI | 人 + 脚本 | SSE 等字段契约 |
| **机器轨 · 拓扑** | `graph.json`（v1→**v2**） | Agent、CI、query | **导出**，禁止手改 v1 惯例 |
| **机器轨 · 消费** | `tech_graph_graph_query`（方案2） | Agent | 代码 | **子图查询**，非整包灌入 |
| **规范层（人机同读）** | `01_struct`、`02_version`、`99_spec`、`99_mermaid_protocol` | 人 + Agent（按需） | 人 + Agent | **不**纳入 v1 flow 导出 |

---

## 3. 演进对照

```text
【旧 · 机器轨】 manifest + contract + *.ai.md（整包消费）

【方案1 · 已交付】 + graph_v1（从 *.ai.md 导出，有损拓扑）

【本草案 · 目标】
  manifest + contract
  + graph_v2（富化 + 等价门禁）
  + graph_query（方案2）
  + 按需：01_struct / 99_spec / *.ai.md 片段
```

---

## 4. graph_v1 未覆盖范围（设计边界，非遗漏）

| 文件 | 原因 |
| --- | --- |
| `01_struct.md` | classDiagram 表结构真值；规则禁止单靠 graph 推断表 |
| `02_version.md` | timeline 叙述，非依赖图 |
| `99_spec.md` / `99_mermaid_protocol.md` | 规约与协议；导出器跳过 `99_*` 且仅扫 `*.ai.md` |
| 人读 `10_flow_*.md` | 非导出输入；与 `.ai.md` 语义对齐即可 |

v2 **仍可不合并** 规范层全文；通过 **Agent 加载顺序** 与可选后续 `struct.json` 切片处理。

---

## 5. 等价性（论文对照 · 工程化）

| 论文概念 | 工程验收 |
| --- | --- |
| 三相塌缩等价（ARI=1） | 锚点集 + 边标签 + 拓扑 与 `.ai.md` 参考一致率达阈值 |
| 有损投影 | v1 整包 ≠ `.ai.md`；闸口 A 已否定「一律 JSON」 |
| SelectEnd（硬路由） | `graph_query` 返回 k-hop 子图，替代读 7 文件 mermaid 总串 |

---

## 6. 阶段门闸

| 闸口 | 状态 | 结论要点 |
| --- | --- | --- |
| **A**（方案1） | 已归档 | `gate_ctx_ab`：token≈1:1；P1/P2 偏 Mermaid；不签收 v1 整包 |
| **B**（方案2） | 本 SPEC 后续 | 现状 vs v1 vs **v2+query** |

---

## 7. 相关路径

| 类型 | 路径 |
| --- | --- |
| Task（draft） | `ai-ink-brain-api-python/docs/tasks/active/task_engineering_tech_graph_v2_graph_query_v1.md` |
| SPEC 方案1/2 | `docs/tech_graph/SPEC/json_graph/scheme_1_graph_json.md` · `query_graph/scheme_2_graph_query.md` |
| 实验定稿 | `ai-ink-brain-api-python/docs/diary/jsonPKmermaid/reports/conclusion_gate_ctx_ab_final_zh.md` |
