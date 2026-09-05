---
title: 'CLAUDE.md — ai-project2026 vault'
graph-excluded: true
---

# CLAUDE.md

This file provides guidance to Claude Code when working with this vault.

## Vault 性质

`ai-project2026/` 是一个 **Obsidian vault + Git 仓库** 的混合体，作为 AI 项目学习与实战第二大脑使用。它和父 vault（`E:\my-know\`）并存：

- **父 vault**（`my-know/`）：系统化知识库，三层架构 `raw/` (人类只读) + `wiki/` (LLM 控制) + `outputs/` (衍生报告)
- **本 vault**（`ai-project2026/`）：轻量项目日志 + 学习记录，无三层结构

不要把父 vault 的 INGEST / QUERY / REFLECT 等重型流程套到本 vault。

## vault 结构

| 目录 | 用途 | 写入规则 |
|------|------|----------|
| `教学素材/` | 课程、教材、灵感来源 | Pi 自由读写 |
| `视频笔记/` | 视频/讲座/播客笔记 | Pi 自由读写 |
| `每日笔记/` | 每日学习/开发 log | Pi 自由读写 |
| `Templates/` | 笔记模板 | **只读，禁止修改** |
| `images/` | Obsidian 附件 | Pi 自由读写 |
| `.obsidian/` | Obsidian 应用配置 | 仅提交非用户特定配置（app.json / appearance.json / core-plugins.json） |
| `.claude/` | Claude Code 项目配置 | 按需使用 |
| `AGENTS.md` | Pi 工作规则 | graph-excluded |
| `CLAUDE.md` | 本文件 | graph-excluded |

## 常用命令

```bash
# 切到本 vault
cd "E:/my-know/ai-project2026"

# 查看 git 状态
git status

# 提交变更
git add -A && git commit -m "<说明>"

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

本 vault 适合：项目实战记录、每日学习 log、视频/课程笔记、个人创作草稿。
