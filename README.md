# cyning-ink-workspace

> **定位**：Cyning 的 **AI Ink 多子仓研发聚合根**（Git 根仓库）。承载 **总调度**（[`AGENTS.md`](AGENTS.md)）、**Harness V2**（[`docs/harness/`](docs/harness/README.md)）、工作区 **Cursor 规则**等；**不包含** `ai-ink-brain`、`ai-ink-brain-api-python` 等业务源码树（二者为 **独立远程仓库**，需单独克隆到本目录下，见下文）。

---

## 与本工作区配套的子仓（需单独 clone）

| 目录名 | 说明 |
|--------|------|
| `ai-ink-brain/` | Next.js 博客 + BFF（独立 Git 仓库） |
| `ai-ink-brain-api-python/` | FastAPI RAG / ChatBI 等（独立 Git 仓库） |
| `Snail/py-Snail/`、`Python-learning/`、`secondCar/` | 其余子目录见 [`AGENTS.md`](AGENTS.md) §1；均为本机聚合，**默认不在本根仓内提交**（根 `.gitignore` 已排除）。 |

---

## 推荐本地布局（首次）

```bash
# 1. 克隆本工作区（远程创建后替换 URL）
git clone <YOUR_CYNING_INK_WORKSPACE_REPO_URL> cyning-ink-workspace
cd cyning-ink-workspace

# 2. 在同级路径下克隆业务仓（目录名须与 AGENTS.md 一致）
git clone <YOUR_AI_INK_BRAIN_REPO_URL> ai-ink-brain
git clone <YOUR_AI_INK_BRAIN_API_PYTHON_REPO_URL> ai-ink-brain-api-python
```

说明：本机文件夹仍名为 `Projects` 亦可；**`cyning-ink-workspace`** 为对外仓库名与推荐克隆目录名，便于与泛称「Projects」区分。

---

## 文档入口

| 路径 | 内容 |
|------|------|
| [`AGENTS.md`](AGENTS.md) | 总调度、子仓索引、任务落盘规则 |
| [`docs/harness/README.md`](docs/harness/README.md) | Harness 规划、验收、任务目录、prompts 索引 |
| [`docs/meta/github_new_repo_fields.md`](docs/meta/github_new_repo_fields.md) | 新建 GitHub 远程时的 **Description / Topics** 等可复制字段 |

---

## 在 GitHub 上创建远程仓库

**可复制字段（仓库名、Description、Topics、向导选项）** 已集中在：

**[`docs/meta/github_new_repo_fields.md`](docs/meta/github_new_repo_fields.md)**

---

## 给 Cursor

`cyning-ink-workspace`、`Harness`、`docs/harness`、`AGENTS.md`、`多子仓`、`clone`
