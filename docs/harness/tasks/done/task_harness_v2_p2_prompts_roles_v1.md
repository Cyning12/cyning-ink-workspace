# 工作区 Harness Task：Harness V2 P2 — 角色帽子 Prompt 落盘（`docs/harness/prompts/`）（v1）

> **状态**：`done（2026-05-13 验收通过）`  
> **任务落盘**：`docs/harness/tasks/done/`（归档后路径）。  
> **前置**：`docs/harness/HARNESS_V2_PLAN.md` **§4 P1** 已落地；P1 任务单见 **[`../done/task_harness_v2_p1_frontend_vitest_quality_gate_v1.md`](../done/task_harness_v2_p1_frontend_vitest_quality_gate_v1.md)**（已归档至 `docs/harness/tasks/done/`）。  
> **关联 Harness**：`docs/harness/HARNESS_V2_PLAN.md` **§4 P2 项 6**、**§3**  
> **关联 Issue/PR**：无  

---

## Harness 元信息

| 字段 | 取值 |
|------|------|
| **test_strategy** | `not_applicable` |
| **test_strategy_note** | 交付物为 Prompt/规范 Markdown，无运行时代码；质量靠 **自检清单 + 人工审阅** 验收。 |
| **freeze_id** | （可选）以 `HARNESS_V2_PLAN.md` §10 最新修订 + 本任务合并日为准 |

### failure_paths

| 触发条件 | 系统行为 | 可重试 | 可见性 |
|----------|----------|--------|--------|
| 帽子内容与 `HARNESS_V2_PLAN.md` §3 矛盾 | Code Review 打回 | 修订后重提 | PR 评论 |
| 路径不在 `docs/harness/prompts/` 约定下 | 索引链接 404 | 修正路径 | `README` 预览 |
| 仅写英文长文、无稳定关键词 | Agent 检索失败 | 按 §「给 Cursor」补关键词 | 复检不通过 |

---

## 背景与目标

P0/P1 已补齐 **Verify**（CI + 最小单测）。`HARNESS_V2_PLAN.md` **§4 P2 项 6** 要求：在 **`docs/harness/prompts/`** 维护 **各角色帽子** 独立 md、版本化，并与 **§3** 硬规则摘要语义等价。

本任务目标：

1. **新建目录** `docs/harness/prompts/`（相对工作区根 `Projects/`）。
2. **至少 4 份**角色文件（可拆可并，以下为建议最小集；若合并为更少文件，须在 `prompts/README.md` 说明映射）：
   - **需求 / 任务分析**（验收可观测、`failure_paths`、非范围、依赖链接）
   - **规格或任务审查**（只输出缺口；契约变更标冻结点升级）
   - **执行编码**（必读路径、`test_strategy` 门闸、拒开工条件）
   - **自检 + 独立复检**（可拆为两份 md；若合并须含两套输入裁剪规则）
3. **每顶帽子** 须含统一骨架段落（与规划 §3 一致）：**身份 → 只做什么 → 禁止什么 → 输入假设 → 输出形状 → 停止条件 → 交接物**；单文件建议 **≤1200 字**（中文为主，专有名词英文），避免单块过长挤占 Agent 上下文。
4. **更新索引**：`docs/harness/README.md` 增加 `prompts/` 入口表；`HARNESS_V2_PLAN.md` **§3** 或 **§8** 增加一行链到 `prompts/README.md`。
5. **（可选）** `AGENTS.md` §8 增加一句「角色帽子见 `docs/harness/prompts/`」。

---

## 范围

- [x] 创建 `docs/harness/prompts/README.md`：文件列表、使用方式（例如：按对话角色复制 system 前缀）、修订记录表。
- [x] 创建上述角色 **Markdown** 文件（命名建议：`10-requirements.md`、`20-review-spec-task.md`、`30-execute-code.md`、`40-self-check-and-reinspect.md` — 可调整，须在 README 中列出）。
- [x] 与 **`HARNESS_V2_PLAN.md` §3** 表格逐条对照，**无遗漏、无矛盾**（有取舍须在 README「与 §3 差异」一节写清）。
- [x] 更新 **`docs/harness/README.md`**。
- [x] 更新 **`HARNESS_V2_PLAN.md`**（§3 或 §8、§10 修订记录至少一处）。

## 非范围

- **不**实现 Cursor Hooks / Skills 自动挂载帽子（另 task）。
- **不**新增 P2 项 5「独立 Verification job」（另 task）。
- **不**修改前后端业务代码与 CI workflow（除非修正文档中的错误链接）。

---

## 依赖与引用

| 依赖 | 路径 |
|------|------|
| 帽子硬规则摘要 | `docs/harness/HARNESS_V2_PLAN.md` §3 |
| P2 条目 | 同上 §4 **P2 项 6** |
| 目录索引 | `docs/harness/README.md` |
| 总入口 | `AGENTS.md` §8 |
| 任务规范 | `docs/harness/tasks/README.md` |

---

## 验收标准

- [x] `docs/harness/prompts/` 下 **README + ≥4 角色文件** 可打开，相对链接在 GitHub / 本地预览均有效。
- [x] `HARNESS_V2_PLAN.md` §3 中每类「硬规则」在 prompts 中有 **可定位** 对应段落（README 中给对照表即可）。
- [x] `docs/harness/README.md` 已链到 `prompts/README.md`。
- [x] `HARNESS_V2_PLAN.md` §10 **修订记录** 追加一行（日期 + 摘要）。
- [x] 全文 **无绝对本机路径**（不写 `/Users/...`）；**给 Cursor** 段含稳定关键词：`Harness`、`prompts`、`帽子`、`拒开工`、`test_strategy`。

---

## 手动测试用例

1. [x] 从 `docs/harness/README.md` 点进 `prompts/README.md`，再进入任一角色文件，确认可读。  
2. [x] 任选一角色 md，复制首段到空白对话作为 system 前缀试跑（可选），确认无自相矛盾指令。  

---

## 实现备忘（由执行 Agent 回填）

| 项 | 内容 |
|----|------|
| 新建/修改文件列表 | 新建：`docs/harness/prompts/README.md`、`10-requirements.md`、`20-review-spec-task.md`、`30-execute-code.md`、`40-self-check.md`、`50-independent-reinspect.md`（自检与复检分文件；复检文件含 **全局验收** 第二节）。修改：`docs/harness/README.md`、`docs/harness/HARNESS_V2_PLAN.md`（§2/§3/§8/§10/给 Cursor）、根 `AGENTS.md` §8 |
| 与 §3 差异（若有） | 无实质规则冲突；README「与 §3 差异」已写为细化为可复制指令 |

---

## 给 Cursor

`Harness`、`P2`、`prompts`、`帽子`、`HARNESS_V2_PLAN` §3、`README`、`修订记录`、`拒开工`、`test_strategy`、`docs/harness/tasks`
