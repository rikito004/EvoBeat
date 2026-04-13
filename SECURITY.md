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

## 安全默认值（已强制）
- `MAX_AUTO_AMOUNT=100`
- `REQUIRE_WALLET_CONFIRMATION=true`
- 所有 wallet 操作必须用户“确认”/“YES” + 交易模拟
- 私钥永不落地（OnchainOS TEE）

## 密钥管理要求
- 严禁提交任何 .env 文件
- 建议 30 天轮换一次
- GITHUB_TOKEN 只给必要 scope

## 应急响应
1. 立即停止 Agent（`pm2 stop EvoBeat`）
2. 轮换所有密钥
3. 检查 Hermes Memory 是否有异常记录
4. 提交新 Issue 并通知社区

## 安全工具
- `npm audit --level high`
- gitleaks / trufflehog（CI 推荐）
- Hermes 内置 Skill 签名验证（未来支持）

我们致力于让 EvoBeat 成为最安全的自进化音乐 Agent。
