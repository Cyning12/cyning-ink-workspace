# 工作区总调度（cyning-ink-workspace / 多子仓）

> **用途**：给「总 Agent」与「子 Agent」划定边界、阅读顺序与跨仓协作入口。  
> **范围**：**工作区根**（建议本地目录名 **`cyning-ink-workspace`**）下当前五个子目录；本文件不替代各仓内的规则文件（`.cursor/rules/*.mdc`）与项目配置真值表。  
> **语言**：说明以简体中文为主；代码与专有名词保持英文。  
> **新增权威规范**：全仓库统一在子仓 **`docs/_tech_graph/`** 维护技术图谱（目录名 `_tech_graph`）；物理落点与 Ink 前端 **R1** 迁移见 **第 7.0 节** 与 [`docs/tech_graph/改进方向.md`](docs/tech_graph/改进方向.md)。

---

## 1. 子项目一览（当前）

| 目录 | 角色 | 与谁关联 | Agent / 配置入口 |
|------|------|----------|------------------|
| `ai-ink-brain/` | Next.js 博客 + BFF、页面与本地 Node RAG、转发 Python API | 配对后端：`ai-ink-brain-api-python/`（`PY_API_URL`）；未来可承接 Snail 产出的内容资产 | `AGENTS.md` → `docs/meta/PROJECT_CONFIG_AI_INK_BRAIN.md`、`content/tasks/active/`、`content/tasks/done/`、`content/tasks/README.md`、`docs/_tech_graph/`、工作区规则（`.cursor/rules/*.mdc`） |
| `ai-ink-brain-api-python/` | FastAPI：Embedding / Chunking / Retrieval / ingest、RAG 日志 | 配对前端：`ai-ink-brain/`；不负责页面与 Next UX | `AGENTS.md` → `docs/meta/PROJECT_CONFIG_AI_INK_BRAIN_API_PYTHON.md`、`docs/tasks/*.md`、`docs/_tech_graph/`、工作区规则（`.cursor/rules/*.mdc`） |
| `Snail/py-Snail/` | 爬虫与抓取管线（Agent Tool、目录工作流、本地 / Supabase 等）；功能会持续迭代 | 规划：抓取结果未来进入 `ai-ink-brain` 的内容体系（具体落盘路径与契约待任务单约定）；与博客 RAG 共用概念上可能涉及同一 Supabase/pgvector，以各仓真值表为准 | `docs/task/`、`docs/webs/webs.md`、`supabase_sql/agent_crawler_documents.sql`、`.env.example`、`_tech_graph/` |
| `Python-learning/` | Python 语法练习与习题解析 | 默认隔离：一般不引用其他子项目代码或契约 | 该仓规则文件（`.cursor/rules/*.mdc`） |
| `secondCar/` | 二手车价格预测竞赛（数据科学） | 独立项目，不与其他子仓关联 | `AGENTS.md` → `README.md`、`docs/_tech_graph/`、该仓规则文件（`.cursor/rules/*.mdc`） |

---

## 2. 总设职责、任务单落盘与可读性（协作约定）

> 是否写入配置？**是**：以本 `AGENTS.md` §2 为权威（便于人读与 `@` 引用）；工作区规则以 `.cursor/rules/*.mdc` 为准，避免重复维护。子仓已有任务目录的，沿用下表路径，不另起命名体系。

### 2.1 总设（架构 / 统筹 Agent）做什么

- **全局**：对照本文件 §1、§3–§6 与各仓 `PROJECT_CONFIG_*.md`，划边界、拆需求、标依赖（前端 / 后端 / Snail / 跨仓）。
- **架构图谱化**：优先生成或更新 **`docs/_tech_graph/`** 下的 Mermaid 流程图、Struct 模型、版本时间线，作为全团队唯一可信架构来源。流程图必须维护双轨（`.md` + `.ai.md`），遵循拓扑协议。
- **任务初稿**：在对应子仓的任务目录新建或更新 Markdown；写清背景、范围、验收口径、风险，并预留「由前端 / 后端 Agent 补全」小节（实现细节、接口字段、测试列表等由子 Agent 丰富）。
- **真值不复制**：环境变量表、目录地图仍以各仓 `PROJECT_CONFIG` 为准；任务单内用链接或相对路径引用，避免复制粘贴导致漂移。

### 2.2 任务文档保存位置

| 子项目 | 任务目录（相对工作区根） | 命名建议 |
|--------|------------------------------|----------|
| 前端 Ink-Brain | `ai-ink-brain/content/tasks/active/`（归档：`content/tasks/done/`） | `task_<主题简写>.md`；规则见 `content/tasks/README.md` |
| 后端 API Python | `ai-ink-brain-api-python/docs/tasks/` | `*.md` |
| Snail | `Snail/py-Snail/docs/task/` | 同现有规范 |
| Python-learning | 无统一任务目录 | 练习即文件本体 |
| secondCar | `secondCar/docs/spec/` | 同现有规范 |

### 2.3 任务单结构（兼顾 Cursor 与人的阅读）

- **标题（H1）**：动词 + 范围。
- **元信息**：状态、关联图谱（`docs/_tech_graph/xxx.md`）、Issue/PR。
- **背景与目标**：短段落，描述完成态行为。
- **范围 / 非范围**：列表，减少越界。
- **依赖与引用**：`PROJECT_CONFIG`、API、表名、图谱文件路径。
- **验收标准**：`- [ ]` 可勾选列表。
- **实现备忘**：由子 Agent 回填文件列表、接口、图谱变更点。
- **测试策略（Harness V2）**：`test_strategy` 取 `required | recommended | not_applicable`；`required` 表示关键路径须先有可失败自动化测试再改实现；`not_applicable` 须附一行理由，禁止滥用。字段说明见 `docs/harness/HARNESS_V2_PLAN.md` **§5**。
- **失败路径**：建议独立小节（触发条件、系统行为/错误码、是否可重试、用户可见类型）；不明确时执行 Agent 可拒开工，仅输出缺口清单。与 **§8 Harness** 规划一致。
- **给 Cursor**：保留稳定关键词（验收、非范围、依赖、图谱、`docs/_tech_graph`、`test_strategy`、`failure_paths`、`Harness`）。

### 2.4 日记 / 日志（可复用规则）

- **日记正文**：`ai-ink-brain/content/diary/`（日期命名）
- **前端总结**：`ai-ink-brain/docs/diary/`
- **后端总结**：`ai-ink-brain-api-python/docs/diary/`
- **格式约束**：无绝对路径；单段不超 300 字

---

## 3. 调度顺序（总 Agent 建议 · 图谱优先增强版）

### 3.1 全栈 / RAG / 博客需求（图谱优先）

1. 读各仓 `docs/_tech_graph/` 图谱体系，理解整体流程与结构
2. 读前端真值表：`ai-ink-brain/docs/meta/PROJECT_CONFIG_AI_INK_BRAIN.md`
3. 读后端真值表：`ai-ink-brain-api-python/docs/meta/PROJECT_CONFIG_AI_INK_BRAIN_API_PYTHON.md`
4. 读对应任务单：`task_*.md`
5. 开发前先读图，开发后自动更新图谱
6. 遵守各仓规则文件（`.cursor/rules/*.mdc`），冲突以任务单 + 图谱 + 真值表为准

### 3.2 仅前端或仅后端

- 只动 UI/Next/BFF：仅在 `ai-ink-brain/` 内修改，以其 **`docs/_tech_graph/`** 为准（Ink 前端 **R1** 迁移见 [`docs/tech_graph/改进方向.md`](docs/tech_graph/改进方向.md)）
- 只动 RAG/ingest/DB：仅在后端仓修改，以其 **`docs/_tech_graph/`** 为准

### 3.3 Snail

- 以任务、图谱、代码入口为准
- 未来对接 Ink-Brain 时，同步更新双方 **`docs/_tech_graph/`** 与 `PROJECT_CONFIG`

### 3.4 Python-learning

- 独立练习，不拉通其他项目

### 3.5 secondCar

- 独立数据科学项目，不与其他子仓关联
- 以 `README.md` + `docs/_tech_graph/` + `docs/spec/` 为准

---

## 4. 跨仓协作要点（摘要）

| 要点 | 说明 |
|------|------|
| HTTP 契约 | 前端 `PY_API_URL` → Python 服务 |
| 向量 / 表结构 | 以各仓 `PROJECT_CONFIG`、`init.sql`、`docs/_tech_graph/01_struct.md` 为准 |
| 密钥规范 | 不上传 `.env`、API Key、service role |
| 架构一致性 | 跨仓流程变更必须同步更新对应 **`docs/_tech_graph/`** 图谱 |

---

## 5. 子仓 Agent 薄索引

| 子仓 | 入口文档 | 代码入口 |
|------|----------|----------|
| 前端 | `ai-ink-brain/AGENTS.md` + `docs/_tech_graph/` | `app/`、`components/`、`lib/` |
| 后端 | `ai-ink-brain-api-python/AGENTS.md` + `docs/_tech_graph/` | `api/index.py`、`api/ingest_pipeline.py`、`api/rag_env.py` |
| Snail | `Snail/py-Snail/AGENTS.md` | `app/main.py`、`app/services/` |
| secondCar | `secondCar/AGENTS.md` + `docs/_tech_graph/` | `code/main.py`、`feature/engineering.py`、`model/catboost_trainer.py` |

---

## 6. 维护说明

- **新增子项目时**：追加角色 / 关联仓 / 配置 / 任务路径 / 图谱目录
- **变更跨仓契约时**：同步更新 `PROJECT_CONFIG_*.md` + **`docs/_tech_graph/`** + 本节摘要
- **确保总 Agent 与子 Agent 永远以图谱为单一事实来源**，大幅降低幻觉与上下文爆炸。

---

## 7. 全仓库统一 `_tech_graph` 规范（强制）

### 7.0 物理落点（目录名仍为 `_tech_graph`）

- **Ink 前端**：`ai-ink-brain/docs/_tech_graph/`（若仓库仍为历史 **仓根** `_tech_graph/`，须先按 [`docs/tech_graph/改进方向.md`](docs/tech_graph/改进方向.md) **R1** 完成迁入）。
- **Ink 后端**：`ai-ink-brain-api-python/docs/_tech_graph/`。
- 下文树状结构及习惯简称 **`_tech_graph/`** 均指 **上述目录内的文件集合**（非工作区根路径）。

所有子项目必须遵守相同图谱结构：

```
docs/_tech_graph/   （位于各子仓内；仅示意，实际以各仓为准）
├─ 00_main.md              # 顶层流程总图（人类友好版）
├─ 00_main.ai.md           # 顶层流程总图（AI 协议版）
├─ 01_struct.md            # 数据结构/Struct 模型
├─ 02_version.md           # 版本迭代时间线
├─ 10_flow_*.md            # 业务子流程（人类友好版）
├─ 10_flow_*.ai.md         # 业务子流程（AI 协议版）
├─ 99_spec.md              # 实现规约
└─ 99_mermaid_protocol.md  # Mermaid 拓扑协议（流程图复杂的子项目使用）
```

### 7.1 双轨制

| 后缀 | 用途 | 维护者 | 适用图类型 |
|------|------|--------|-----------|
| `.md` | 人类友好版 | 开发者 | 全部 |
| `.ai.md` | AI 协议版 | LLM / 脚本 | flowchart 流程图 |

- **classDiagram / timeline / gantt** 等无流程边的图，无需 `.ai.md`
- **flowchart** 必须同时维护 `.md` + `.ai.md`，语义等价
- 修改代码后，优先更新 `.ai.md`，再同步 `.md`

### 7.2 拓扑协议（流程图强制）

边标记规范：
- `->` 同步执行、`~>` 异步（await）、`=>` 映射/赋值
- `?>` 条件分支、`[ok]` `[err]` 状态标记
- `::yields` `::branches` `::merges` `::triggers` `::gates` `::signoff` `::archives` 元关系

约束：
- 禁止裸边（无边标记的 `-->`）
- 锚点用 `// → path#Ln` 独立注释行
- 异常分支外挂，HappyPath 走主干

### 7.3 通用原则

- 图谱优先于纯文本文档
- 代码变更 → 自动增量更新图谱
- 禁止虚构结构、流程、字段
- 前后端 Snail secondCar 各自维护独立图谱，不互相覆盖

---

## 8. Harness 工程（V2 初版入口）

> **目标**：在现有 Inform（本文件、`PROJECT_CONFIG`、`docs/_tech_graph/`）与 Constrain（各仓 `.cursor/rules`、契约脚本）之上，补强 **Verify（CI 与可执行验收）**、**任务单测试策略**、以及 **角色帽子（Guides）** 与 SDD 的可执行闭环。

- **详规（初版 `draft`）**：[`docs/harness/HARNESS_V2_PLAN.md`](docs/harness/HARNESS_V2_PLAN.md) — 分层落盘、三支柱与帽子关系、`test_strategy` / `freeze_id` / `failure_paths` 字段细则、CI P0–P2 批次、修订记录。
- **P0 验收单（已落地对照）**：[`docs/harness/HARNESS_V2_P0_ACCEPTANCE.md`](docs/harness/HARNESS_V2_P0_ACCEPTANCE.md) — 用于归档或 PR 说明的人工勾选与 GitHub Actions 说明。
- **目录索引**：[`docs/harness/README.md`](docs/harness/README.md) — 规划与测评文档一览。
- **基线测评（含 P0 后对照 §8）**：[`docs/harness/Harness工程测评-Desktop-Projects-ai-ink.md`](docs/harness/Harness工程测评-Desktop-Projects-ai-ink.md)。
- **任务单**：**§2.3** 已增加与 Harness 对齐的推荐字段；各仓 `content/tasks/README.md` / `docs/tasks/README.md` 已链至规划 **§5**。
- **合并前必绿（Ink 前后端，PR 至 `main` / `production`）**：
  - 前端仓：`pnpm install --frozen-lockfile` → `pnpm lint` → `pnpm test` → `pnpm build`（与 `ai-ink-brain/.github/workflows/quality.yml` 中 workflow 名 **`quality`**、job **`lint-and-build`** 一致；单测命令为 **`pnpm test`**，CI 日志中对应 step 名为 **Test**）。
  - 后端仓：`pytest tests -m "not intent_eval and not intent_benchmark"`（与 `ai-ink-brain-api-python/.github/workflows/pytest.yml` 一致）；图谱与跨仓契约仍以既有 `tech-graph*.yml` 为准。
