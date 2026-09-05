# CLAUDE.md

This file provides guidance to Claude Code when working with this vault.

## Vault 性质

`ai-project2026/` 是一个 **Obsidian vault + Git 仓库** 的混合体，作为 AI 项目学习与实战第二大脑使用。它和父 vault（`E:\my-know\`）并存：

- **父 vault**（`my-know/`）：系统化知识库，三层架构 `raw/` (人类只读) + `wiki/` (LLM 控制) + `outputs/` (衍生报告)
- **本 vault**（`ai-project2026/`）：轻量项目日志 + 学习记录，无三层结构

不要把父 vault 的 INGEST / QUERY / REFLECT 等重型流程套到本 vault。

## vault 结构

| 目录 | 用途 | 写入规则 |
|------|------|---------|
| `教学素材/` | 课程、教材、灵感来源 | Pi 自由读写 |
| `视频笔记/` | 视频/讲座/播客笔记 | Pi 自由读写 |
| `每日笔记/` | 每日学习/开发 log | Pi 自由读写 |
| `lessons/` | TS / Next.js 等课程 HTML 课件 | Pi 自由读写 |
| `learning-records/` | 每课反馈、zone of proximal development | Pi 自由读写 |
| `reference/` | 速查表、参考资料 | Pi 自由读写 |
| `projects/` | vibe coding 实战项目源码 | Pi 自由读写 |
| `Templates/` | 笔记模板 | **只读，禁止修改** |
| `images/` | Obsidian 附件 | Pi 自由读写 |
| `.obsidian/` | Obsidian 应用配置 | 仅提交非用户特定配置（app.json / appearance.json / core-plugins.json） |
| `.claude/skills/` | 项目专用 skill（已 commit） | Pi 自由读写 |
| `.claude/settings.local.json` 等 | Claude Code 本地状态 | **已 gitignore，不要 commit** |
| `AGENTS.md` | Pi 工作规则 | graph-excluded |
| `CLAUDE.md` | 本文件 | graph-excluded |
| `DASHBOARD.md` | 进度仪表盘（驾驶舱） | graph-excluded，由 `/收工` 自动维护 |

## 🔧 工作流 skills（本 vault 专用）

`ai-project2026` 有两个内置 skill，**只在本 vault 生效**：

| 触发词 | Skill | 作用 |
|--------|-------|------|
| 「开工」「开始」「我来了」「上次做到哪」「继续」「resume」 | `kaigong`（/开工） | 读 `DASHBOARD.md` + 检查 git 状态 + 建议下一步 |
| 「收工」「结束」「下班」「保存」「打包」「good night」 | `shougong`（/收工） | 更新 `DASHBOARD.md` + git commit + push |

### /开工 流程（5 步）

1. 判断工作目录（在 vault 根 + git repo）
2. 读 `DASHBOARD.md`（摘要，不全文倒出来）
3. 检查本地 git 状态
4. 检查远端（30 分钟内 fetch 过就跳过；落后 N 个 commit 时**不主动 pull**，提醒用户）
5. 给出结构化摘要 + 建议下一步，等用户选方向

### /收工 流程（5 步）

1. 盘点今天做了什么（从对话历史摘要）
2. **先判断**：今天有实质进度吗？没有就跳过，避免 commit 噪音
3. 更新 `DASHBOARD.md`（frontmatter + 「上次做到哪」+ 「最近更动纪录」表 + 「踩坑笔记」）
4. `git add` 具体档案 + `git commit` + `git push origin main`（**不用** `git add -A`，避免误提交 `.claude/settings.local.json`）
5. 报告三勾同步状态

### 使用示例

```
你：开工
Pi：（自动读 DASHBOARD、查 git、给摘要 + 建议下一步）

你：今天学了 TS Lesson 0002，Demo 跑通了，Quiz 错了一道
Pi：（自动更新 DASHBOARD、commit + push、给三勾表）

你：收工
Pi：（完成上面那一切）
```

### 不依赖 skill 的备用

换电脑或 skill 没载入时，可手动触发：
- 「读 `DASHBOARD.md`，告诉我进度」
- 「请按 `.claude/skills/shougong/SKILL.md` 的 SOP 帮我收工」

### 跨电脑

- `git clone https://github.com/hujun711/ai-project2026` 后，`.claude/skills/` 已包含在 repo 里
- 但 `.claude/settings.local.json` 是 gitignore 的，需在本机重新跑一次 `claude` 配权限

## 常用命令

```bash
# 切到本 vault
cd "E:/my-know/ai-project2026"

# 查看 git 状态
git status

# 提交变更（/收工 skill 会自动做）
git add <具体档案，不要 add -A>
git commit -m "<动词 + 对象>"
git push

# 推送到 GitHub（hujun711）
git push

# 拉取远端
git pull

# 拉取 GitHub 状态
gh repo view
```

## GitHub 仓库

- 远端：`https://github.com/hujun711/ai-project2026`
- 拥有者：`hujun711`（gh CLI 当前活跃账号）
- 可见性：public
- 本仓库内 git user 设为 `hujun711`（**仅本仓库 local config**，不动全局）

## 笔记规范

参考 `AGENTS.md` 的「笔记规范」一节。核心要点：

- 文件名用英文 kebab-case（`vibe-coding-intro.md`，**禁止** `VibeCoding.md` 或 `vibe_coding.md`）
- 中文写入正文，英文术语首次出现括号标注
- frontmatter 必填 `title` / `date` / `tags`
- 系统文件加 `graph-excluded: true`，避免污染图谱

## 何时不应在本 vault 工作

- **查询系统性知识** → 回到父 vault `my-know/` 走 QUERY 流程
- **摄入外部文章** → 父 vault 的 INGEST 流程（带 SHA-256 去重 + concept 对齐）
- **综合分析 / gap report** → 父 vault 的 REFLECT 流程

本 vault 适合：项目实战记录、每日学习 log、视频/课程笔记、个人创作草稿、TS 课程学习。
