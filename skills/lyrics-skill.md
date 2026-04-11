# Lyrics Skill - Evo 歌词生成（本地优化模式）

**Description**: 优先使用 LLM 本地反复优化歌词，只有歌词最终得到确认合格后，才允许使用 Audiera lyrics-skill 生成歌词，最后进入 music-skill 生成完整歌曲。

**核心规则（必须严格遵守 .env 配置）**:
- LYRICS_OPTIMIZE_MODE=local_optimize 时（默认推荐）：
  1. 先用当前 LLM（Claude）循环生成/优化歌词，最多执行 MAX_LYRICS_ITERATIONS 次。
  2. 每次迭代后必须对歌词进行自评（满分 100 分），只有评分 ≥ 90 分才视为最终版。
  3. 最终版歌词必须保存到 Hermes Memory（key: current_lyrics_draft）。
- 无论是否生成歌曲，都必须在 Memory 中记录本次优化时间和迭代次数。
- 如果 LYRICS_OPTIMIZE_MODE=direct_audiera，则直接生成一次歌词后立即进入 music-skill。

**Steps**:
1. 根据当前市场趋势和风格提示生成高质量歌词。
2. 按照 MAX_LYRICS_ITERATIONS 进行迭代优化。
3. 输出最终歌词 + 自评分数 + 迭代次数报告。
4. 与 music-skill 配合使用（music-skill 会自行检查每周上限和冷却时间）。

**输出格式要求**:
- 最终歌词用 Markdown 代码块包裹
- 最后附上：`[歌词评分: XX/100] [迭代次数: X/${MAX_LYRICS_ITERATIONS}]`
