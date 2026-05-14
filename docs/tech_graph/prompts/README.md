# tech_graph 专题 — Prompts（已填调用体）

## 与 `docs/harness/prompts/` 的分工

| 目录 | 放什么 | 不放什么 |
| --- | --- | --- |
| **`docs/harness/prompts/`** | Harness **帽子母版**（`10`/`20`/`22`/`30`/`40`/`50`）、**`TEMPLATE-*-invoke.md`**、**`EXAMPLE-*`** 等通模 | 某一业务专题（如本 tech_graph）的 **已填长 Prompt**、迭代中的对话体 |
| **`docs/tech_graph/prompts/`**（本目录） | 仅 **本专题** 的 **已替换占位符** 的可复制 Prompt、场景化 invoke 说明、与 SPEC 强绑定的调用正文 | Harness 通模副本；避免与 `TEMPLATE-*` 同名混淆 |

**规则（强制）**：凡为 **tech_graph / graph.json / 三方案** 起草的 **生成型、已填 Prompt**，一律落本目录；**禁止**再新增到 `docs/harness/prompts/`（除非升级为 Harness 通用模板并经规划修订）。

**帽子真值仍链 Harness**：正文里引用 `docs/harness/prompts/10-requirements.md` 等 **不**表示文件要迁到 Harness 目录，仅表示 **行为约束** 仍以 Harness 文档为准。

## 本目录索引

| 文件 | 用途 |
| --- | --- |
| [PROMPT-filled-requirements-tech-graph-phase1-v1.md](./PROMPT-filled-requirements-tech-graph-phase1-v1.md) | 需求帽：方案1 双仓 task 初稿（已填，复制 §A） |

## 命名建议

| 片段 | 含义 |
| --- | --- |
| `PROMPT-filled-` | 已填占位符，可直接贴对话 |
| `requirements` / `execute` / `review` | 对应帽子简称 |
| `tech-graph` | 专题 slug |
| `phaseN` / `v1` | 阶段与版本 |

## 给 Cursor

`tech_graph`、`prompts`、`已填 Prompt`、`不污染 harness`、`TEMPLATE`
