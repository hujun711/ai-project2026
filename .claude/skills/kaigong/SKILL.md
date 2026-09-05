---
name: kaigong
description: 开工接续助手。当用户说「开工」、「开始工作」、「我来了」、「上次做到哪」、「我们继续」、「接下来呢」、「接续工作」、「来吧」、「resume」、「continue」等任何要接续上次工作的请求时，请一定要使用此技能。本技能会读取 vault 根的 DASHBOARD.md、回报上次进度、检查 git 状态（含远端 fetch）、建议下一步该做什幺。专为 ai-project2026 vault 设计。
---

# 开工接续助手（ai-project2026 专用）

新对话开始时，帮用户快速进入「上次做到哪」的脉络，避免从零开始解释。

## 内核原则

1. **不主动 git pull**（避免覆盖用户本地未 commit 变动，只提醒「要不要 pull」）
2. **30 分钟内 fetch 过就跳过**（避免单台多对话冗余）
3. **若 DASHBOARD.md 不存在就回报 + 询问**，不乱建档
4. **跟 `/收工` skill 是「对偶」关系**：收工存进去、开工读出来

## 开工 SOP（依序执行）

### 步骤 1：判断工作目录
- 从 `$PWD` 取得当前目录
- 确认是 ai-project2026 vault（路径包含 `ai-project2026`）—— 否则提醒「请先 cd 到 vault 根目录」
- 确认是 git repo（`.git` 目录存在）—— 否则提醒
- 满足条件 → 记下 `REPO_NAME=ai-project2026`

### 步骤 2：读取 DASHBOARD.md
- 路径：`./DASHBOARD.md`（vault 根）
- 若不存在 → 提醒「建议先用懒人包 #07 初始化建 DASHBOARD」+ 仍继续做 git 检查
- 读取并解析 frontmatter 中的结构化字段（last_action / next_step / wip）

### 步骤 3：摘要「上次做到哪」
从 DASHBOARD 读（精简版、不要全文倒出来）：
- 「⏯️ 上次做到哪」段（frontmatter 的 last_action + WIP）
- 「➡️ 下一步」段（frontmatter 的 next_step 列表）
- 「🕳️ 踩坑笔记」最近一笔（只在跟下一步直接相关时提）

### 步骤 4：检查本地 git 状态
```bash
git status --short
```
- clean → 「本地工作区干净」
- 有未 commit 变动 → 列出，提醒「要继续还是放弃？」

### 步骤 5：检查远端（30 分钟判断）
```bash
[ -n "$(find .git/FETCH_HEAD -mmin -30 2>/dev/null)" ] || git fetch origin 2>/dev/null
BEHIND=$(git rev-list HEAD..origin/HEAD --count 2>/dev/null || echo 0)
```
- BEHIND > 0 → 提醒「远端有 N 个新 commit，要 git pull 吗？」**不主动 pull**
- BEHIND = 0 → 「本地是最新状态」

### 步骤 6：扫描 vault 目录状态（轻量）
只检查**已知目录**的存在性 + 最新变动：
```bash
ls -lt lessons/ 每日笔记/ 视频笔记/ 教学素材/ learning-records/ 2>/dev/null | head -20
```
列出最近改动的 5 个文件，让用户一眼看到最近动过什幺。

### 步骤 7：报告 + 建议下一步
给结构化摘要：
```
📂 专案：ai-project2026
📊 Mission：[[MISSION]] / [[CURRICULUM]]
📘 上次做到哪：<从 DASHBOARD 摘要 1-2 句>
🔧 本地 git：<clean / 有 N 个未 commit 变动>
🌐 远端：<最新 / 落后 N commits，建议 git pull>
📁 最近改动的档案：<最多列 5 个>
➡️ 建议下一步：
   1. <从 DASHBOARD「下一步」段第 1 项，或推断>
   2. <可选：第 2 项>

要从哪个方向开始？
```
等用户选方向，不要自己擅自继续。

## 不该做的事

- ❌ 主动 `git pull`（会撞用户本地未 commit 变动）
- ❌ 主动修改 DASHBOARD.md（那是 `/收工` 的事）
- ❌ 在没有 DASHBOARD 时硬建一个（先问用户）
- ❌ 把 DASHBOARD 内容**全文倒出来**（要摘要、保持精简）
- ❌ 触发父 vault（`E:\my-know\`）的 INGEST / QUERY / REFLECT 流程（本 vault 不走）
- ❌ 引用系统文件 wikilink（`[[log]]` `[[index]]` `[[QUESTIONS]]`）

## 与 /收工 skill 的对偶关系

| 面向 | `/收工` | `/开工` |
|------|--------|--------|
| 主要动作 | 摘要今天做什幺 | 摘要上次做什幺 |
| DASHBOARD | **写入** | **读出** |
| Git | `add` + `commit` + `push` | `status` + `fetch`（不 pull） |
| 何时触发 | 结束对话前 | 新对话开头 |
| 对外副作用 | 推 GitHub、改 DASHBOARD | **无**（只读、只报告） |

**设计原则**：开工是「读」、收工是「写」。永不重叠、不冲突。

## 本 vault 速查

| 想做什幺 | 走哪条路 |
|---------|---------|
| 记录今天学习 | `每日笔记/YYYY-MM-DD.md`（模板：`Templates/每日笔记模板.md`） |
| 整理视频课笔记 | `视频笔记/<slug>.md`（模板：`Templates/视频笔记模板.md`） |
| 存教学素材 | `教学素材/<slug>.md`（模板：`Templates/教学素材模板.md`） |
| 跟踪 TS 学习进度 | 更新 `CURRICULUM.md` 状态列 + `learning-records/<lesson>.md` |
| 系统性知识查询 | 回父 vault `E:\my-know\` 走 QUERY |
| 新建项目源码 | `projects/<name>/`（不在 vault 根乱堆） |
| 收尾 | 对 Claude 说「**收工**」 |

## Skill 安装位置说明

本 skill 安装在 `<vault>/.claude/skills/kaigong/SKILL.md`，**只在本 vault 生效**。
若换电脑或换 vault，需要：
- 重新放置本文件
- 或在全局 `~/.claude/skills/kaigong/SKILL.md` 同步一份（修改路径提示）
