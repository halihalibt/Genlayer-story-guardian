# Projects 提交说明（待网页钱包实测后使用）

## 可提交的链接

- 公开试玩：https://story-guardian-clocktower.zsf197176.chatgpt.site
- 公开代码：https://github.com/halihalibt/Genlayer-story-guardian/tree/projects-story-guardian
- 原 Intelligent Contracts 提交快照：https://github.com/halihalibt/Genlayer-story-guardian/tree/intelligent-contracts-submission
- 已部署合约：https://explorer-studio.genlayer.com/address/0x66772109f272c69498168503A5868b6Ecf8fEd08
- 规则 ID：`clocktower-v1`
- 已有三条链上判定：`try-001`（APPROVED）、`try-002`（REJECTED）、`try-003`（REJECTED）

## 项目介绍（英文，可复制）

Story Guardian is a browser-based interactive story game powered by a GenLayer Intelligent Contract. Players describe their own solution to The Clocktower Letter instead of selecting preset options. The website reads the immutable policy and finalized sample verdicts directly from Studionet without a wallet. Players can connect an EVM wallet, submit a new proposal through the RuleGate contract, follow the transaction, and read the final onchain verdict and reasoning. The contract uses natural-language assessments with independent validator checks and deterministic verdict mapping. The frontend includes Chinese and English, transaction recovery after refresh, and links to the contract and transaction explorer. It is a free testnet demonstration.

## 提交前核对

1. 用浏览器钱包从网页提交一个**新的**方案，得到最终判定和交易哈希。
2. 刷新网页后，在“我的提交记录”中打开该方案并核对判定。
3. 保存网页判定截图、钱包交易截图或浏览器交易页链接。
4. 确认以上公开试玩与代码链接可以正常打开，再按 Portal 的 Projects 表单要求填写。

尚未取得新的网页钱包交易时，应说明：“The read-only app and historical onchain outcomes are verified. A new wallet-signed website submission remains to be demonstrated.” 不要把 Studio 中的旧交易说成从网页提交。
