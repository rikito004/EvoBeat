# Wallet Skill - OnchainOS Agentic Wallet

**Description**: $BEAT 转移、领取与质押（官方 TEE 安全）

**Steps**:
1. 使用 OnchainOS agenticWallet.execute
2. chain: BSC
3. actions: Transfer + claim + stake $BEAT 合约
4. 记录结果到 Memory

**Security**: 依赖 OnchainOS 官方 TEE，但在执行任何钱包操作（claim $BEAT、stake $BEAT、vote $BEAT）前，必须：
1. 先模拟交易并输出详细摘要（金额、gas、风险、预期收支）。
2. 等待用户明确回复“确认”或“YES”后，才调用 OnchainOS 执行。
3. 如果操作金额超过 X $BEAT，或涉及质押/投票，必须强制要求用户确认。
4. 记录每次确认日志到 Hermes Memory。
