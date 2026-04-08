## EvoBeat 部署指南

# 1. 安装 Hermes Agent
curl -fsSL https://raw.githubusercontent.com/NousResearch/hermes-agent/main/scripts/install.sh | bash
source ~/.bashrc

# 2. Clone 本仓库
git clone https://github.com/rikito004/EvoBeat.git
cd EvoBeat

# 3. 初始化 Audiera 官方 skills
git submodule update --init --recursive

# 4. 配置环境变量
cp .env.example .env
# 至少填写 LLM_API_KEY
# 如需其他变量，请参考 Hermes / OnchainOS 文档

# 5. 安装OchainOS依赖
npm install
# 添加 Audiera 与 OnchainOS skills（根据官方最新文档调整）
npx skills add @audiera/beatvote-skill @onchainos/agentic-wallet

# 6. 启动 EvoBeat
hermes run --profile evo-beat --persona "Evo"

