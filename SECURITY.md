```markdown
# Security Policy

## Supported Versions
- main 分支为最新稳定版（推荐使用）

## Reporting a Vulnerability
发现安全问题请**私信**仓库所有者或提交 Issue（标题前缀 `[SECURITY]`）。

## 威胁模型
- **供应链攻击**：Hermes install.sh、npm 依赖
- **密钥泄露**：LLM / OnchainOS / GitHub Token
- **钱包风险**：$BEAT 自动转账/质押
- **Agent 自我进化**：Skill 被恶意修改
- **本地私钥风险**

## 本地私钥模式警告（高风险，仅本地使用）
- `LOCAL_TEST_PRIVATE_KEY_MODE=true` + `LOCAL_TEST_PRIVATE_KEY` **仅供 clone 后本地使用**。
- 私钥会明文落地在 `.env` 中（存在极高泄露风险）。
- 离开本地后请**立即**将 `LOCAL_TEST_PRIVATE_KEY_MODE` 设回 `false` 并**删除私钥**。
- Hermes 在此模式下会切换为本地私钥签名（非 OnchainOS TEE），模型可能间接访问私钥。
- 建议仅在本地测试机、虚拟机或临时容器中使用。

## 安全默认值（已强制）
- `MAX_AUTO_AMOUNT=0`（推荐）
- `REQUIRE_WALLET_CONFIRMATION=true`
- 所有 wallet 操作必须用户“确认”/“YES” + 交易模拟
- 生产环境可选择使用 OnchainOS 官方 TEE（私钥永不落地），本地可选择私钥模式。

## 密钥管理要求
- 建议 30 天轮换一次
- GITHUB_TOKEN 只给必要 scope

## 应急响应
1. 立即停止 Agent（`pm2 stop EvoBeat`）
2. 轮换所有密钥（包括本地私钥）
3. 检查 Hermes Memory 是否有异常记录
4. 提交新 Issue 并通知社区

## 安全工具
- `npm audit --level high`
- gitleaks / trufflehog（CI 推荐）
- Hermes 内置 Skill 签名验证（未来支持）

致力于让 EvoBeat 成为最安全的自进化音乐 Agent。
