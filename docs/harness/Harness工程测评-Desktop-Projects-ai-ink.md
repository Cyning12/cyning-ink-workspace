# Harness 工程建设测评报告

**评测范围**：`/Users/cyning/Desktop/Projects` 内与 Ink-Brain 全栈相关的前后端仓库（**不含** `Snail/`、`Python-learning/`）。  
**评测对象**：

| 仓库 | 角色 |
|------|------|
| `ai-ink-brain/` | 前端（Next.js / TS） |
| `ai-ink-brain-api-python/` | 后端（FastAPI / Python） |
| `Projects/AGENTS.md`（工作区根） | 多子仓调度与协作 Harness |

**评测方法**：对照课程中的 Harness 三支柱 **Inform（告知）/ Constrain（约束）/ Verify（验证）**，并结合 **Guides（引导）** 与 **Sensors（传感器）** 是否成体系；**仅阅读仓库现状，未做任何修改**。

**评测日期**：2026-05-11  

---

## 1. 总评摘要

| 维度 | 前端 `ai-ink-brain` | 后端 `ai-ink-brain-api-python` | 说明 |
|------|---------------------|--------------------------------|------|
| **Inform** | **强** | **强** | 各仓 `AGENTS.md`、`docs/meta/PROJECT_CONFIG_*.md`、`docs/_tech_graph/`、任务单目录、工作区总 `AGENTS.md` 形成清晰阅读顺序与真值表，符合「地图而非手册 + 仓库即记录」。 |
| **Constrain** | **中强** | **中强** | ESLint（Next core-web-vitals + TS）、`tsconfig strict`、`/.cursor/rules/*.mdc`；后端规则 + 技术图谱 manifest / 跨仓契约脚本，约束可机械校验部分已超出普通项目。 |
| **Verify** | **偏弱** | **中等（本地强、CI 不全）** | 前端：**未发现**自动化测试脚本与 **PR 合并门禁**（无 `lint`/`build` 的常规 CI）。后端：`tests/` 体量可观且 `conftest.py` 有环境隔离设计，但 **GitHub Actions 中未看到 pytest 流水线**，合并背压主要依赖图谱类检查与契约检查。 |

**一句话**：**「告知 + 架构/契约约束」已达到高 Harness 成熟度；「验证层在 CI 里持续背压」前端缺口大，后端未闭环到默认流水线。**

---

## 2. 前端 `ai-ink-brain`（Next.js）

### 2.1 Inform（告知）

- **`AGENTS.md`**：必读顺序明确（`PROJECT_CONFIG` → `.cursor/rules` → `_tech_graph` → 任务与归档规则），并指向工作区根协作约定，**符合课程中 AGENTS 作为入口地图**。
- **`docs/meta/PROJECT_CONFIG_AI_INK_BRAIN.md`**（由 AGENTS 引用）：承担环境变量与契约摘要，**接近 SDD 真值表**。
- **`docs/_tech_graph/`** + `99_mermaid_protocol`：架构「唯一可信来源」、双轨 `.md` / `.ai.md`，**强于普通 README**。
- **`content/tasks/active|done`**：任务驱动与验收、`git mv` 归档约定，**把流程写进仓库**。

### 2.2 Constrain（约束）

- **`package.json`**：`pnpm lint` → `eslint`；`eslint.config.mjs` 使用 `eslint-config-next`（core-web-vitals + typescript）。
- **`tsconfig.json`**：`"strict": true`，属静态类型约束（开发期与构建期 Guides/Sensors 之间）。
- **`.cursor/rules/`**：多份 `.mdc`（技术图谱、前端架构、UI、可观测性等），**偏向 Guides**，与课程「用信号引导」一致。

### 2.3 Verify（验证）— 主要短板

- **自动化测试**：`package.json` 中**无** `test` / `vitest` / `jest` / `playwright` 等脚本与依赖；仓库内**未见**成体系的单元/E2E 测试目录，**TDD/回归背压在工具链层面缺失**。
- **CI（GitHub Actions）**：仅见 `.github/workflows/rag_ingest_supabase.yml`（定时 / `workflow_dispatch` 的 RAG ingest），**未见** `pull_request` / `push` 上跑 `pnpm lint` 或 `pnpm build` 的质量门。
- **影响**：合并到主干时**无默认机器背压**保证「能构建、能通过 ESLint」；与课程强调的 **CI 三道门 / 背压** 相比，**Verify 层未落地到流水线**。

### 2.4 与课程概念对照

| 课程要点 | 前端现状 |
|----------|----------|
| 仓库即记录 | **满足**（配置、图谱、任务在仓内） |
| AGENTS 地图 | **满足** |
| Lint 机械化 | **本地有**；**CI 未绑 PR** |
| pytest / 分层测试 | **缺失** |
| 背压合并 | **弱**（依赖人为或平台外检查） |

**前端 Harness 成熟度（主观档）**：**Inform / Constrain 高，Verify 低** → 综合约 **B（文档与规范驱动强，机器验证未闭环）**。

---

## 3. 后端 `ai-ink-brain-api-python`（FastAPI）

### 3.1 Inform（告知）

- **`AGENTS.md`**：与前端对称，指向 `PROJECT_CONFIG`、`docs/_tech_graph/`、`docs/tasks/`、归档规则与安全红线，**结构优秀**。
- **`docs/meta/PROJECT_CONFIG_AI_INK_BRAIN_API_PYTHON.md`**、**`docs/spec/`**（如 v3-agent 阶段验收类文档）：**规格与验收可追溯**，贴近 SDD。
- **`docs/tasks/`**、**`docs/diary/`**：任务与过程记录进仓库。

### 3.2 Constrain（约束）

- **`.cursor/rules/`**：RAG、错误处理、图谱更新等 **Guides**。
- **`tools/tech_graph_manifest_check.py`**（CI：`tech-graph.yml`）：对 `_manifest.json`、API/SQL 等做清单级校验，**属于自定义「结构/契约 Linter」**，与课程 `check_report_structure.py` 同类思想。
- **`tools/tech_graph_contract_check.py`**（CI：`tech-graph-contract.yml`）：检出前端仓（固定 `Cyning12/ai-ink-brain`、`ref: production`）与后端一起做**跨仓契约**检查，**Harness 亮点**（前后端 SSE/事件名等不一致会在 CI 暴露）。

### 3.3 Verify（验证）

- **`tests/`**：多个 `test_*.py`，覆盖 unified chat、Text2SQL、ingest、路由、Supabase 重试、Intent 等；**工程上已投入测试资产**。
- **`tests/conftest.py`**：在导入 `api` / dotenv 前固定 Intent 相关环境变量，避免全量 pytest 误触真实 LLM，**符合课程/Hermes 案例中「测试隔离、Key 置空」思路**（实现方式为进程级 env，而非 CI 内统一 `pytest` job）。
- **CI**：存在 **`tech-graph`** 与 **`tech-graph-contract`** 两条 PR/push 工作流；**未发现**在 CI 中执行 `pytest` 的配置文件。
- **影响**：**图谱与跨仓契约**在合并前有背压；**业务回归测试**依赖本地或别处的习惯/手动，**默认合并路径上无 pytest 红灯**。

### 3.4 与课程概念对照

| 课程要点 | 后端现状 |
|----------|----------|
| 自定义结构 Linter | **有**（manifest + contract，且跨仓） |
| 错误信息可带 fix | 图谱脚本以报错列表为主；**未逐条对照**是否长期嵌入「FIX:」式文案（非本次全文审计） |
| pytest 分层 / CI 背压 | **测试存在**；**CI 未纳入 pytest** → 与课程 `quality_gate.yml` 第二道门相比**差一环** |
| API Key 在 CI 置空 | contract / manifest job **未展示** pytest 级 Key 清理；意图相关由 `conftest` 在**测试进程内**缓解 |

**后端 Harness 成熟度（主观档）**：**Inform / Constrain 高，Verify 中**（本地与专项脚本强，**合并门禁未覆盖单测**）→ 综合约 **B+**。

---

## 4. 工作区根 `Projects/AGENTS.md`

- **多子仓调度**、任务落盘路径、图谱优先、`DIARY_GUIDE`、**`_tech_graph` 为统一架构来源**等约定完整，**属于工作区级的 Inform + 流程 Constrain**。
- 与两个 Ink 子仓 **形成互补**：子仓 AGENTS 不重复写全局规则，**符合「渐进式披露」**。

**注意**：表中仍列出 `Snail`、`Python-learning`、`secondCar` 等；**本次评测按要求未展开 Snail 与 Python-learning**。

---

## 5. 改进优先级建议（仅建议，未执行）

以下按 **投入小 / 对 Harness 闭环收益大** 排序，供后续改造参考。

1. **前端 CI（高优先级）**：对 `main`/`production` 的 `pull_request` + `push` 增加 job：`pnpm install --frozen-lockfile` → `pnpm lint` → `pnpm build`（可再分快/慢 job）。  
2. **后端 CI（高优先级）**：在现有 workflow 之后或并行增加 `pytest`（建议 `-m "not slow"` 或显式排除需真实 LLM 的 marker），并在 CI env 中 **unset / 空值** 敏感 Key，与 `conftest` 双保险。  
3. **前端最小 Verify**：至少增加 **Smoke**（如 `next build` 已通过则部分覆盖）或关键 BFF 路由的 **少量单测**（Vitest + MSW），再逐步扩面。  
4. **统一「质量门」文档**：在任一仓 `AGENTS.md` 或工作区 `AGENTS.md` 增加「合并前必绿检查列表」指向上述 CI，与课程 **背压** 叙事对齐。  

---

## 6. 结论表（Harness 三支柱）

| 支柱 | 工作区根 | 前端 | 后端 |
|------|----------|------|------|
| **Inform** | 优 | 优 | 优 |
| **Constrain** | 优（流程+图谱体系） | 良（ESLint + strict TS + rules） | 良–优（rules + manifest + 跨仓 contract） |
| **Verify** | 依赖各仓 CI | **弱**（无 PR 测试/构建门） | **中**（有测试与图谱 CI，**缺 pytest CI**） |

---

## 7. 附录：本次检视的关键路径（便于复核）

| 路径 | 说明 |
|------|------|
| `/Users/cyning/Desktop/Projects/AGENTS.md` | 工作区总调度 |
| `/Users/cyning/Desktop/Projects/ai-ink-brain/AGENTS.md` | 前端 Agent 导航 |
| `/Users/cyning/Desktop/Projects/ai-ink-brain/package.json` | 脚本与依赖（无 test） |
| `/Users/cyning/Desktop/Projects/ai-ink-brain/.github/workflows/rag_ingest_supabase.yml` | 唯一前端 workflow |
| `/Users/cyning/Desktop/Projects/ai-ink-brain-api-python/AGENTS.md` | 后端 Agent 导航 |
| `/Users/cyning/Desktop/Projects/ai-ink-brain-api-python/.github/workflows/tech-graph.yml` | 图谱 manifest CI |
| `/Users/cyning/Desktop/Projects/ai-ink-brain-api-python/.github/workflows/tech-graph-contract.yml` | 跨仓契约 CI |
| `/Users/cyning/Desktop/Projects/ai-ink-brain-api-python/tests/conftest.py` | pytest 环境隔离意图 |
| `/Users/cyning/Desktop/Projects/ai-ink-brain-api-python/tools/tech_graph_manifest_check.py` | 结构/清单类 Linter |
| `ai-ink-brain/.github/workflows/quality.yml` | **P0 后**：PR/push 上 lint + build（相对工作区根） |
| `ai-ink-brain-api-python/.github/workflows/pytest.yml` | **P0 后**：PR/push 上 pytest 门禁 |

---

## 8. 2026-05-13 后续落地（Harness V2 · Verify P0）

> 以下条目为 **P0 前** 正文 §2–§6 之后的增量；以远端 GitHub Actions 实际绿灯为准。

| 变更 | 路径（相对工作区根 `Projects/`） |
|------|----------------------------------|
| 前端 PR/push：`pnpm` install → lint → build | `ai-ink-brain/.github/workflows/quality.yml` |
| 后端 PR/push：`pytest`（排除 `intent_eval` / `intent_benchmark`） | `ai-ink-brain-api-python/.github/workflows/pytest.yml` |
| V2 规划与修订记录 | `docs/harness/HARNESS_V2_PLAN.md` |
| P0 验收单（勾选与 Actions 说明） | `docs/harness/HARNESS_V2_P0_ACCEPTANCE.md` |
| 本目录索引 | `docs/harness/README.md` |
| 工作区 Harness 任务单（`active` / `done`） | `docs/harness/tasks/`（见 `docs/harness/tasks/README.md`） |

**结论表（§6）更新口径**：Ink 前后端 **Verify** 由「弱 / 中」提升为「**PR 上具备默认 pytest / lint+build 背压**」，与 `HARNESS_V2_PLAN.md` **§4 P1**（前端单测、统一 checklist 扩面）仍属后续。

---

*本报告由自动化阅读目录与代表性文件生成；若本地分支名、workflow 与远端不一致，以实际 GitHub 配置为准。*
