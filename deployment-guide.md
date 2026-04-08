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

