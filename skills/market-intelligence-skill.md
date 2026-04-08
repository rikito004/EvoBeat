# Market Intelligence Skill - Evo 实时市场数据

**Description**: 获取 Audiera + OnchainOS 实时数据，驱动进化决策。

**Steps**:
1. OnchainOS MCP 优先：$BEAT K线、funding rate、top tokens
2. OnchainOS dex-market：BSC 链上行情 + 余额
3. Audiera Beatvote 页面 puppeteer 抓取：投票排行、点赞、播放量、Top/Bottom 歌曲
4. 计算 stage（market_mode / soul_mode）并保存到 Hermes Memory
5. 返回数据给 Evo 决策
   
**When to use**: 每次生成歌曲前 + 进化 reflection 时
