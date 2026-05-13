# docs/harness/tasks（工作区 Harness 任务）

> **用途**：承载 **跨子仓**、**流程 / CI / 帽子 / 验收单** 等与 `docs/harness/` 强相关的任务单；**不替代**各业务仓内任务（前端 `ai-ink-brain/content/tasks/`、后端 `ai-ink-brain-api-python/docs/tasks/` 等）。  
> **真值**：命名与归档规则以 **本 README** 为准；字段约定见 `../HARNESS_V2_PLAN.md` **§5**。

---

## 目录结构（对齐前后端「active / done / _views」习惯）

```
docs/harness/tasks/
  README.md           # 本文件
  active/             # 进行中 / 待开始
  done/               # 已验收归档
  _views/             # 聚合索引（只链路径，非真值）
    done.md
    in_progress.md
    design.md           # draft / 缺状态（可选）
```

---

## 与前后端任务目录的分工

| 任务类型 | 落盘目录 |
|----------|----------|
| **工作区 Harness**（多子仓调度、CI 门禁对齐、帽子 prompts、根 `AGENTS` / `docs/harness` 规划与验收） | **`docs/harness/tasks/active|done`**（本目录） |
| **前端业务功能**（页面、BFF、Next 等） | `ai-ink-brain/content/tasks/`（见该仓 `README.md`） |
| **后端业务功能**（API、RAG、Text2SQL 等） | `ai-ink-brain-api-python/docs/tasks/`（见该仓 `README.md`） |

若任务 **同时** 改工作区文档与某一子仓代码：任务单仍放在 **业务主交付仓** 或 **本目录** 二选一，正文须写清 **双仓 PR 顺序**；避免两份任务单漂移。

---

## 新增任务如何落盘

- **新建位置**：一律放在 `docs/harness/tasks/active/`
- **命名**：`task_<domain>_<topic>_vN.md`（与前后端 `task_*` 风格一致）
- **必须字段**：头部含 `> **状态**：...`（`draft` / `pending` / `in_progress` / `done` / `done（YYYY-MM-DD 验收通过）`）

---

## 归档流程（验收后必做）

1. 核对「验收标准」已全部勾选或已书面签核。  
2. 将头部 `状态` 改为 `done（YYYY-MM-DD 验收通过）`。  
3. 在工作区根执行：  
   `git mv docs/harness/tasks/active/<文件名>.md docs/harness/tasks/done/`  
4. 在 `_views/done.md` 追加指向 `../done/<文件名>.md` 的相对链接。  
5. 若曾列入 `_views/in_progress.md`，同步移除或更新。

**硬规则**：禁止仅改头部为 `done` 而文件仍留在 `active/`（与前后端任务目录规则一致）。

---

## 视图索引维护规则（最小集）

- `_views/design.md`：`draft` / 缺状态字段清单（按需）
- `_views/in_progress.md`：`in_progress` / `pending` 等推进中任务
- `_views/done.md`：已完成任务链接

---

## 给 Cursor

`Harness`、`docs/harness/tasks`、`active`、`done`、`_views`、`验收`、`HARNESS_V2_PLAN` §5
