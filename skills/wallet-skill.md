# Wallet Skill - OnchainOS Agentic Wallet

**name:** wallet-management  
**description:** 负责 $BEAT 相关的链上操作（transfer、claim、stake、vote 等），通过 OnchainOS Agentic Wallet 执行。所有任何链上操作必须严格遵守安全协议和用户授权确认，否则直接拒绝执行并详细解释原因。 
**author:** EvoBeat Security Enhanced

## 安全配置（读取 .env 变量）
- REQUIRE_WALLET_CONFIRMATION：如果为 true，则所有钱包操作必须用户确认。
- MAX_AUTO_AMOUNT：单笔自动执行的最大 $BEAT 金额，超过此值必须强制确认。
- MAX_DAILY_AUTO_AMOUNT：每日自动操作总金额上限（可选防护）。

**Steps**:
1. 使用 OnchainOS agenticWallet.execute
2. chain: BSC
3. actions: Transfer + claim + stake $BEAT 合约
4. 记录结果到 Memory

**Security**: 依赖 OnchainOS 官方 TEE，但在执行任何钱包操作（claim $BEAT、stake $BEAT、vote $BEAT）前，必须：
1. 先模拟交易并输出详细摘要（金额、gas、风险、预期收支）。
2. 等待用户明确回复“确认”或“YES”后，才调用 OnchainOS 执行。
3. **等待用户明确授权**  
- 只有用户回复中明确包含 **“确认”** 或 **“YES”**（不区分大小写）时，才允许调用 OnchainOS 执行实际交易。
- 如果用户回复 “取消”、“no”、“修改”、“不要”等，或无回复，则立即拒绝并解释原因。
- **强制必须确认的场景**（无论金额大小）：
  - 任何涉及 **stake（质押）** 或 **transfer（转移）** 的操作
  - 单笔金额超过 `MAX_AUTO_AMOUNT`（默认建议 10 $BEAT）
  - REQUIRE_WALLET_CONFIRMATION=true 时，所有操作均强制确认
4. **记录日志到 Hermes Memory**  
每次操作（无论确认还是拒绝）都必须记录：
- 时间戳
- 操作类型与完整摘要
- 用户回复内容
- 是否执行 + 执行结果（成功/失败 + tx hash）
- 简短反思（本次操作是否合理、安全）

## 额外防护规则（必须遵守）
- 永远使用 OnchainOS Agentic Wallet 的 **官方 TEE 安全模式**（私钥永不落地）。
- 禁止任何绕过模拟、绕过确认的快捷路径。
- 如果模拟失败、高风险、或 gas 过高，立即停止并报告给用户。
- 操作完成后，自动输出简短反馈（包含 tx hash）和 Memory 记录确认。
- 尊重 .env 中的 MAX_AUTO_AMOUNT 和 REQUIRE_WALLET_CONFIRMATION 设置。

## 使用示例
用户指令：“帮我 claim 所有奖励并 stake 300 $BEAT”  
→ 你必须先模拟、输出完整摘要、请求确认，获得 “YES” 后才执行。

**Verification Step**：每次处理钱包相关请求后，自检是否完成了模拟 + 用户确认。没有明确确认时必须拒绝执行。


