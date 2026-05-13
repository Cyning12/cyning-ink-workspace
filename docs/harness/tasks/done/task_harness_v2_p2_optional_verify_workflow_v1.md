# 工作区 Harness Task：Harness V2 P2 — 可选独立 Verification（CI 与流程）（v1）

> **状态**：`done（2026-05-13 验收通过）`  
> **任务落盘**：`docs/harness/tasks/done/`（归档后路径）。  
> **前置**：**P2 项 6** 已完成（[`../done/task_harness_v2_p2_prompts_roles_v1.md`](../done/task_harness_v2_p2_prompts_roles_v1.md)）；前后端已有 **`quality`** / **`pytest`** 全量门禁；本单为 **项 5** 增量。  
> **关联 Harness**：`docs/harness/HARNESS_V2_PLAN.md` **§4 P2 项 5**、**§7**（复检与输入隔离）  
> **关联 Issue/PR**：无  

---

## Harness 元信息

| 字段 | 取值 |
|------|------|
| **test_strategy** | `recommended` |
| **test_strategy_note** | 以新增/调整 **workflow YAML** 为主；合并前须在 PR 上跑通对应 Actions；不要求先写单元测试再写 YAML。 |
| **freeze_id** | （可选）以 `HARNESS_V2_PLAN.md` §10 最新修订为准 |

### failure_paths

| 触发条件 | 系统行为 | 可重试 |
|----------|----------|--------|
| 新增 workflow 与现有 `quality`/`pytest` 重复跑测、耗时翻倍 | 文档中明确 **并行 vs 合并** 策略；必要时用 `paths`/`paths-ignore` 收窄触发 | 调触发条件后重跑 |
| `verify` job 名与分支保护配置不一致 | Required checks 不绿 | 对齐 GitHub Settings 命名 |
| 仅文档无 YAML | 验收须说明「组织暂不启用第二套 job」并保留 **可启用路径** | 后续再开 PR 补 YAML |

---

## 背景与目标

`HARNESS_V2_PLAN.md` **§4 P2 项 5**：**可选独立 Verification job** — 仅跑 **测试 + 静态分析**，与「写代码」Agent 权限在 **组织层面** 可分离（例如：合并前强制通过的 check 与开发者在本地跑的命令一致，但 **workflow 名称/职责** 可与「全量 build/图谱」拆分，便于分支保护 **多条 Required** 或 **CODEOWNERS + 环境** 策略）。

本任务目标：

1. **落盘决策文档**（`docs/harness/` 下新建 `VERIFICATION_CI_PATTERN.md` 或等价文件名）：写清 **与现有 `quality` / `pytest` / `tech-graph*` 的关系**、推荐 **两种落地形态**（**A** 并行轻量 `verify` workflow；**B** 仅在文档中约定「复检 Agent 只贴日志、不触写权限」而不新增 YAML），及 **分支保护** 配置要点（链接 GitHub 官方文档即可，不复制长文）。
2. **（可选实现）** 若选形态 **A**：在 **`ai-ink-brain`** 与 **`ai-ink-brain-api-python`** 各增 **一条** 独立 workflow（建议 workflow 文件名含 `verify`，如 `verify-fast.yml`），**仅**包含：前端 `pnpm test`（或 `lint`+`test` 不含 `build`，须在文档说明取舍）；后端 `pytest`（与现有 `pytest.yml` **相同 marker/env**，避免行为分叉）。**须**在文档中说明与 `quality.yml` / `pytest.yml` **是否同时启用** 及如何避免重复计费。
3. **更新索引**：`docs/harness/README.md`、`HARNESS_V2_PLAN.md` **§4 P2 项 5**（标为「指南已实现」或「已实现 YAML」二选一）、**§10** 修订记录；根 **`AGENTS.md` §8** 若新增 workflow 名则补充「合并前必绿」一句。

---

## 范围

- [x] 新建 **`docs/harness/VERIFICATION_CI_PATTERN.md`**（或任务内拟定并经评审的最终文件名），含：目标、与现有 workflow 对照表、形态 A/B、分支保护建议、**给 Cursor** 关键词。
- [x] 在 **`HARNESS_V2_PLAN.md` §4** 更新 **P2 项 5** 状态句（与实现程度一致）。
- [x] 更新 **`docs/harness/README.md`** 链到该文档。
- [x] **（可选）** 两个子仓各新增 **verify** 类 workflow 文件；若不做 YAML，须在正文章节 **「未启用 YAML 的理由」** 写一句（如：与 `pytest`/`quality` 完全重复）。

## 非范围

- **不**替代现有 **`tech-graph.yml` / `tech-graph-contract.yml`** 契约门禁。  
- **不**引入自托管 Runner 采购与计费谈判（仅文档可提及为远期）。  
- **不**修改 `docs/harness/prompts/` 帽子正文（除非为对齐新增 workflow 名而改一句）。

---

## 依赖与引用

| 依赖 | 路径 |
|------|------|
| 现有 CI | `ai-ink-brain/.github/workflows/quality.yml`、`ai-ink-brain-api-python/.github/workflows/pytest.yml` |
| 合并前必绿真值 | `AGENTS.md` §8、`HARNESS_V2_P0_ACCEPTANCE.md` §3 |
| 复检摘要 | `HARNESS_V2_PLAN.md` §7 |
| 任务规范 | `docs/harness/tasks/README.md` |

---

## 验收标准

- [x] 决策文档可读，且 **明确** 与 `quality`/`pytest` 的边界（不误导为「第二套真值」）。  
- [x] `HARNESS_V2_PLAN.md` §10 有修订记录；§4 项 5 与事实一致。  
- [x] `docs/harness/README.md` 已索引新文档。  
- [x] 若新增 YAML：**PR 上** 新 workflow 有 **至少一次成功运行记录**（或本地 `act` 等价说明写入实现备忘）；**无**与现有 marker/env 不一致的后端 pytest 行为。

---

## 手动测试用例

1. 从 `docs/harness/README.md` 打开新文档，按其中步骤能在 GitHub UI 找到对应 check（若已启用 YAML）。  
2. 未启用 YAML 时：Reviewer 能按文档执行「复检输入裁剪」流程（与 prompts 复检帽一致即可引用链）。

---

## 实现备忘（由执行 Agent 回填）

| 项 | 内容 |
|----|------|
| 新建/修改文件列表 | 新建：`docs/harness/VERIFICATION_CI_PATTERN.md`；`ai-ink-brain/.github/workflows/verify-fast.yml`；`ai-ink-brain-api-python/.github/workflows/verify-fast.yml`。修改：`docs/harness/README.md`、`docs/harness/HARNESS_V2_PLAN.md`（§4 项 5、§8、§10、给 Cursor）、根 `AGENTS.md` §8 |
| 选用形态 A 或 B（或混合） | **混合**：形态 **A**（两子仓 `verify-fast.yml`）+ 文档中形态 **B** 说明；**必绿真值**仍为 `quality` / `pytest`（见 `VERIFICATION_CI_PATTERN` §5）。 |
| GitHub Actions 首绿 | 需在 **合并本变更后的 PR** 于 GitHub Actions 上确认 `verify-fast` workflow 至少一次成功（本环境无法代跑远程 check）。 |
| 本地等价验证 | 前端：`pnpm lint` + `pnpm test` 通过。后端：导出与 `pytest.yml` 相同 `env` 后 `pytest tests -m "not intent_eval and not intent_benchmark"` → **114 passed**（与 CI marker 一致）。 |

---

## 给 Cursor

`Harness`、`Verify`、`verification`、`workflow`、`quality`、`pytest`、`分支保护`、`HARNESS_V2_PLAN` §4 P2、`docs/harness/tasks`
