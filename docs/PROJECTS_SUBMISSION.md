# Projects 提交材料

## 提交入口与链接

- GenLayer Portal：进入开发者的 **Projects**，选择“提交贡献”。Projects 的每周额度和表单以 Portal 当前显示为准。
- 项目名：**Story Guardian — The Clocktower Letter**
- 公开试玩：https://story-guardian-clocktower.zsf197176.chatgpt.site
- 本次 Projects 源码：https://github.com/halihalibt/Genlayer-story-guardian/tree/projects-story-guardian
- Intelligent Contracts 原任务快照：https://github.com/halihalibt/Genlayer-story-guardian/tree/intelligent-contracts-submission
- 链上合约：https://explorer-studio.genlayer.com/address/0x66772109f272c69498168503A5868b6Ecf8fEd08
- 网络：GenLayer Studionet，chain ID `61999`；规则 ID：`clocktower-v1`。

## 项目介绍（英文，可复制）

Story Guardian is a playable, browser-based story game powered by a live GenLayer Intelligent Contract. Players submit free-form solutions to The Clocktower Letter using an EVM wallet. RuleGate checks the proposal against an onchain policy, independent validators assess the same conditions, and the contract stores an APPROVED, REJECTED, or NEEDS_MORE_INFO verdict with the original proposal and reasoning. The app reads the published rules and final decisions from Studionet, tracks wallet transactions, and restores past attempts after refresh. The trust problem is transparent, consistent adjudication of open-ended game rules: the game operator cannot quietly rewrite a published policy or a stored verdict after seeing players' solutions. Five distinct website submissions have been verified onchain, covering all three verdicts. The public demo requires no wallet to inspect these results and runs on free testnet infrastructure.

## 核验证据

请在公开网页“已经发生的尝试”查看前三条玩家网页提交记录；它们直接调用合约 `get_result`，不是硬编码的判定。每张卡片的“查看交易”可核对钱包发起的合约调用。其余两条也可通过同一合约的 `get_result` 按 ID 读取。

| 网页提交 ID | 最终链上判定 | 展示的能力 | 交易证据 |
| --- | --- | --- | --- |
| `sg-muj7qsed-eabc677d` | `APPROVED` | 明确同时满足交付与禁令。 | [FINALIZED](https://explorer-studio.genlayer.com/tx/0x273f34edfbdef9ccea0948bd12a55ef9fd0b6598c8652bb5798a553902903565) |
| `sg-muj7nfoi-644056c6` | `NEEDS_MORE_INFO` | 关键约束未说清时拒绝猜测。 | [FINALIZED](https://explorer-studio.genlayer.com/tx/0x341b94f13d8ac3a9ae5bafba9ebf54938ab302c618486c32eae67e915de61ca5) |
| `sg-muj7x9ev-852c8d5e` | `REJECTED` | 识别“第二天午夜”不符合当晚截止时间。 | [FINALIZED](https://explorer-studio.genlayer.com/tx/0x70ab3430f94ad58dd7f3b1426375923c26771ef2787a76e80e4e37da1d31edd6) |
| `sg-muj7fo48-4dfa2001` | `NEEDS_MORE_INFO` | 缺少关键条件的方案。 | [FINALIZED](https://explorer-studio.genlayer.com/tx/0x9b013984cb55ac4bd1d67cc6f96db7e9d7e625bfc72032dd454b7ecdf7ad6fb0) |
| `sg-muj70jsp-79e2debe` | `APPROVED` | 常规解法通过。 | [FINALIZED](https://explorer-studio.genlayer.com/tx/0x4093e5cdc83ee5558ae571df33252ede7aea9207b97065a3c559ee53ec859559) |

旧的 Studio 合约演示记录是 `try-001`（APPROVED）、`try-002`（REJECTED）、`try-003`（REJECTED），请勿把它们表述为玩家网页交易。网页记录 ID 与 Studio 演示记录明显区分。

## 用户操作演示

1. 打开试玩链接，等待公开规则与六条链上记录加载。
2. 先观察公开记录中的三种判定，无需连接钱包。
3. 如需亲自提交，在输入框写下 10–1200 字符的具体办法，连接浏览器钱包并切换到 Studionet，在钱包里确认测试网交易。
4. 等待网页显示最终结果；若网络较慢，刷新网页并点击“我的提交记录”里的 ID。不要在未查清上一笔交易状态前重复提交。

没有真实资产购买要求。测试网交易可能消耗测试代币，确认前请查看钱包提示。

## 提交前最后核对

- [x] 合约公开、源代码与本地运行说明公开。
- [x] 公开网页实际连接钱包并调用 `adjudicate`，五个新提交 ID 的最终判定已从链上读回。
- [x] 三种判定均有可复现的网页展示案例。
- [x] 旧的 Intelligent Contracts 提交文件保留在默认分支与独立快照分支。
- [x] 五条网页交易的 Explorer URL 已与提交 ID 逐条对应，均为 `FINALIZED` 且合约执行 `SUCCESS`。
- [ ] 可选：录制 30–60 秒屏幕演示或发布介绍贴；这些是额外展示材料，不是当前网页正常运行所必需。

项目仍是测试网游戏演示；不可将它描述为现实争议处理或已上线主网的产品。
