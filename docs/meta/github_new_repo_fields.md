# GitHub 新建仓库：可复制字段（cyning-ink-workspace）

> 创建远程后，在本地工作区根执行：`git remote add origin <HTTPS 或 SSH URL>`，再 `git push -u origin main`（分支名以你本地为准）。

---

## Repository name（仓库名）

```text
cyning-ink-workspace
```

---

## Description（简介，≤350 字符）

**英文（推荐，GitHub 展示通用）**：

```text
Aggregator & harness for AI Ink multi-repo dev: AGENTS routing, Harness V2 docs, Cursor workspace rules. Does not include ai-ink-brain / ai-ink-brain-api-python source—clone those repos alongside this root.
```

**中文（可选第二语言/备注）**：

```text
AI Ink 多仓聚合根：总调度 AGENTS、Harness V2 文档与 Cursor 工作区规则；不含前后端源码，需与 ai-ink-brain、ai-ink-brain-api-python 并列克隆。
```

---

## Website（可选）

留空；或填个人主页、文档站等完整 `https://...` URL。

---

## Topics（标签，在仓库页面逐个添加）

建议每条单独添加（GitHub UI 为标签列表，非逗号分隔一行）：

- `ai-ink`
- `harness`
- `monorepo-tooling`
- `documentation`
- `cursor`
- `developer-workflow`

---

## 创建向导中的选项

| 选项 | 建议 |
|------|------|
| **Public / Private** | 含 `AGENTS` 与规则时多为 **Private**；若仅公开 Harness 文档可再评估 |
| **Add a README** | **不要勾选**（本地已有根 [`README.md`](../../README.md)），避免与首次 push 冲突 |
| **Add .gitignore** | **不要选模板**（本地已有根 `.gitignore`） |
| **Choose a license** | 任选或跳过；本根仓以文档为主 |

---

## 首 push 后自检

```bash
git remote -v
git status
git push -u origin main
```

（若默认分支为 `master` 或其他名称，替换最后一行。）

---

## 给 Cursor

`cyning-ink-workspace`、`GitHub`、`Description`、`Topics`、`git remote`
