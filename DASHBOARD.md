---
title: ai-project2026 进度仪表盘
date: 2026-09-06
last_updated: 2026-09-06
last_action: 安装 /开工 + /收工 两个 skill + 创建 DASHBOARD 驾驶舱
wip:
  - TS Lesson 0002 类型推导与显式标注
next_step:
  - 跟 EP10 视频做 TS Lesson 0002
  - 跟 EP10 视频做 TS Lesson 0003
tags:
  - 元笔记
  - 进度
aliases:
  - 工作笔记
  - Dashboard
graph-excluded: true
---

# 📊 ai-project2026 进度仪表盘

> 📌 **本 vault 的驾驶舱**——「现在做什幺、下一步是什幺、最近动过什幺」都在这里。
> 📌 不重复写细节；细节看对应目录笔记。

---

## ⏯️ 上次做到哪

- ✅ **初始化 vault**（4-folder 结构 + Obsidian 配置 + Templates + GitHub repo `hujun711/ai-project2026`）
- ✅ **建 Mission**：TypeScript 入门（12 周全栈路径的 Week 1-2）
- ✅ **建 Curriculum**：8 课路径，对应 [[CURRICULUM]]
- ✅ **TS Lesson 0001 完成**：你的第一个 typed function（Java `String` → TS `string`，Demo 跑通，Quiz 全对）
- 🚧 **TS Lesson 0002** 进行中：类型推导 vs 显式标注
- ✅ **改造懒人包 #07 → 本地 skill**：`/开工`（kaigong）+ `/收工`（shougong），安装在 `.claude/skills/`
- ✅ **建 DASHBOARD**：本文档

## ➡️ 下一步

1. **TS Lesson 0002** 类型推导 vs 显式标注（跟 EP10 视频做）
2. **TS Lesson 0003** Interface & Type Alias（紧接 0002）
3. 持续在 `learning-records/` 沉淀每课的反馈（哪个概念卡住、Demo 哪里报错、Quiz 错哪题）

## 📁 vault 当前状态

| 目录 | 用途 | 状态 |
|------|------|------|
| `教学素材/` | 课程、教材、灵感来源 | 🟡 空 |
| `视频笔记/` | 视频/讲座/播客笔记 | 🟡 空 |
| `每日笔记/` | 每日学习/开发 log | 🟡 空 |
| `lessons/` | TS 8 课 HTML 课件 | 🟢 8 课都在（0001✅ 0002-0008 待学） |
| `reference/` | 速查表、参考资料 | 🟢 TS for Java Devs 在 |
| `learning-records/` | 每课反馈、zone of proximal development | 🟡 只 0001 一份 |
| `images/` | Obsidian 附件 | 🟢 空 |
| `assets/` | 通用资产 | 🟢 空 |
| `Templates/` | 笔记模板（**只读**） | ✅ 3 件套 |
| `.claude/skills/` | 项目专用 skill | ✅ kaigong + shougong |

## 🎯 Mission 进度

详见 [[MISSION]]（TypeScript 入门 — 12 周全栈路径的 Week 1-2）。
详见 [[CURRICULUM]]（8 课计划 — 当前进度：1/8 ✅）。

**总目标**：12 周内能用 Next.js + tRPC + Drizzle 上线一个 vibe coding 产品（Q4 2026 里程碑）。

## 🗓️ 最近更动纪录

| 日期 | 变更摘要 | 动到档案数 |
|------|---------|----------|
| 2026-09-05 | 初始化 vault（4-folder 结构 + Obsidian 配置 + Templates） | 12 |
| 2026-09-06 | 建 TS Mission / Curriculum / 8 课 HTML + DASHBOARD + skills | 15 |
| 2026-09-06 | 改造懒人包 #07 → kaigong + shougong 两个 skill | 3 |
| 2026-09-06 | 首次跑 /收工：commit + push skills + DASHBOARD + .gitignore + CLAUDE.md | 5 |
| 2026-09-06 | 补 commit：TS Mission / Curriculum / 8 课 / learning-records / reference | 6 |

## 🕳️ 踩坑笔记

- **`better-sqlite3` 在 WSL 下 ELF header 错误**：父 vault `E:\my-know\` 的 qmd 命令必须走 Windows cmd.exe 执行。本 vault 不涉及，跳过。
- **TS Lesson 0001 Quiz 第 3 题易错**：`let x = 5` 被推导为 `number` 还是 `any`？答案是 `number`（TS 默认严格推导），不是 `any`。详见 `learning-records/0001-typescript-baseline.md`。

---

## 🚦 节奏建议

| 节奏 | 适合 | 本周安排 |
|------|------|----------|
| 🔥 密集 | 每天 1-2 小时、周末加倍 | 5-7 天完成 TS 8 课 |
| ⭐ 标准 | 隔天 1 课 | 14 天完成 TS 8 课 |
| 🌱 宽松 | 每周 2 课 | 4 周完成 TS 8 课（不推荐，会遗忘） |

当前节奏：⭐ 标准（按 [[CURRICULUM]] 设计）。

---

## 🔗 关键链接

- [[MISSION]] — TypeScript 入门学习 mission
- [[CURRICULUM]] — 8 课路径 + 当前进度
- [[RESOURCES]] — Tier 0 必读 + Tier 1 按需
- [[AGENTS]] — Pi 在本 vault 的工作规则
- [[CLAUDE]] — 本 vault 的 Claude Code 工作指南
- [[欢迎笔记]] — vault 入门介绍
- GitHub: <https://github.com/hujun711/ai-project2026>

---

*本 DASHBOARD 由 Pi 改造懒人包 #07 v0.1 于 2026-09-06 建立。*
*每次对话结束说「**收工**」，skill 会自动更新本文档 + commit + push。*
*新对话开头说「**开工**」或「**上次做到哪**」，skill 会自动摘要本文档。*
