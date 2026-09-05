---
name: shougong
description: 收工同步助手。当用户说「收工」、「结束了」、「准备换电脑」、「该同步的同步」、「先到这里」、「打包」、「保存」、「下班」、「good night」等任何要结束工作并进行同步的请求时，请一定要使用此技能。本技能会智能更新 vault 根的 DASHBOARD.md、git commit + push GitHub。专为 ai-project2026 vault 设计。
---

# 收工同步助手（ai-project2026 专用）

对话结束前，把今天的工作完整保存：
- **DASHBOARD.md**：智能更新「上次做到哪」+「最近更动纪录」
- **GitHub**：commit + push 本 repo 变动
- **本地 vault**：不需要额外操作（vault 就是本地）

## 收工 SOP（依序执行）

### 步骤 1：盘点今天做了什幺
从对话历史摘要：
- 完成的档案（新建 / 修改 / 删除）
- 关键决策（选了哪个方案、否了哪个方向）
- 踩到的新坑
- 学到的关键概念

### 步骤 2：判断是否值得收工
**先问自己：今天有实质进度吗？**
- ❌ **没有**（只是问问题 / 闲聊 / 探索没动手）→ 跳过 SOP，告诉用户「今天没动档案，不跑收工。需要时再说」
- ✅ **有**（新建/修改/删除了档案，或有重大决策要记录）→ 继续

### 步骤 3：确认工作目录
- 当前目录必须是 `ai-project2026` vault 根
- 否则提醒「请先 cd 到 vault 根」

### 步骤 4：更新 DASHBOARD.md
读现有 DASHBOARD.md，更新以下几段：

#### 4a. 更新 frontmatter 字段
```yaml
---
title: ai-project2026 进度仪表盘
date: <今天日期>
last_updated: <今天日期>
last_action: <一句话总结今天动作>
wip: <还在进行中的任务，最多 3 项>
next_step:
  - <下一步 1>
  - <下一步 2>
graph-excluded: true
---
```

#### 4b. 更新「⏯️ 上次做到哪」段
把今天做的最关键 2-3 件事列出来，每件一句：
```
## ⏯️ 上次做到哪

- ✅ <完成项 1>（<一句话细节>）
- ✅ <完成项 2>
- 🚧 <还在做的项目>（<当前状态>）
```

#### 4c. 更新「🗓️ 最近更动纪录」表格
表格追加一行：
```
| <今天日期> | <一句话摘要> | <动到的档案数> |
```

#### 4d. 更新「🕳️ 踩坑笔记」（若有新坑）
按主题分类追加：
```
- [<主题>] <坑 + 解法>（YYYY-MM-DD）
```

### 步骤 5：Git commit + push
```bash
cd "<vault 根>"
# 本 vault 不是 GDrive，不需要 appendAtomically 设置
git add DASHBOARD.md <今天动到的档案>
# ⚠️ 不要 add .claude/（除非本 vault 需要提交 skill）
# ⚠️ 不要 add .obsidian/workspace（本地状态）
git status --short
git commit -m "<今天工作摘要>"
git push origin main
```

**commit message 写法**：
- 标题行：「动词 + 对象」（例：`完成 TS Lesson 0002 + 更新 dashboard`）
- 正文：3-5 条 bullet 描述变动 + 为什幺（例：`* 简化类型推导讲解，加 Java var 对比\n* 加 5 道 quiz\n* DASHBOARD 状态推进到 0002`）

**禁止**：
- ❌ `git add -A` 或 `git add .`（避免误提交 .claude/、.obsidian/workspace）
- ❌ `git add .claude/`（除非用户明确说要提交 skill）

### 步骤 6：报告同步状态
给用户一个三勾表格：

| 平台 | 动到的档案 | 状态 |
|------|----------|------|
| 本地 vault | <档案列表> | ✅ |
| DASHBOARD | 更新进度 + 更动纪录 | ✅ |
| GitHub | commit + push | ✅ |

## DASHBOARD.md frontmatter 模板

首次初始化时使用：
```yaml
---
title: ai-project2026 进度仪表盘
date: <今天>
last_updated: <今天>
last_action: 初始化 DASHBOARD + 安装 /开工 /收工 skills
wip: []
next_step:
  - 跟 EP10 视频做 TS Lesson 0002
graph-excluded: true
---
```

## 不该做的事

- ❌ 对「没实质进度」的对话也跑同步（浪费 commit 噪音）
- ❌ 把 `.claude/settings.local.json`、`.obsidian/workspace` commit 进去
- ❌ commit message 写「更新」、「修改」这种没资讯的字
- ❌ 主动 `git push` 到非 main 分支（除非用户明示）
- ❌ 跨 vault 操作（不要去动父 vault `E:\my-know\`）
- ❌ 在 DASHBOARD 用中文文件名（slug 一律英文 kebab-case）
- ❌ commit 时遗漏 DASHBOARD 更新（commit 和 DASHBOARD 永远成对）

## 与 /开工 skill 的对偶关系

| 面向 | `/收工` | `/开工` |
|------|--------|--------|
| 主要动作 | 摘要今天做什幺 | 摘要上次做什幺 |
| DASHBOARD | **写入** | **读出** |
| Git | `add` + `commit` + `push` | `status` + `fetch`（不 pull） |
| 何时触发 | 结束对话前 | 新对话开头 |
| 对外副作用 | 推 GitHub、改 DASHBOARD | **无**（只读、只报告） |

## 安全提醒

- ⚠️ `.claude/settings.local.json` 可能含 permissions + token（不要 commit）
- ⚠️ `.obsidian/workspace.json` 是本地 UI 状态（不要 commit）
- ⚠️ 已在 `.gitignore` 保护这两类文件

## Skill 安装位置说明

本 skill 安装在 `<vault>/.claude/skills/shougong/SKILL.md`，**只在本 vault 生效**。
若需要 commit skill 到 git（让另一台电脑能 clone 后直接用），明示告诉 Claude：
> 「请把 .claude/skills/ 也 commit 进去」

否则默认不提交（保持本机本地状态）。

## 进阶：手动触发收工

若重启 Claude Code 后 skill 没自动触发，可以对 Claude 说：
> 「请按 `.claude/skills/shougong/SKILL.md` 的 SOP 帮我收工」

## 跨电脑工作流

| 场景 | 操作 |
|------|------|
| 换电脑后第一次开工 | `git clone https://github.com/hujun711/ai-project2026` → `cd` → 把 `.claude/skills/` 内容补回去 |
| 临时换电脑但没装 skill | 对 Claude 说「读 DASHBOARD.md，告诉我进度」（不依赖 skill 也能开工） |
| 想让 skill 跨电脑生效 | 把 `.claude/skills/` 也 push 到 GitHub（明示告诉 Claude） |
