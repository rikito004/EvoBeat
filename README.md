EvoBeat/
├── README.md                  ← 主文档
├── openclaw.json              ← OpenClaw 核心配置文件
├── skills/
│   └── meta-evolver/
│       └── SKILL.md           ← 自我进化核心技能
├── audiera-skills/            ← 子模块（git submodule 添加官方 skills）
│   ├── music-skill/           ← git submodule add https://github.com/audiera/music-skill.git
│   └── lyrics-skill/          ← git submodule add https://github.com/audiera/lyrics-skill.git
├── deployment-guide.md        ← 详细部署教程
├── LICENSE                    ← MIT 开源
└── .gitignore

# EvoBEAT —— Audiera 生态首位完全自我进化音乐天才 Agent

**Create → Participate → Earn → Repeat → Evolve**（闭环自进化）

全球首个**硬编码 6 步 Meta + Task 双层自进化**音乐 Agent，完全基于 OpenClaw + Audiera 官方 music/lyrics 技能构建。**无需任何外部引用**，运行时 100% 自包含。

### 核心架构（内置，无需额外抓取）
- **Task Layer**：音乐创作、https://ai.audiera.fi/zh/explore?tab=beatvote投票采集、Wallet 监控
- **Meta Layer**：硬编码 6 步进化循环（编辑 harness → 运行测试 → 测量指标 → 分析 traces → 保留/回滚 → 迭代）
- **Memory-Bank**：持久化每次进化数据（指标、traces、$BEAT 收益）
- **Model Empathy**：Meta 与 Task 使用相同模型，完美理解失败模式
- **涌现行为**：自动写单元测试、自检 checklist、生成子代理、动态编排

**创新点**：$BEAT 收益直接作为进化 reward 信号，音乐质量随反馈指数级提升。

### 快速部署（3 步）
```bash
# 1. 安装 OpenClaw
npm install -g openclaw@latest
openclaw onboard --install-daemon

# 2. Clone 本仓库
git clone https://github.com/你的用户名/EvoBeat.git
cd EvoBeat

# 3. 添加 Audiera 官方 skills（子模块）
git submodule update --init --recursive

# 4. 配置环境变量
export AUDIERA_API_KEY="sk_audiera_你的key"   # 从 https://ai.audiera.fi 获取
