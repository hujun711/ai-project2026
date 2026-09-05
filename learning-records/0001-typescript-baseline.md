# LR-0001: TS 学习 baseline — Java 心智模型已建立

**What was established**：用户在 2026-09-06 启动 TypeScript 学习，背景为 Java 后端工程师（强类型、泛型、Spring/JVM、并发、数据库）。明确目标：Java → TypeScript 全栈 → vibe coding 生产力。明确决定：跳过 Vue，单语言全栈方向（Next.js + tRPC + Drizzle + Vercel），12 周路径。

**Why it matters**：未来 session 不需要重新讲「什么是泛型」「什么是接口」「什么是依赖注入」「什么是接口隔离」。可以直接用 Java 概念做类比，跳到 TS 独有的部分（structural typing、type inference、discriminated unions、utility types、模板字面量类型）。

**Implications**：
- 课程跳过 OOP 基础、集合框架、并发原语
- 优先讲 TS 独有：structural typing、type inference、discriminated unions、utility types、`as const`
- 每个 TS 概念都要给 Java 对应点（如：`unknown` ≈ `Object` 上界，`never` ≈ 无返回方法的返回类型）
- 不深讲 React/Vue（Next.js 时再学）
- 节奏：1 lesson / 周，每 lesson 必须有可运行 demo
- vibe coding 杠杆点必标：哪些 TS 写法能让 Claude Code / Cursor 生成更准确的代码
