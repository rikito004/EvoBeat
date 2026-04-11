
# Music Skill - Evo 音乐生成（带成本控制）

**Description**: 只有歌词已本地优化合格得到确认 + 满足每周创作限制 + 冷却时间后，才调用 AUDIERA API 生成完整歌曲。

**核心规则（必须严格遵守 .env 配置）**:
- 必须先检查以下条件（全部通过才允许调用 AUDIERA）：
  1. 本周已创作歌曲数量 < MAX_SONGS_PER_WEEK（当前为 1）
  2. 距离上次成功生成歌曲已超过 AUDIERA_SONG_COOLDOWN（当前为 7d）
- 使用 Hermes Memory 记录每次**成功调用 AUDIERA** 的时间和计数（key: song_creation_log），每周一 00:00 UTC 自动重置计数。
- 如果任一条件不满足：
  - 跳过 AUDIERA 调用
  - 只将当前 Memory 中的 current_lyrics_draft 保存为「待生成歌词」
  - 输出「已进入冷却/达到每周上限，本周不再生成新歌」的提示
- 只有条件全部通过时，才真正调用 AUDIERA API 生成带人声的完整歌曲。

**Steps**:
1. 从 Memory 读取 current_lyrics_draft（必须是LLM本地优化后得到确认的最终版才提交给lyrics-skill生成歌词）
2. 检查 MAX_SONGS_PER_WEEK 和 AUDIERA_SONG_COOLDOWN
3. 如果通过 → 接收 {{STYLE_HINT}}（market_mode 或 soul_mode）歌词并调用lyrics和Audiera music API
4. 成功后：
   - 上传到 Beatvote
   - 在 Memory 中记录本次创作时间和计数
   - 返回 song_id 和链接

**When to use**: 仅在 EvoBeat 反射循环（EVOLVE_INTERVAL）中、且所有成本控制条件满足时使用。

**输出格式要求**:
- 如果跳过：明确说明原因 + 剩余冷却时间 + 本周剩余次数
- 如果成功：返回 song_id、Beatvote 链接、完整歌词
