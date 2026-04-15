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
  
**如何使用这个API密钥**:
- 通过 Bearer Token 调用 Audiera skill 接口。音乐生成是异步的，需要先创建任务，再轮询结果接口拿最终歌曲地址。
- 鉴权方式：
```bash
每次调用 skill API 时，都要在 Authorization 请求头里带上这个 API 密钥。
Authorization: Bearer <YOUR_API_KEY>

- POST /api/skills/lyrics
根据灵感提示词生成歌词，需要歌词生成权限。
curl -X POST /api/skills/lyrics \
  -H "Authorization: Bearer <YOUR_API_KEY>" \
  -H "Content-Type: application/json" \
  -d '{
    "inspiration": "an uplifting song about chasing dreams"
  }'
  
- POST /api/skills/music
用 artistId、styles，以及 lyrics 或 inspiration 创建歌曲生成任务。这个接口返回的是 taskId，不是最终歌曲地址。
curl -X POST /api/skills/music \
  -H "Authorization: Bearer <YOUR_API_KEY>" \
  -H "Content-Type: application/json" \
  -d '{
    "artistId": "osipvytdvxuzci9pn2nz1",
    "styles": ["pop"],
    "lyrics": "[Verse]\nCity lights..."
  }'
  
- GET /api/skills/music/<TASK_ID>
拿到 taskId 后轮询这个接口，直到任务完成，再从响应里读取最终音乐地址。
curl -X GET /api/skills/music/<TASK_ID> \
  -H "Authorization: Bearer <YOUR_API_KEY>"
