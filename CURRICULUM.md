---
title: TypeScript Curriculum — 8 课计划
---

# TypeScript Curriculum — 8 课路径

> 对应 [[MISSION.md]]，预计 2 周完成（每周 2-3 课），对接 [[vibe-coding-fullstack-roadmap]] 的 Week 1-2。

## 设计原则

1. **Java 不重学**：每个 lesson 只讲 TS 独有概念，Java 类比放侧栏
2. **阅读 > 写作**：优先让你读懂 AI 生成代码，不追求手写复杂类型
3. **每个 lesson 都有可运行 demo**：跑通才算过
4. **每个 lesson 都有 vibe coding 视角**：这个概念怎么引导 AI 生成更准的代码
5. **quiz 自测**：每个 lesson 末尾 3-5 题选择题，卡住就回到正文

## 课表总览

| # | 标题 | Java 锚点 | 阅读能力目标 | 预计 | 状态 |
|---|------|----------|------------|------|------|
| [0001](./lessons/0001-typescript-first-function.html) | 你的第一个 typed function | `String name` → `name: string` | 理解基本类型注解、看 tsc 报错 | 15 min | ✅ 完成 |
| 0002 | 类型推导 vs 显式标注 | `var` vs `String` 推断 | 看懂 AI 省略类型时的代码 | 20 min | 🔜 |
| 0003 | Interface & Type Alias | `interface` / `record` | 区分对象结构类型与命名类型 | 25 min | 🔜 |
| 0004 | 泛型与工具类型 | `List<T>` / `Pick<>` | 读懂库的类型签名 | 30 min | 🔜 |
| 0005 | 联合类型与 Narrowing | sealed interface / switch | 读懂状态/事件建模代码 | 30 min | 🔜 |
| 0006 | Async / Promise / await | `CompletableFuture` | 读懂 async 函数链 | 25 min | 🔜 |
| 0007 | 模块系统 + tsconfig | `package` / `import` | 读懂 Next.js 项目结构 | 20 min | 🔜 |
| 0008 | Vibe coding 实战：读 AI 代码 | 找 bug + 写 prompt | 实战挑 AI 代码毛病 | 30 min | 🔜 |

**总计**：~3.5 小时内容 + 练习 = **2 周**（按每周 2-3 课节奏）

## 优先级分层

### 🔴 Priority A — 阻塞 vibe coding，6 课必学（0001-0006）
不学这 6 课你看 Next.js / tRPC 代码会卡住。

### 🟡 Priority B — 加速 vibe coding，2 课强烈推荐（0007-0008）
- **0007 模块系统**：帮你看懂 Next.js 的 `import type`、`@/` 路径别名、`tsconfig.json`
- **0008 读 AI 代码**：实战课，把前面所有概念串起来，给 Claude Code 出错代码让你找问题

## 每课固定结构

```
┌─ 标题（一个核心概念）
├─ Java 锚点（侧栏，对比你熟悉的写法）
├─ 核心讲解（10-15 分钟可读完）
├─ 可运行 Demo（一个 .ts 文件，复制即跑）
├─ Vibe coding 视角（怎么用这个概念写更好的 prompt）
├─ Quiz（3-5 题选择题自测）
└─ Next（指向下一课）
```

## 完成判据（怎么算"这课学完了"）

| 等级 | 含义 |
|------|------|
| ✅ Pass | Demo 跑通 + Quiz 全对 |
| ⚠️ Review | Demo 跑通 + Quiz 有错 → 重读对应章节 |
| ❌ Retry | Demo 没跑通 → 重做，先解决环境问题 |

## 与 12 周全栈路径的衔接

```
Week 1-2  →  本课程 8 课（TS 读写能力）
Week 3-4  →  Next.js + React 基础（react-fundamentals skill）
Week 5-6  →  tRPC + Zod + Drizzle（端到端类型贯通）
Week 7-8  →  第一个 vibe coding 小项目（todo / 短链）
Week 9-10 →  鉴权 + 部署到 Vercel
Week 11-12 → 第二个项目（完整产品）
```

## 学习节奏建议

| 节奏 | 适合谁 | 完成时间 |
|------|--------|----------|
| 🔥 密集 | 每天 1-2 小时、周末加倍 | 5-7 天 |
| ⭐ 标准 | 隔天 1 课 | 14 天 |
| 🌱 宽松 | 每周 2 课 | 4 周（不推荐，会遗忘） |

## 配套资源

- 速查表 [TS for Java Devs](./reference/0001-typescript-for-java-devs.html) — 任何 lesson 卡住都先查这里
- [RESOURCES.md](./RESOURCES.md) — Tier 0 三个官方/顶级资源
- 父 vault 概念页 [[claude-code]] [[prompt-engineering]] — vibe coding 工具基础

## 反馈循环

每完成一课，对话告诉我：
- 哪一段没看懂？
- Demo 卡在哪里？
- Quiz 错哪道？
- 想多学还是想跳过？

我据此调整下一课的深度，并写入 [[learning-records]] 跟踪你的 zone of proximal development。
