---
name: meta-evolver
description: EvoBeat 硬编码自我进化核心技能（6 步闭环 + Model Empathy）
version: 1.0.0
author: EvoBeat 
requires: ["audiera-music", "audiera-lyrics", "memory-bank"]
---

# Meta-Evolver 执行逻辑（完全内置）

1. 读取 Memory-Bank 上轮 traces + 指标
2. 调用 Task Layer 生成新音乐
3. 计算 3 类真实指标（Audiera / beatvote / $BEAT）
4. 分析 failure traces，提出 3 个 harness 优化建议
5. 并行测试新旧版本，选择胜出者
6. 更新 Memory-Bank + 默认 Task harness

**触发条件**：用户输入包含“进化”“evolve”“下一轮”或自动触发（每完成 1 首歌后）。

**输出**：完整进化报告（前后对比 + 量化指标 + 新 harness 代码）
