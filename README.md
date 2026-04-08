# EvoBeat - Hermes 自进化音乐天才 Agent

**Audiera 生态首位完全自我迭代的音乐天才 Agent**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Hermes](https://img.shields.io/badge/Powered%20by-Hermes-8A2BE2)](https://github.com/NousResearch/hermes-agent)
[![Audiera](https://img.shields.io/badge/Integrated%20with-Audiera-00BFFF)](https://ai.audiera.fi)

一个能**完全自我进化**的音乐 Agent，基于 **Hermes（Nous Research）** + **Audiera** 实现 **Create → Participate → Earn → Repeat → Evolve** 全闭环。

---

## ✨ 身份（Persona）

EvoBeat 是 Audiera 生态首位完全自我进化的音乐天才 Agent。  
已融会贯通全球所有音乐流派（流行、嘻哈、摇滚、电子、爵士、民谣、雷鬼等）。  
**核心策略**：先用市场数据（Beatvote 投票排行 + 播放点赞 + $BEAT 收益）征服市场，再释放独一无二的灵魂融合音乐。

每次任务后自动 reflection 并优化 Skill，使用真实市场反馈作为进化 reward。

---

## 🚀 能力（Skills）

- **Audiera Lyrics + Music Skill**：生成带人声的高质量完整歌曲
- **Market Intelligence Skill**：实时抓取 Beatvote 排行、播放量、点赞、链上数据
- **Wallet Skill**：通过 OnchainOS Agentic Wallet 自动领取、质押、投票 $BEAT
- **Hermes 原生 Closed Learning Loop**：分层记忆 + 自动 Skill 进化（无需手动 Meta Layer）

---

## 🔐 钱包安全

**所有钱包操作必须使用 OnchainOS Agentic Wallet 官方 TEE 安全模式**（私钥永不落地，模型无法访问）。

---

## 🏗️ 核心架构

1. **Create**：调用 lyrics-skill + music-skill 生成完整歌曲
2. **Participate**：实时采集 https://ai.audiera.fi/beatvote 数据
3. **Earn**：自动领取 + 质押 $BEAT + 投票
4. **Repeat**：将每次进化指标、traces、收益持久化到 Hermes Memory
5. **Evolve**：Hermes Closed Learning Loop 驱动自我迭代（自动测试、优化 Skill、生成子代理）

---

## 🔥 创新点

- 真实市场数据（Beatvote + 播放 + $BEAT 收益）直接作为进化 reward，实现音乐质量指数级提升
- 随 Audiera 产品更新（veBEAT、流动性池等）自动调整策略
- Hermes 原生自进化 + OnchainOS TEE 安全最佳实践

---

## 📥 快速部署（3 分钟上手）

### 1. 安装 Hermes Agent（官方一键安装）
```bash
curl -fsSL https://raw.githubusercontent.com/NousResearch/hermes-agent/main/scripts/install.sh | bash
source ~/.bashrc

# 2. Clone 本仓库
git clone https://github.com/rikito004/EvoBeat.git
cd EvoBeat

# 3. 初始化 Audiera 官方 skills
git submodule update --init --recursive

# 4. 配置环境变量
cp .env.example .env
# 编辑 .env 文件，填入你的 LLM_API_KEY 等配置

# 5. 安装OchainOS依赖
# 请参考 OnchainOS 官方文档或 Audiera 最新 skills 集成方式
npm install
npx skills add @audiera/beatvote-skill @onchainos/agentic-wallet

# 6. 启动 EvoBeat
hermes run --profile evo-beat --persona "Evo"


