# 📚 Web3 每日英语词汇卡 | Daily Web3 English Vocabulary Cards

> 内容来源 / Source：北京大学肖臻老师《区块链技术与应用》公开课
> Bilibili 课程：[BV1Vt411X7JF](https://www.bilibili.com/video/BV1Vt411X7JF/?p=17)
> 第十七讲内容：ETH 交易树和收据树 (Ethereum Transaction & Receipt Trees)

---

## 📖 第十七讲：交易树和收据树 | Lecture 17: Transaction & Receipt Trees

### 🧩 卡片 1：交易树基础

| 英文 | 中文 | 释义 |
|------|------|------|
| **Transaction Trie** | 交易树 | 每个区块包含的 Merkle Patricia Tree，组织该区块内的所有交易。树的根哈希存储在区块头的 transactionsRoot 字段 |
| **Transaction Index** | 交易索引 | 交易在区块中的位置序号（0, 1, 2, ...），作为交易树的键。通过索引可以快速定位和验证特定交易 |
| **Transaction Hash (txHash)** | 交易哈希 | 交易数据的 Keccak-256 哈希，作为交易的唯一标识符。用户通过 txHash 查询交易状态 |
| **Transactions Root** | 交易根 | 交易树的根哈希，存储在区块头中。代表该区块所有交易的密码学摘要 |

**核心理解**：交易树记录"发生了什么"——区块中包含哪些交易。它是输入的记录。

---

### 🧩 卡片 2：Merkle 证明应用

| 英文 | 中文 | 释义 |
|------|------|------|
| **Merkle Proof** | 默克尔证明 | 证明某笔交易存在于区块中的密码学证明。只需提供从叶子到根的路径上的兄弟节点哈希，验证复杂度为 O(log n) |
| **Light Client** | 轻客户端 | 只下载区块头的节点，通过 Merkle 证明验证交易和状态，无需下载完整区块链数据 |
| **SPV (Simplified Payment Verification)** | 简化支付验证 | 比特币白皮书提出的轻客户端验证方法。以太坊的轻客户端使用类似原理，通过 Merkle 证明验证交易 |
| **Proof Size** | 证明大小 | Merkle 证明的数据量。对于包含 n 笔交易的区块，证明大小约为 O(log n)，通常几百字节到几 KB |

**验证流程**：
1. 轻客户端请求交易的 Merkle 证明
2. 全节点提供兄弟节点哈希
3. 轻客户端重建路径，计算根哈希
4. 与区块头中的 transactionsRoot 对比

---

### 🧩 卡片 3：收据树基础

| 英文 | 中文 | 释义 |
|------|------|------|
| **Receipt Trie** | 收据树 | 记录每笔交易执行结果的 Merkle Patricia Tree，与交易树平行。树的根哈希存储在区块头的 receiptsRoot 字段 |
| **Transaction Receipt** | 交易收据 | 记录交易执行后的结果，包括 status（成功/失败）、gasUsed（消耗的 Gas）、logs（事件日志）、contractAddress（新创建的合约地址）等信息 |
| **Receipts Root** | 收据根 | 收据树的根哈希，存储在区块头中。代表该区块所有交易执行结果的密码学摘要 |
| **Receipt Index** | 收据索引 | 收据在区块中的位置序号，与交易索引一一对应。第 i 笔交易的收据存储在收据树的第 i 个位置 |

**核心理解**：收据树记录"结果是什么"——每笔交易执行后的状态。它是输出的记录。

---

### 🧩 卡片 4：交易收据字段

| 英文 | 中文 | 释义 |
|------|------|------|
| **Status** | 状态码 | 交易执行结果：1 表示成功，0 表示失败回滚。失败的交易仍会被打包上链，已消耗的 Gas 不退还 |
| **Gas Used** | 已用 Gas | 该笔交易实际消耗的 Gas 数量。如果交易失败，Gas 仍会被消耗（直到失败点） |
| **Cumulative Gas Used** | 累计 Gas 消耗 | 区块中从第一笔交易到当前交易累计消耗的 Gas 总量。用于计算区块的总 Gas 消耗 |
| **Logs Bloom** | 日志布隆过滤器 | 该笔交易触发的所有事件日志的布隆过滤器。用于快速判断某个地址或 topic 是否可能在日志中 |
| **Logs** | 日志数组 | 交易执行过程中触发的所有事件日志。每个日志包含 address、topics、data 字段 |
| **Contract Address** | 合约地址 | 如果交易是合约创建，此字段包含新创建的合约地址；否则为 null |

---

### 🧩 卡片 5：事件与日志

| 英文 | 中文 | 释义 |
|------|------|------|
| **Event** | 事件 | 智能合约通过 emit 关键字触发的日志记录，用于通知链外应用合约状态的重要变化（如转账、状态更新） |
| **Log** | 日志 | 事件的底层实现，存储在交易收据中。包含 address（合约地址）、topics（索引参数）、data（非索引参数） |
| **emit** | 触发/发出 | Solidity 中触发事件的关键字。例如：emit Transfer(from, to, amount) |
| **Event Signature** | 事件签名 | 事件名和参数类型的字符串表示，如 "Transfer(address,address,uint256)"。其 Keccak-256 哈希作为 topics[0] |

**核心理解**：事件是智能合约与链外世界通信的主要方式。合约代码无法读取日志，但链外应用可以监听事件。

---

### 🧩 卡片 6：日志结构

| 英文 | 中文 | 释义 |
|------|------|------|
| **Log Entry** | 日志条目 | 单个事件日志的完整记录，包含 address、topics、data 三个核心字段 |
| **Address** | 合约地址 | 触发该事件的合约地址。用于过滤特定合约的事件 |
| **Topics** | 主题数组 | 索引参数数组（最多 4 个）。topics[0] 是事件签名的 Keccak-256 哈希，topics[1-3] 是标记为 indexed 的参数 |
| **Data** | 数据字段 | 非索引参数的 ABI 编码。包含事件的详细信息，但不能用于快速过滤 |
| **Indexed Parameter** | 索引参数 | 在事件定义中标记为 indexed 的参数，会被放入 topics 数组。最多 3 个索引参数（topics[0] 保留给事件签名） |

**示例**：
```solidity
event Transfer(address indexed from, address indexed to, uint256 value);
```
- topics[0]: keccak256("Transfer(address,address,uint256)")
- topics[1]: from 地址
- topics[2]: to 地址
- data: value（ABI 编码）

---

### 🧩 卡片 7：布隆过滤器

| 英文 | 中文 | 释义 |
|------|------|------|
| **Bloom Filter** | 布隆过滤器 | 概率型数据结构，用于快速判断某个元素是否可能在集合中。可能误报（false positive）但不会漏报（no false negative） |
| **Logs Bloom** | 日志布隆过滤器 | 每个收据和区块头都包含的 2048 位（256 字节）布隆过滤器，记录该交易/区块中所有日志的地址和 topics |
| **False Positive** | 假阳性/误报 | 布隆过滤器判断元素存在，但实际不存在。需要进一步检查确认 |
| **False Negative** | 假阴性/漏报 | 布隆过滤器判断元素不存在，实际也确实不存在。布隆过滤器不会漏报 |
| **Hash Functions** | 哈希函数 | 布隆过滤器使用多个哈希函数将元素映射到位数组。以太坊的 Logs Bloom 使用 3 个哈希函数 |

**工作原理**：
1. 插入：对地址/topic 做 3 次哈希，将对应位设为 1
2. 查询：对目标做 3 次哈希，检查对应位是否都为 1
3. 如果有任何位为 0，元素肯定不存在
4. 如果所有位都为 1，元素可能存在（需进一步确认）

---

### 🧩 卡片 8：事件过滤与检索

| 英文 | 中文 | 释义 |
|------|------|------|
| **Event Filtering** | 事件过滤 | 根据合约地址、topics 等条件筛选事件日志。DApp 通过事件过滤监听合约状态变化 |
| **Topic Filter** | 主题过滤器 | 指定要查询的 topics 值。可以使用 null 作为通配符，匹配任意值 |
| **Block Range** | 区块范围 | 指定查询事件的区块范围，如 fromBlock: 1000000, toBlock: 1000100 |
| **eth_getLogs** | 获取日志 RPC | 以太坊 JSON-RPC 方法，用于查询符合条件的事件日志。返回匹配的日志数组 |

**过滤示例**：
```javascript
{
  address: "0x1234...",  // 合约地址
  topics: [
    "0xddf2...",         // Transfer 事件签名
    null,                // from（任意）
    "0x5678..."          // to（指定地址）
  ],
  fromBlock: 1000000,
  toBlock: "latest"
}
```

---

### 🧩 卡片 9：三棵树的协同

| 英文 | 中文 | 释义 |
|------|------|------|
| **Block Header** | 区块头 | 包含三个根哈希：stateRoot（状态树）、transactionsRoot（交易树）、receiptsRoot（收据树），共同确保区块数据完整性 |
| **State Root** | 状态根 | 执行完所有交易后的全局状态树根哈希。代表"现在是什么样" |
| **Transactions Root** | 交易根 | 该区块所有交易组成的交易树根哈希。代表"发生了什么" |
| **Receipts Root** | 收据根 | 所有交易收据组成的收据树根哈希。代表"结果是什么" |

**三棵树的分工**：
- 状态树：当前状态（账户余额、合约存储）
- 交易树：输入（交易内容）
- 收据树：输出（执行结果、事件日志）

---

### 🧩 卡片 10：轻客户端验证能力

| 英文 | 中文 | 释义 |
|------|------|------|
| **Header-only Sync** | 仅同步区块头 | 轻客户端只下载区块头（约 500 字节/块），不下载完整区块数据 |
| **On-demand Verification** | 按需验证 | 轻客户端需要时向全节点请求 Merkle 证明，验证特定交易或状态 |
| **Trust Minimization** | 信任最小化 | 轻客户端无需信任全节点，通过密码学证明（Merkle 证明）验证数据真实性 |
| **Proof Request** | 证明请求 | 轻客户端向全节点请求 Merkle 证明的 RPC 调用，如 eth_getProof |

**轻客户端可验证**：
- 交易是否在区块中（交易树证明）
- 交易执行结果（收据树证明）
- 账户余额（状态树证明）
- 合约存储值（存储树证明）

---

### 🧩 卡片 11：同步策略

| 英文 | 中文 | 释义 |
|------|------|------|
| **Full Sync** | 完全同步 | 从创世区块开始重放所有交易，重建完整状态树。验证最彻底但耗时最长（数周） |
| **Fast Sync** | 快速同步 | 只下载最近状态和区块头，不重放历史交易。通过状态树根哈希验证状态正确性，大幅加快同步速度（数小时） |
| **Snap Sync** | 快照同步 | 以太坊最新的同步策略，先下载状态快照再同步增量数据。是目前最快的同步方式（数小时） |
| **Warp Sync** | 扭曲同步 | Parity/OpenEthereum 客户端的快速同步方法，类似 Fast Sync |
| **Checkpoint Sync** | 检查点同步 | 从可信检查点开始同步，跳过早期历史。用于 PoS 信标链的快速同步 |

**同步速度对比**：
- Full Sync: 数周
- Fast Sync: 数小时到 1 天
- Snap Sync: 数小时

---

### 🧩 卡片 12：区块头结构

| 英文 | 中文 | 释义 |
|------|------|------|
| **Parent Hash** | 父区块哈希 | 前一个区块的哈希，形成区块链 |
| **Uncle Hash** | 叔父块哈希 | 该区块包含的叔父块的哈希（以太坊特有） |
| **Beneficiary** | 受益人 | 接收区块奖励的矿工地址（PoW）或验证者地址（PoS） |
| **Difficulty** | 难度 | PoW 挖矿难度目标 |
| **Number** | 区块号 | 区块高度，从 0（创世区块）开始递增 |
| **Gas Limit** | Gas 上限 | 该区块允许的最大 Gas 消耗量 |
| **Gas Used** | 已用 Gas | 该区块实际消耗的 Gas 总量 |
| **Timestamp** | 时间戳 | 区块创建时间（Unix 时间戳） |
| **Extra Data** | 额外数据 | 矿工可以包含的任意数据（最多 32 字节） |
| **Mix Hash** | 混合哈希 | PoW 挖矿的中间值（Ethash 特有） |
| **Nonce** | 随机数 | PoW 挖矿的随机数 |

---

## 🔐 综合词汇速查表 | Quick Reference

| 英文术语 | 中文 | 核心关键词 |
|----------|------|-----------|
| Transaction Trie | 交易树 | 区块交易组织 |
| Transaction Index | 交易索引 | 位置序号 |
| Transaction Hash | 交易哈希 | 唯一标识符 |
| Transactions Root | 交易根 | 区块头字段 |
| Merkle Proof | 默克尔证明 | 存在性证明 |
| Light Client | 轻客户端 | 只下载区块头 |
| SPV | 简化支付验证 | 轻量级验证 |
| Receipt Trie | 收据树 | 执行结果记录 |
| Transaction Receipt | 交易收据 | 执行结果 |
| Receipts Root | 收据根 | 区块头字段 |
| Status | 状态码 | 成功/失败 |
| Gas Used | 已用 Gas | 实际消耗 |
| Cumulative Gas Used | 累计 Gas | 区块总消耗 |
| Logs Bloom | 日志布隆过滤器 | 快速检索 |
| Logs | 日志数组 | 事件记录 |
| Contract Address | 合约地址 | 新创建合约 |
| Event | 事件 | 合约日志 |
| Log | 日志 | 事件底层实现 |
| emit | 触发 | Solidity 关键字 |
| Event Signature | 事件签名 | 函数名+参数 |
| Log Entry | 日志条目 | 单个日志 |
| Address | 合约地址 | 触发者 |
| Topics | 主题数组 | 索引参数 |
| Data | 数据字段 | 非索引参数 |
| Indexed Parameter | 索引参数 | 可过滤参数 |
| Bloom Filter | 布隆过滤器 | 概率数据结构 |
| False Positive | 假阳性 | 可能误报 |
| Event Filtering | 事件过滤 | 条件筛选 |
| Block Header | 区块头 | 三个根哈希 |
| Full Sync | 完全同步 | 重放所有交易 |
| Fast Sync | 快速同步 | 下载最近状态 |
| Snap Sync | 快照同步 | 最快同步方式 |

---

## 💡 学习建议 | Study Tips

1. **三棵树的设计体现了以太坊的工程智慧**：
   - 交易树：记录"发生了什么"（输入）
   - 收据树：记录"结果是什么"（输出）
   - 状态树：记录"现在是什么样"（当前状态）

   三者分离使得轻客户端可以按需验证不同类型的数据，是以太坊可扩展性设计的重要组成部分。

2. **事件日志是 DApp 开发的核心**：智能合约通过事件与前端通信。理解 topics、bloom filter 和日志检索机制，是开发实用 DApp 的必备知识。

3. **布隆过滤器的权衡**：
   - 优点：极快的查询速度，极小的存储空间
   - 缺点：可能误报，需要进一步确认
   - 应用：快速过滤掉大量不相关的区块，只对可能包含目标事件的区块做详细检查

4. **indexed vs 非 indexed 参数**：
   - indexed：放入 topics，可以快速过滤，但有数量限制（最多 3 个）
   - 非 indexed：放入 data，可以包含任意数据，但不能用于过滤

   设计事件时需要权衡：哪些参数需要快速检索？

5. **轻客户端的重要性**：轻客户端使得移动设备、浏览器钱包等资源受限环境也能安全地使用以太坊。理解 Merkle 证明是理解轻客户端的关键。

6. **同步策略的演进**：
   - Full Sync：最安全但最慢
   - Fast Sync：平衡安全性和速度
   - Snap Sync：最快，是当前主流

   理解不同同步策略的权衡，有助于选择合适的节点配置。

---

## 🔗 实用示例 | Practical Examples

### 事件定义与日志结构

**Solidity 事件定义**：
```solidity
event Transfer(
    address indexed from,
    address indexed to,
    uint256 value
);
```

**触发事件**：
```solidity
emit Transfer(msg.sender, recipient, amount);
```

**生成的日志**：
```json
{
  "address": "0x1234...",  // 合约地址
  "topics": [
    "0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef",  // Transfer 事件签名
    "0x000000000000000000000000abcd...",  // from（填充到 32 字节）
    "0x0000000000000000000000005678..."   // to（填充到 32 字节）
  ],
  "data": "0x0000000000000000000000000000000000000000000000000de0b6b3a7640000"  // value（100 * 10^18）
}
```

### 事件过滤查询

**查询特定地址的所有转入**：
```javascript
web3.eth.getPastLogs({
  address: tokenAddress,
  topics: [
    web3.utils.keccak256("Transfer(address,address,uint256)"),
    null,  // from（任意）
    web3.utils.padLeft(myAddress, 64)  // to（我的地址）
  ],
  fromBlock: 0,
  toBlock: "latest"
})
```

### Merkle 证明验证

**验证交易存在**：
```
1. 获取交易哈希: txHash
2. 获取 Merkle 证明: proof = [sibling1, sibling2, ...]
3. 重建路径:
   hash = txHash
   for each sibling in proof:
     hash = keccak256(hash + sibling)  // 或 sibling + hash
4. 验证: hash == transactionsRoot
```

---

## 📊 数据大小对比 | Data Size Comparison

### 不同节点类型的存储需求

| 节点类型 | 区块头 | 完整区块 | 状态数据 | 总存储 |
|---------|--------|---------|---------|--------|
| 轻节点 | ✓ | ✗ | ✗ | ~1 GB |
| 全节点（修剪） | ✓ | ✓ | ✓（当前） | ~500 GB |
| 全节点（未修剪） | ✓ | ✓ | ✓（当前） | ~800 GB |
| 归档节点 | ✓ | ✓ | ✓（所有历史） | ~12 TB |

### 单个区块的数据分布

| 组成部分 | 大小 | 占比 |
|---------|------|------|
| 区块头 | ~500 字节 | <1% |
| 交易数据 | ~50 KB | ~50% |
| 收据数据 | ~50 KB | ~50% |
| 总计 | ~100 KB | 100% |

*数据基于平均值，实际大小因区块而异*

---

## 🎯 关键要点总结 | Key Takeaways

1. **交易树 vs 收据树**：交易树记录输入，收据树记录输出。两者配合完整描述了交易的执行过程。

2. **事件日志的单向性**：合约可以写日志但不能读日志。日志是为链外应用设计的，不是为合约间通信设计的。

3. **布隆过滤器的妙用**：用 256 字节的布隆过滤器，可以快速过滤掉 99% 以上的不相关区块，大幅提升事件检索效率。

4. **轻客户端的安全性**：轻客户端通过 Merkle 证明实现信任最小化，无需信任全节点，只需信任数学和密码学。

5. **三个根哈希的完整性保证**：区块头中的三个根哈希（stateRoot、transactionsRoot、receiptsRoot）共同确保了区块数据的完整性和可验证性。

---

*更新日期 / Last Updated: 2026-03-18 | 课程：北大肖臻《区块链技术与应用》EP17*
