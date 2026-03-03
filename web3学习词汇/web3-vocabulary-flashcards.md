# 📚 Web3 每日英语词汇卡 | Daily Web3 English Vocabulary Cards

> 内容来源 / Source：北京大学肖臻老师《区块链技术与应用》公开课
> Bilibili 课程：[BV1Vt411X7JF](https://www.bilibili.com/video/BV1Vt411X7JF/)
> 掘金笔记参考：[第1讲密码学基础](https://juejin.cn/post/7496690671186509843) · [第2讲BTC密码学原理](https://juejin.cn/post/7579813925995675689) · [第3讲BTC数据结构(Hash Pointer&Blockchain)](https://juejin.cn/post/7579659550862508074) · [第3讲BTC数据结构(交易&区块)](https://juejin.cn/post/7579920818871205930)

---

## 📖 第一讲 & 第二讲：密码学原理 | Lecture 1 & 2: Cryptographic Principles

### 🧩 卡片 1

| 英文 | 中文 | 释义 |
|------|------|------|
| **Hash Function** | 哈希函数 | 将任意长度输入映射为固定长度输出的函数 |
| **Hash Value / Digest** | 哈希值 / 摘要 | 哈希函数的输出结果，用于唯一标识数据 |
| **Hash Collision** | 哈希碰撞 | 两个不同输入经过哈希函数得到相同输出的情况 |
| **Collision Resistance** | 抗碰撞性 | 哈希函数的核心安全属性：极难找到两个不同输入有相同哈希 |

**记忆口诀**：哈希函数像"指纹机"——无论原文多长，都压缩成固定长度的"数据指纹"

---

### 🧩 卡片 2

| 英文 | 中文 | 释义 |
|------|------|------|
| **Preimage Resistance** | 原像抵抗 / 单向性 | 给定 H(x)，计算上不可能还原出 x |
| **Second Preimage Resistance** | 第二原像抵抗 | 给定 x₁ 和 H(x₁)，极难找出 x₂ ≠ x₁ 使得 H(x₁)=H(x₂) |
| **Avalanche Effect** | 雪崩效应 | 输入微小改动（哪怕1 bit）导致输出完全不同 |
| **One-way Function** | 单向函数 | 正向计算容易，逆向推导几乎不可能的函数 |

**记忆技巧**：Avalanche = 雪崩 → "雪崩效应"一改全变

---

### 🧩 卡片 3：SHA-256

| 英文 | 中文 | 释义 |
|------|------|------|
| **SHA-256** | SHA-256 算法 | Secure Hash Algorithm 256-bit，比特币使用的核心哈希算法 |
| **Secure Hash Algorithm (SHA)** | 安全哈希算法 | 由美国 NSA 设计的哈希算法系列 |
| **Nonce** | 随机数 / 一次性数 | 挖矿时不断尝试的随机值，满足难度目标则成功出块 |
| **Target** | 难度目标 | 哈希结果必须小于此值，决定挖矿难度 |
| **Proof of Work (PoW)** | 工作量证明 | 通过大量计算（找 nonce）来证明做了足够工作 |

**核心公式**：`SHA256(SHA256(BlockHeader)) < Target` → 挖矿成功 🎉

---

### 🧩 卡片 4：公钥密码体系

| 英文 | 中文 | 释义 |
|------|------|------|
| **Public Key Cryptography** | 公钥密码学 | 使用一对密钥（公钥+私钥）进行加密和验签的密码体系 |
| **Public Key** | 公钥 | 可以公开给所有人，用于验证签名 |
| **Private Key** | 私钥 | 需要严格保密，用于生成数字签名 |
| **Key Pair** | 密钥对 | 公钥和私钥合称为密钥对，数学上紧密关联 |
| **Asymmetric Encryption** | 非对称加密 | 加密和解密使用不同密钥的加密方式 |

**类比**：私钥 = 你的"印章+保险柜密码"，公钥 = 你的"公开身份信息"

---

### 🧩 卡片 5：数字签名

| 英文 | 中文 | 释义 |
|------|------|------|
| **Digital Signature** | 数字签名 | 用私钥对数据进行数学运算生成的签名，可被公钥验证 |
| **Sign / Signing** | 签名 | 用私钥对交易内容进行签署的动作 |
| **Verify / Verification** | 验证 | 用公钥检验签名是否有效的过程 |
| **Non-repudiation** | 不可否认性 | 签名者事后不能否认自己发起过这笔交易 |
| **Authentication** | 身份认证 | 证明"是你本人"发起了这个操作 |
| **Forgery** | 伪造 | 没有私钥就无法伪造有效的数字签名 |

---

### 🧩 卡片 6：比特币地址

| 英文 | 中文 | 释义 |
|------|------|------|
| **Bitcoin Address** | 比特币地址 | 公钥经过多次哈希和编码得到的短字符串，相当于"收款账号" |
| **Wallet** | 钱包 | 存储私钥并管理地址的软件/硬件工具 |
| **Elliptic Curve Cryptography (ECC)** | 椭圆曲线密码学 | 比特币生成公私钥对所使用的数学基础 |
| **Base58Check encoding** | Base58 编码 | 比特币地址的编码格式，去掉易混淆字符（0/O/I/l） |
| **RIPEMD-160** | RIPEMD-160 算法 | 对公钥做哈希压缩时使用的算法之一 |

**地址生成流程**：`私钥 → 公钥 (ECC) → SHA256 → RIPEMD-160 → Base58Check → 地址`

---

## 📖 第三讲：比特币数据结构 | Lecture 3: Bitcoin Data Structures

### 🧩 卡片 7：区块链基本结构

| 英文 | 中文 | 释义 |
|------|------|------|
| **Blockchain** | 区块链 | 通过哈希指针将多个区块串联成链的数据结构 |
| **Block** | 区块 | 区块链的基本单元，包含一批交易数据 |
| **Hash Pointer** | 哈希指针 | 不仅包含数据地址，还包含该数据哈希值的特殊指针 |
| **Linked List** | 链表 | 区块链结构上类似链表，但使用哈希指针连接 |
| **Immutability** | 不可篡改性 | 一旦写入区块链，数据极难被修改 |
| **Decentralization** | 去中心化 | 没有单一控制机构，由分布式节点共同维护 |

---

### 🧩 卡片 8

| 英文 | 中文 | 释义 |
|------|------|------|
| **Genesis Block** | 创世区块 | 区块链中的第一个区块，整条链的起点，硬编码在系统中 |
| **Most Recent Block** | 最新区块 | 链上当前最末尾的区块，也叫 HEAD block |
| **Block Height** | 区块高度 | 某区块距创世区块的区块数量（创世区块高度为 0） |
| **Tamper-evident Log** | 可检测篡改日志 | 一种数据结构，任何人修改历史记录都能被检测出来 |
| **Distributed Ledger** | 分布式账本 | 在多个节点上同步保存的账本 |

**记忆技巧**：Genesis = 起源（《圣经》创世记）→ 创世区块 = 链的"起点"

---

### 🧩 卡片 9：区块结构

| 英文 | 中文 | 释义 |
|------|------|------|
| **Block Header** | 区块头 | 包含区块元数据：前块哈希、Merkle 根、时间戳、难度值、Nonce |
| **Block Body** | 区块体 | 包含该区块打包的所有交易数据列表 |
| **Version** | 版本号 | 区块头字段，标识软件协议版本 |
| **Timestamp** | 时间戳 | 区块头字段，记录该区块被创建的大致时间 |
| **Difficulty Target** | 难度目标 | 区块头字段，当前出块需要满足的哈希难度 |
| **Previous Block Hash** | 前块哈希 | 区块头字段，指向上一个区块，形成哈希链 |

---

### 🧩 卡片 10：Merkle 树

| 英文 | 中文 | 释义 |
|------|------|------|
| **Merkle Tree** | 默克尔树 | 一种二叉树结构，叶子是数据哈希，上层是子节点哈希的哈希 |
| **Merkle Root** | 默克尔根 / 根哈希 | 默克尔树最顶层节点的哈希值，存储在区块头中 |
| **Leaf Node** | 叶子节点 | 默克尔树最底层节点，存储每笔交易的哈希 |
| **Binary Tree** | 二叉树 | 每个节点最多有两个子节点的树结构 |
| **Root Hash** | 根哈希 | 代表整个数据集的唯一哈希值 |
| **Sibling Node** | 兄弟节点 | Merkle 证明中，与目标节点同层的配对节点 |

**核心用途**：用一个固定长度的根哈希"代表"区块中所有交易，高效验证数据完整性

---

### 🧩 卡片 11：Merkle 证明

| 英文 | 中文 | 释义 |
|------|------|------|
| **Merkle Proof** | 默克尔证明 | 证明某条数据是否在 Merkle 树中，只需提供从叶到根的哈希路径 |
| **Proof of Membership** | 成员证明 | 证明"某条数据在集合中" |
| **Proof of Inclusion** | 包含证明 | 与成员证明同义，证明数据被包含在集合中 |
| **Proof of Non-Membership** | 非包含证明 | 证明"某条数据不在集合中"（需要 Sorted Merkle Tree 或 MPT） |
| **Light Client** | 轻节点 / 轻客户端 | 只存储区块头、通过 Merkle Proof 验证交易的节点 |
| **Merkle Patricia Trie (MPT)** | 默克尔帕特里夏树 | 以太坊使用的改进树结构，支持非包含证明 |

**效率优势**：Merkle Proof 的长度仅为 O(log N)，N 笔交易只需 log₂N 个哈希即可验证

---

### 🧩 卡片 12：交易数据结构

| 英文 | 中文 | 释义 |
|------|------|------|
| **Transaction (TX)** | 交易 | 比特币网络中的基本操作单元，记录转账信息 |
| **UTXO** | 未花费交易输出 | Unspent Transaction Output，比特币系统中的"余额"表示方式 |
| **Transaction Input (TxIn)** | 交易输入 | 引用一个之前未花费的 UTXO 作为资金来源 |
| **Transaction Output (TxOut)** | 交易输出 | 指定接收方地址和金额 |
| **Locking Script** | 锁定脚本 | 定义"谁能花这笔钱"的条件（即接收方条件） |
| **Unlocking Script** | 解锁脚本 | 证明"我有权花这笔钱"的脚本（通常包含签名） |
| **Change Output** | 找零输出 | 交易中多余的金额返回给发送方自己的地址 |
| **Transaction ID (TxID)** | 交易 ID | 对整笔交易进行哈希后得到的唯一标识符 |

**核心规则**：一个 UTXO 只能被花费一次，这从根本上防止了双花攻击

---

### 🧩 卡片 13：网络与节点

| 英文 | 中文 | 释义 |
|------|------|------|
| **Node** | 节点 | 参与区块链网络的计算机（钱包/矿工/验证者等） |
| **Full Node** | 全节点 | 存储完整区块链数据并独立验证所有交易的节点 |
| **Miner** | 矿工 | 通过计算 PoW 来打包交易并争夺出块奖励的节点 |
| **Broadcasting** | 广播 | 将交易/区块信息发送给网络中所有节点的过程 |
| **Peer-to-Peer (P2P)** | 点对点 | 无中心服务器、节点之间直接通信的网络架构 |
| **Consensus** | 共识 | 分布式网络中所有节点对同一状态达成一致的机制 |
| **Double Spending** | 双花攻击 | 尝试将同一笔比特币花费两次的攻击行为 |

---

## 🔐 综合词汇速查表 | Quick Reference

| 英文术语 | 中文 | 核心关键词 |
|----------|------|----------|
| Hash Function | 哈希函数 | 固定长度输出、不可逆 |
| Collision Resistance | 抗碰撞性 | 安全性基础 |
| Preimage Resistance | 原像抵抗 | 单向性 |
| Avalanche Effect | 雪崩效应 | 微小改动→大变化 |
| SHA-256 | 安全哈希算法256位 | 比特币核心算法 |
| Nonce | 随机数 | 挖矿关键变量 |
| Proof of Work (PoW) | 工作量证明 | 挖矿算法 |
| Public Key | 公钥 | 可公开 |
| Private Key | 私钥 | 严格保密 |
| Digital Signature | 数字签名 | 身份认证 |
| Non-repudiation | 不可否认性 | 签名法律效力 |
| Bitcoin Address | 比特币地址 | 收款账号 |
| Blockchain | 区块链 | 哈希链式结构 |
| Block Header | 区块头 | 元数据 |
| Block Body | 区块体 | 交易列表 |
| Genesis Block | 创世区块 | 链的起点 |
| Hash Pointer | 哈希指针 | 防篡改指针 |
| Tamper-evident Log | 可检测篡改日志 | 区块链本质 |
| Merkle Tree | 默克尔树 | 二叉哈希树 |
| Merkle Root | 默克尔根 | 写入区块头 |
| Merkle Proof | 默克尔证明 | O(logN) 验证 |
| Proof of Membership | 成员证明 | 数据存在证明 |
| Proof of Non-Membership | 非包含证明 | 数据不存在证明 |
| Light Client | 轻节点 | 只验证区块头 |
| UTXO | 未花费交易输出 | 比特币余额模型 |
| Transaction (TX) | 交易 | 基本操作单元 |
| Double Spending | 双花攻击 | 安全威胁 |
| Consensus | 共识 | 分布式一致性 |
| P2P Network | 点对点网络 | 去中心化通信 |
| Decentralization | 去中心化 | 无单一控制者 |

---

## 💡 学习建议 | Study Tips

1. **每日 3 张卡**：每天专注学习 3 张词汇卡，反复复习效果更好
2. **造句练习**：用英文描述一个你学到的概念，强化记忆
3. **联系上下文**：每个词汇都在具体的比特币场景中理解，避免孤立记忆
4. **拓展阅读**：掌握基础词汇后，尝试阅读比特币白皮书英文原版 [Bitcoin Whitepaper](https://bitcoin.org/bitcoin.pdf)

---

*更新日期 / Last Updated: 2026-03-03 | 课程：北大肖臻《区块链技术与应用》EP1-EP3*
