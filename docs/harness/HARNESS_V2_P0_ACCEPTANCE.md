# Harness V2 · P0（Verify）验收单

> **用途**：记录已落地改动与 **人工/流程验收** 勾选项，便于归档或 PR 说明引用。  
> **范围**：Ink 全栈 **P0 = PR 上默认质量门**（前端 lint+build、后端 pytest）；不含 P1 前端单测扩面等后续项。  
> **真值**：实现以各子仓 `.github/workflows/*.yml` 与代码为准；本单为验收视图。

---

## 1. 交付摘要

| 子项 | 说明 |
|------|------|
| **前端 CI** | `ai-ink-brain/.github/workflows/quality.yml`，workflow 名 **`quality`**：`pnpm install --frozen-lockfile` → `pnpm lint` → `pnpm build`；触发分支 **`main`**、**`production`**；`pull_request` 与 `push`。 |
| **后端 CI** | `ai-ink-brain-api-python/.github/workflows/pytest.yml`，workflow 名 **`pytest`**：`pytest tests -m "not intent_eval and not intent_benchmark"`；同上触发；CI `env` 为 dummy Key + 澄清/意图评测闸关闭，与 `tests/conftest.py` 意图一致。 |
| **规划与索引** | `docs/harness/HARNESS_V2_PLAN.md`（§4 P0 已标为已实现）、`docs/harness/README.md`、根 `AGENTS.md` §8。 |
| **测评对照** | `docs/harness/Harness工程测评-Desktop-Projects-ai-ink.md` **§8**、§7 附录表已增上述 workflow 路径。 |
| **任务单规范** | `ai-ink-brain/content/tasks/README.md`、`ai-ink-brain-api-python/docs/tasks/README.md` 已链 **`HARNESS_V2_PLAN.md` §5**（`test_strategy` / `failure_paths` 等）。 |

---

## 2. 代码与测试变更（验收引用）

| 路径（相对 `Projects/`） | 变更要点 |
|--------------------------|----------|
| `ai-ink-brain-api-python/api/unified_chat.py` | `_sse_emit_queue_maxsize()` 下限由 `8` 改为 `1`，与「单测可调低队列」注释一致。 |
| `ai-ink-brain-api-python/tests/test_unified_chat_sse_incremental_vnext.py` | `test_sse_incremental_queue_backpressure_emits_truncated`：`run` mock 增加 `plan_execution_token`；SSE 以 `iter_bytes()` 读完全流再断言。 |

---

## 3. 本地等价验收命令（与 CI 对齐）

**前端**（在 `ai-ink-brain/` 根目录；无 TTY 时需 `CI=true`，与 pnpm 在 CI 中的行为一致）：

```bash
CI=true pnpm install --frozen-lockfile && pnpm lint && pnpm build
```

**后端**（在 `ai-ink-brain-api-python/` 根目录）：须先导出与 **`.github/workflows/pytest.yml` `jobs.pytest.env`** 同名变量（尤其是 **`CHATBI_V3_LOW_CONFIDENCE_CLARIFY=false`**），否则本地会走「澄清短路」而 CI 不会，易出现用例误失败。

```bash
export CHATBI_V2_INTENT_EVAL=false
export CHATBI_V2_INTENT_BENCH_RUN=false
export CHATBI_V2_INTENT_LLM=false
export CHATBI_V3_LOW_CONFIDENCE_CLARIFY=false
export CHATBI_PYTEST_KEEP_INTENT_ENV=0
export SILICONFLOW_API_KEY=sf-dummy-ci
export OPENAI_API_KEY=
export NEXT_PUBLIC_SUPABASE_URL=http://supabase.test
export SUPABASE_SERVICE_ROLE_KEY=service-role-dummy
export NEXT_PUBLIC_ADMIN_SECRET=secret-token-1234567890
export API_KEY=api-key-123
export TEXT2SQL_DATABASE_URL=postgresql://u:p@localhost:5432/postgres

pip install -r requirements.txt
pytest tests -m "not intent_eval and not intent_benchmark" -q --tb=short
```

---

## 4. GitHub 侧验收（人工勾选）

- [ ] 两子仓已 **push** 含上述 workflow 的提交到远端，且默认使用分支名与 `on.branches` 中 **`main` / `production`** 一致（若团队仅用 `master` 等，须改 workflow 或增加分支名）。
- [ ] 组织/仓库 **Settings → Actions** 未禁用（私有仓常见「需管理员开启」）。
- [ ] 在 **Actions** 页可看到 **`quality`**（前端仓）、**`pytest`**（后端仓）在 **PR** 与/或 **push** 上执行记录，且最近一条为 **绿色**（或与失败原因已登记、已修复）。
- [ ] **分支保护规则**（若启用）：将上述 workflow 设为 **Required status checks**（可选，属流程加固）。

---

## 5. 与 GitHub Actions 的关系（常见问题）

**前端 CI 是否还要单独「配置 GitHub 的 Action」？**

- **不必在网页上重复创建同名流水线**：仓库内已有 **`ai-ink-brain/.github/workflows/quality.yml`**，即 **GitHub Actions** 定义；合并到远端后由 GitHub 自动识别并运行。
- **仍需满足**：远端启用 Actions、分支名匹配、依赖可从公网安装（`pnpm`/`npm` 注册表；若组织要求 Artifactory，再在 workflow 里加 registry 配置）。
- **与 Vercel 等的关系**：部署平台的 build **不替代** PR 上的 **lint/build 门禁**；合并背压建议以 **本仓库 Actions 绿灯** 为准（见 `HARNESS_V2_PLAN.md` P1 可继续扩 checklist）。

---

## 6. 验收结论（填写区）

| 项 | 内容 |
|----|------|
| **验收日期** | 2026-05-13 |
| **验收人** | （本地） |
| **前端 `quality` 最近一次** | **本地等价**：`CI=true pnpm install --frozen-lockfile && pnpm lint && pnpm build` 已通过（`pnpm lint` 含 1 条既有 `react-hooks/exhaustive-deps` warning，非 error）。GitHub Actions 上请以 **`quality`** workflow 最新绿色 run 为准并补链。 |
| **后端 `pytest` 最近一次** | **本地等价**：对上表 `export` 后 `pytest tests -m "not intent_eval and not intent_benchmark"` **114 passed**。GitHub Actions 上请以 **`pytest`** workflow 最新绿色 run 为准并补链。 |
| **备注** | GitHub 侧：仓库 **Settings → Actions** 需启用；workflow 已随各子仓 `.github/workflows/*.yml` 落盘，无需在网页重复「创建」同名流水线。第 4 节勾选请在远端确认后人工更新。 |

---

## 7. 修订记录

| 日期 | 摘要 |
|------|------|
| 2026-05-13 | 初版：P0 落地验收单，与 `HARNESS_V2_PLAN.md`、测评 §8 一致 |
| 2026-05-13 | 第 3 节：对齐 `pytest.yml` 全量 `env`；补充 `CI=true`；第 6 节记录本地等价验收通过 |

---

## 给 Cursor 的稳定关键词

`Harness`、`P0`、`验收`、`quality`、`pytest`、`GitHub Actions`、`Verify`
