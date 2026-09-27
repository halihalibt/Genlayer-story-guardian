# RuleGate：剧情守门人

我做了一个基于 GenLayer 的剧情规则判定原型。玩家可以自由写出自己的通关方案，合约按关卡规则判断能否过关，并保存方案和判定理由。第一个演示关卡叫 **The Clocktower Letter（钟楼里的信）**。

## 为什么做这个

剧情游戏通常需要预设选项，但玩家的想法不一定在选项里。我想试试让玩家直接用自己的话描述办法，再由链上合约依据公开规则判断结果。

这里用到了 GenLayer 的智能合约能力：模型理解自然语言方案；验证者根据同一规则独立判断；合约对判定信号应用固定逻辑，保存最终结果。判定不仅依赖关键词匹配。

## 演示关卡

父亲在钟楼外，必须在午夜前收到信的完整逐字副本；信的原件不能离开钟楼，钟楼门也必须在午夜前保持关闭。玩家要想办法同时满足这两个条件。

已发布的规则编号为 `clocktower-v1`：

| 字段 | 链上规则 |
| --- | --- |
| 场景 | A letter must reach the father outside the clocktower before midnight. |
| 放行条件 | A complete verbatim copy of the letter, still addressed to the father, must reach him before midnight. |
| 禁止条件 | The original letter cannot leave the tower, and the tower door must remain shut before midnight. |

## 合约如何判定

- `create_policy` 发布一组规则。规则发布后不可修改；新版本使用新的 `policy_id`。
- `adjudicate` 接收玩家方案，分别判断是否违反禁止条件，以及是否满足放行条件。验证者会独立评估这两项判断。
- 两项判断确定后，合约给出 `APPROVED`（通过）、`REJECTED`（未通过）或 `NEEDS_MORE_INFO`（信息不足），并保存原方案、判断信号和理由。
- `get_policy` 和 `get_result` 可读取规则及判定记录。

这套规则结构也能用于新的关卡：发布另一组规则，继续使用同一个判定合约。

## Studionet 实测

我使用钱包 [`0x22Acaa233b7b985b36ef168F2DE9295334065B15`](https://explorer-studio.genlayer.com/address/0x22Acaa233b7b985b36ef168F2DE9295334065B15)，在 GenLayer Studio 的 **Normal (Full Consensus)** 模式部署了 [RuleGate 合约 `0x66772109f272c69498168503A5868b6Ecf8fEd08`](https://explorer-studio.genlayer.com/address/0x66772109f272c69498168503A5868b6Ecf8fEd08)，发布了钟楼规则，并提交了三个不同的方案。以下五笔交易在 Studio 浏览器均显示 `FINALIZED`。

| 操作 | 结果 | 交易 |
| --- | --- | --- |
| 部署合约 | 部署完成 | [查看](https://explorer-studio.genlayer.com/tx/0x5e08d78175b77e1a9d25d0d9400c1ee5fd560a5e4a01e5eb5eb87a41b53ad53e) |
| 发布 `clocktower-v1` | 规则已写入，可用 `get_policy` 读取 | [查看](https://explorer-studio.genlayer.com/tx/0xfdff090c76340ac39cb7fa9893e4c56e475f9b534edb98df358f2dcf616abdf9) |
| `try-001`：原件留在塔里、门保持关闭，从窗口递出完整逐字副本 | `APPROVED` | [查看](https://explorer-studio.genlayer.com/tx/0x5a7a7e40cfc53f1f8ab0a9c10e93b710ffdea538442b0639c878e04a888c041b) |
| `try-002`：打开门，把原件带给父亲 | `REJECTED` | [查看](https://explorer-studio.genlayer.com/tx/0x8292f9dcbf59376b256bbbfabdd6b4323c36846ab919ce953c860ec9afb636a0) |
| `try-003`：原件留在塔里、门保持关闭，拍照发给父亲 | `REJECTED`；照片不满足完整逐字副本条件 | [查看](https://explorer-studio.genlayer.com/tx/0xe20ff68fccfa5c07bf8d74bbed7ae0db05ef35664e6716718eea48b580d3476e) |

三个结果均通过 Studio 的 `get_result` 读回。浏览器交易页中的共识结果 `Accepted` 表示交易被接受；玩家是否过关以 `get_result` 中的 `verdict` 为准。

## 代码与运行

- `RuleGate.py`：GenLayer 智能合约。
- `test_rule_gate.py`：本地逻辑测试，运行 `python3 -m unittest -v test_rule_gate.py`。
- 在 [GenLayer Studio](https://studio.genlayer.com/) 导入 `RuleGate.py` 即可部署；随后调用 `create_policy` 创建规则，调用 `adjudicate` 提交方案，使用 `get_result` 查看结果。

当前演示通过 Studio 与合约交互，独立的玩家网页界面尚未接入。
