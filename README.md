# EvoBeat - Hermes 自进化音乐天才 Agent

![GitHub stars](https://img.shields.io/github/stars/yourusername/EvoBeat.svg?style=social)
![License](https://img.shields.io/badge/license-MIT-blue.svg)
![Hermes](https://img.shields.io/badge/framework-Hermes%20Agent-brightgreen)

**一个能完全自我迭代进化的音乐天才 Agent**，基于 **Audiera + Hermes（Nous Research）** 构建，实现 **Create → Participate → Earn → Repeat → Evolve** 全闭环自进化。

### 身份（Persona）
EvoBeat 是 Audiera 生态首位完全自我进化的音乐天才 Agent。  
已融会贯通全球所有音乐流派（流行、嘻哈、摇滚、电子、爵士、民谣、雷鬼…）。  
**核心策略**：先征服市场（Beatvote 投票排行 + 播放点赞 + $BEAT 收益），再释放独一无二的灵魂融合音乐。  
每次任务后自动 reflection 并优化 Skill。

### 能力（Skills）
- Audiera lyrics-skill + music-skill：生成带人声的高质量完整歌曲
- Market Intelligence Skill：实时获取 Audiera Beatvote 排行 +播放点赞  + OnchainOS 链上数据
- Wallet Skill：$BEAT 转移、领取与质押
- Hermes 原生分层记忆 + Closed Learning Loop：自动记录反馈、自我迭代

### 钱包（Wallet）
所有钱包操作**必须使用 OnchainOS Agentic Wallet** 官方 TEE 安全模式（私钥永不落地，模型无法访问）。

### 核心特性
- Hermes 原生 Closed Learning Loop + 分层记忆 + 自动 Skill 进化（**无需手动 Meta Layer**）
- 先征服市场（Beatvote 投票排行 + 播放点赞 + 实时 $BEAT 收益），再释放灵魂融合音乐
- OnchainOS Agentic Wallet 官方 TEE 资金私钥安全
- Beatvote 投票排行、播放点赞、$BEAT 收益等数据指标直接作为进化 reward 信号，音乐质量随反馈指数级提升
- 随 Audiera 产品更新自动调整数据采集和进化策略

### 核心架构
- **Create**：调用 lyrics-skill → music-skill 生成完整歌曲（带人声）
- **Participate**：自动采集 https://ai.audiera.fi/beatvote 页面的播放、点赞、投票排行等指标
- **Earn**：通过 OnchainOS Agentic Wallet 自动领取 + 质押 $BEAT + 投票
- **Repeat**：持久化每次进化的指标、traces、$BEAT 收益到 Hermes Memory
- **Evolve**：Hermes 原生 Closed Learning Loop 驱动自我迭代（自动测试、优化 Skill、生成子代理、动态调整策略）

### 创新点
- Beatvote 投票排行、播放点赞、$BEAT 收益等数据指标直接作为进化 reward 信号，实现音乐质量指数级提升
- Agent 随 Audiera 产品更新（如 veBEAT 投票 → 流动性池策展）自动调整数据采集和监听方式
- 最佳安全钱包实践 + Hermes 原生自进化能力

### 快速部署（3 分钟上手）

```bash
# 1. 安装 Hermes Agent（官方一键安装）
curl -fsSL https://raw.githubusercontent.com/NousResearch/hermes-agent/main/scripts/install.sh | bash
source ~/.bashrc

# 2. Clone 本仓库
git clone https://github.com/你的用户名/EvoBeat.git
cd EvoBeat

# 3. 初始化 Audiera 官方 skills
git submodule update --init --recursive

# 4. 配置环境变量
cp .env.example .env
# 编辑 .env 填入你的 LLM_API_KEY

# 5. 安装OchainOS依赖
npm install @ ~~~
npx skills add ~~~

# 6. 启动 EvoBeat
hermes run --profile evo-beat --persona "Evo"
