# 📚 Web3 每日英语词汇卡 | Daily Web3 English Vocabulary Cards

> 内容来源 / Source：北京大学肖臻老师《区块链技术与应用》公开课
> Bilibili 课程：[BV1Vt411X7JF](https://www.bilibili.com/video/BV1Vt411X7JF/?p=4)
> 第四讲内容：BTC 协议 (Bitcoin Protocol)

---

## 📖 第四讲：比特币协议 | Lecture 4: Bitcoin Protocol

### 🧩 卡片 1：交易与余额

| 英文 | 中文 | 释义 |
|------|------|------|
| **Coinbase Transaction** | 铸币交易 | 每个区块中的第一笔交易，由矿工创建，用于新币发行和收取手续费 |
| **Genesis Transaction** | 创世交易 | 经常与铸币交易同义，指无输入的凭空产生的资金交易 |
| **Double Spending Attack** | 双花攻击 / 双重支付 | 试图将同一笔数字资产（如比特币）花费两次的恶意行为 |
| **UTXO (Unspent Transaction Output)** | 未花费交易输出 | 比特币的账本模型：每一次花费都必须明确引用之前的记录作为输入并销毁 |

**记忆技巧**：比特币没有"账户余额"这个数字，你的钱是一堆没有花出去的 UTXO 碎片。

---

### 🧩 卡片 2：分布式共识基础

| 英文 | 中文 | 释义 |
|------|------|------|
| **Distributed Consensus** | 分布式共识 | 去中心化网络中，使得互不信任的所有节点对状态达成一致的机制 |
| **Nakamoto Consensus** | 中本聪共识 | 基于 PoW 和最长链规则的共识机制，通过投入算力证明诚实 |
| **Longest Chain Rule** | 最长链规则 | 发生分叉时，节点默认选择累积难度最高（最长）的链作为有效主链 |
| **Sybil Attack** | 女巫攻击 | 攻击者伪造大量虚假节点/身份试图控制共识投票的攻击 |

**类比**：女巫攻击就像“买水军刷票”，但比特币用 PoW 规定必须出示“算力”，导致“水军数量”失去意义。

---

### 🧩 卡片 3：分布式系统理论

| 英文 | 中文 | 释义 |
|------|------|------|
| **CAP Theorem** | CAP定理 | 一致性(C)、可用性(A)、分区容忍性(P)无法三者兼得的分布式理论 |
| **Eventual Consistency** | 最终一致性 | 放弃强同步，只要经过一段时间（如6个区块），全网数据终将一致 |
| **Distributed Hash Table (DHT)** | 分布式哈希表 | 通过哈希函数在P2P网络中寻址与存储的常见底层架构（如 BT/IPFS） |

**区块链特性**：比特币为了确保网络不会宕机（A）和能应对网络断开（P），牺牲了强一致性（C），选择了 AP + 最终一致性。

---

### 🧩 卡片 4：传统共识与成员管理

| 英文 | 中文 | 释义 |
|------|------|------|
| **Paxos / Raft** | Paxos/Raft算法 | 传统的分布式一致性算法，用于中心或联盟少量节点间容错 |
| **Membership** | 成员管理 | 分布式系统中规定哪些节点可以加入系统、如何加入的限制机制 |
| **Permissionless** | 无准入许可 / 开放式 | 任何人随时可加入或退出且不需要审核的网络属性（如比特币） |
| **Permissioned** | 许可型 / 联盟式 | 需要身份验证和授权才能加入的网络（如联盟链） |

---

## 🔐 综合词汇速查表 | Quick Reference

| 英文术语 | 中文 | 核心关键词 |
|----------|------|----------|
| Coinbase Transaction | 铸币交易 | 唯一产币方式 |
| Double Spending | 双重支付 / 双花 | 防御核心 |
| UTXO | 未花费交易输出 | 记账模型 |
| Nakamoto Consensus | 中本聪共识 | PoW + 最长链 |
| Longest Chain Rule | 最长链规则 | 胜出链 |
| Sybil Attack | 女巫攻击 | 虚假身份 |
| Permissionless | 无准入许可 | 随时加入 |
| CAP Theorem | CAP 定理 | 三留其二 |
| Eventual Consistency | 最终一致性 | 弱一致性 |
| Distributed Consensus | 分布式共识 | 去中心化一致 |
| DHT | 分布式哈希表 | P2P寻址存储 |
| Paxos / Raft | 传统共识算法 | 联盟链常用 |

---

## 💡 学习建议 | Study Tips

1. **对比记忆**：注意对比传统银行账户模型与比特币的 **UTXO模型**，对比 Paxos 等传统共识与比特币的 **Nakamoto Consensus**。
2. **连接思维导图**：结合 `肖臻老师区块链技术与应用.mmd` 思维导图中“如何设计一个加密货币”部分复习这些名词。

---

*更新日期 / Last Updated: 2026-03-06 | 课程：北大肖臻《区块链技术与应用》EP04*
