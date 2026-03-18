# 📚 Web3 每日英语词汇卡 | Daily Web3 English Vocabulary Cards

> 内容来源 / Source：北京大学肖臻老师《区块链技术与应用》公开课
> Bilibili 课程：[BV1Vt411X7JF](https://www.bilibili.com/video/BV1Vt411X7JF/?p=15)
> 第十五讲内容：ETH 账户 (Ethereum Accounts)

---

## 📖 第十五讲：以太坊账户 | Lecture 15: Ethereum Accounts

### 🧩 卡片 1：账户类型

| 英文 | 中文 | 释义 |
|------|------|------|
| **EOA (Externally Owned Account)** | 外部账户 | 由私钥控制的账户，类似比特币地址。可以发起交易、转账 ETH、调用合约，但不包含代码 |
| **Contract Account** | 合约账户 | 由智能合约代码控制的账户，没有私钥。只能被外部交易或其他合约调用触发，不能主动发起交易 |
| **Account** | 账户 | 以太坊中的基本实体，包含余额和状态。与比特币的 UTXO 模型不同，以太坊采用账户模型 |
| **Address** | 地址 | 以太坊账户的唯一标识符，160 位（20 字节）十六进制字符串，以 0x 开头。EOA 地址由公钥哈希生成，合约地址由创建者地址和 nonce 计算得出 |

**核心理解**：以太坊有两种账户类型，EOA 由人控制，合约账户由代码控制。这种双账户设计是智能合约平台的基础。

---

### 🧩 卡片 2：账户状态结构

| 英文 | 中文 | 释义 |
|------|------|------|
| **Balance** | 余额 | 账户拥有的以太币数量，以 Wei 为最小单位（1 ETH = 10^18 Wei）。每次转账或 Gas 消耗都会更新余额 |
| **Nonce** | 交易序号 | EOA 的 nonce 记录该账户发送的交易总数，防止重放攻击；合约的 nonce 记录该合约创建的合约数量 |
| **Storage Root** | 存储根 | 账户存储树（Storage Trie）的根哈希，指向合约的持久化存储数据。EOA 此字段为空 |
| **Code Hash** | 代码哈希 | 合约账户的代码哈希值。合约部署后代码不可修改，因此代码哈希是不可变的。EOA 此字段为空哈希 |
| **Wei** | Wei | 以太币的最小单位，1 ETH = 10^18 Wei。命名来自密码学先驱戴伟（Wei Dai） |
| **Ether (ETH)** | 以太币 | 以太坊的原生加密货币，用于支付交易费用（Gas）和作为价值存储 |

**核心理解**：以太坊账户状态由四个字段完整定义：Balance、Nonce、StorageRoot、CodeHash。这四个字段的组合决定了账户在任意时刻的完整状态。

---

### 🧩 卡片 3：密钥与地址生成

| 英文 | 中文 | 释义 |
|------|------|------|
| **Private Key** | 私钥 | 256 位随机数，控制 EOA 账户的唯一凭证。通过椭圆曲线算法（secp256k1）生成对应的公钥和地址 |
| **Public Key** | 公钥 | 由私钥通过椭圆曲线算法生成的 512 位数字。公钥可以公开，用于验证签名 |
| **Keccak-256** | Keccak-256 哈希 | 以太坊使用的哈希算法（SHA-3 的前身）。EOA 地址是公钥 Keccak-256 哈希的后 20 字节 |
| **secp256k1** | secp256k1 椭圆曲线 | 以太坊和比特币使用的椭圆曲线加密算法，用于从私钥生成公钥和数字签名 |
| **Checksum Address** | 校验和地址 | EIP-55 提案的地址格式，通过大小写混合编码校验和，防止地址输入错误。例如 0x5aAeb6053F3E94C9b9A09f33669435E7Ef1BeAed |

**地址生成流程**：
1. 生成 256 位随机私钥
2. 通过 secp256k1 生成 512 位公钥
3. 对公钥做 Keccak-256 哈希
4. 取哈希结果的后 20 字节作为地址

---

### 🧩 卡片 4：交易类型

| 英文 | 中文 | 释义 |
|------|------|------|
| **Transaction** | 交易 | 由 EOA 签名并广播的状态改变请求。包含 from、to、value、data、gasLimit、gasPrice、nonce 等字段 |
| **Message Call** | 消息调用 | 合约之间的内部调用，不是交易。通过 CALL、DELEGATECALL、STATICCALL 等操作码触发 |
| **Contract Creation** | 合约创建 | to 字段为空（null）的特殊交易，data 字段包含合约初始化代码（constructor）和字节码。成功后返回新创建的合约地址 |
| **Value Transfer** | 价值转移 | 普通的 ETH 转账交易，to 字段指向接收方地址，value 字段指定转账金额，data 字段为空 |

---

### 🧩 卡片 5：交易字段详解

| 英文 | 中文 | 释义 |
|------|------|------|
| **from** | 发送方 | 交易发起者的 EOA 地址，由签名推导得出（不在交易数据中显式包含） |
| **to** | 接收方 | 目标地址。如果是合约调用则为合约地址，如果是合约创建则为 null |
| **value** | 转账金额 | 随交易转移的 ETH 数量（以 Wei 为单位） |
| **data** | 数据/输入 | 附加数据。合约调用时包含函数选择器和参数；合约创建时包含初始化代码；普通转账时为空 |
| **gasLimit** | Gas 限制 | 该交易允许消耗的最大 Gas 数量 |
| **gasPrice** | Gas 价格 | 每单位 Gas 的价格（以 Wei 为单位） |
| **nonce** | 序号 | 发送方账户的交易计数器，确保交易顺序执行，防止重放攻击 |
| **v, r, s** | 签名参数 | ECDSA 签名的三个组成部分，用于验证交易的真实性和完整性 |

---

### 🧩 卡片 6：合约调用机制

| 英文 | 中文 | 释义 |
|------|------|------|
| **Function Selector** | 函数选择器 | 函数签名的 Keccak-256 哈希的前 4 字节，用于标识要调用的合约函数。例如 transfer(address,uint256) 的选择器是 0xa9059cbb |
| **Function Signature** | 函数签名 | 函数名和参数类型的字符串表示，如 "transfer(address,uint256)"。注意参数类型之间没有空格 |
| **ABI (Application Binary Interface)** | 应用二进制接口 | 定义如何与智能合约交互的标准，包括函数签名、参数类型、返回值等。类似于 API 但用于二进制层面 |
| **ABI Encoding** | ABI 编码 | 将函数调用参数编码为字节序列的规则。以太坊使用严格的编码规范确保跨语言兼容性 |

---

### 🧩 卡片 7：合约地址生成

| 英文 | 中文 | 释义 |
|------|------|------|
| **CREATE** | CREATE 操作码 | 标准的合约创建操作码。合约地址 = keccak256(RLP(sender_address, nonce)) 的后 20 字节 |
| **CREATE2** | CREATE2 操作码 | EIP-1014 引入的新合约创建操作码，允许通过 salt 参数生成可预测的合约地址。地址 = keccak256(0xff, sender, salt, keccak256(init_code)) 的后 20 字节 |
| **Salt** | 盐值 | CREATE2 中的 256 位参数，用于生成确定性地址。相同的 sender、salt 和 init_code 总是生成相同的合约地址 |
| **Deterministic Address** | 确定性地址 | 可以在部署前预先计算的合约地址。CREATE2 使得状态通道、工厂合约等高级模式成为可能 |

**CREATE vs CREATE2**：
- CREATE：地址依赖 nonce，无法预测
- CREATE2：地址依赖 salt，可以预测

---

### 🧩 卡片 8：调用类型

| 英文 | 中文 | 释义 |
|------|------|------|
| **CALL** | CALL 操作码 | 标准的合约调用，在目标合约的上下文中执行。msg.sender 是调用者，存储修改发生在目标合约 |
| **DELEGATECALL** | DELEGATECALL 操作码 | 委托调用，在调用者的上下文中执行目标合约代码。msg.sender 保持不变，存储修改发生在调用者合约。常用于代理模式和库 |
| **STATICCALL** | STATICCALL 操作码 | 静态调用，保证不修改状态。如果被调用代码尝试修改状态，调用会失败。用于只读操作 |
| **CALLCODE** | CALLCODE 操作码 | 已废弃的操作码，类似 DELEGATECALL 但 msg.sender 会改变。不推荐使用 |

**核心理解**：
- CALL：我调用你，在你的地盘执行
- DELEGATECALL：我借用你的代码，在我的地盘执行
- STATICCALL：我只看不改

---

## 🔐 综合词汇速查表 | Quick Reference

| 英文术语 | 中文 | 核心关键词 |
|----------|------|-----------|
| EOA | 外部账户 | 私钥控制 |
| Contract Account | 合约账户 | 代码控制 |
| Account | 账户 | 基本实体 |
| Address | 地址 | 160 位标识符 |
| Balance | 余额 | Wei 单位 |
| Nonce | 交易序号 | 防重放攻击 |
| Storage Root | 存储根 | 合约存储树根 |
| Code Hash | 代码哈希 | 合约代码哈希 |
| Wei | Wei | 最小单位 |
| Ether (ETH) | 以太币 | 原生货币 |
| Private Key | 私钥 | 256 位密钥 |
| Public Key | 公钥 | 512 位密钥 |
| Keccak-256 | Keccak-256 | 以太坊哈希算法 |
| secp256k1 | secp256k1 | 椭圆曲线算法 |
| Checksum Address | 校验和地址 | EIP-55 格式 |
| Transaction | 交易 | 状态改变请求 |
| Message Call | 消息调用 | 合约内部调用 |
| Contract Creation | 合约创建 | 部署新合约 |
| Value Transfer | 价值转移 | ETH 转账 |
| Function Selector | 函数选择器 | 前 4 字节哈希 |
| Function Signature | 函数签名 | 函数名+参数类型 |
| ABI | 应用二进制接口 | 交互标准 |
| CREATE | CREATE 操作码 | 标准创建 |
| CREATE2 | CREATE2 操作码 | 可预测地址 |
| Salt | 盐值 | 确定性参数 |
| CALL | CALL 操作码 | 标准调用 |
| DELEGATECALL | DELEGATECALL | 委托调用 |
| STATICCALL | STATICCALL | 静态调用 |

---

## 💡 学习建议 | Study Tips

1. **账户模型 vs UTXO 模型**：
   - 以太坊账户模型：直观、适合智能合约，但有状态爆炸问题
   - 比特币 UTXO 模型：隐私性好、并行验证，但不适合复杂逻辑

   理解两种模型的权衡是掌握区块链设计的基础。

2. **四字段定义账户状态**：记住 Balance、Nonce、StorageRoot、CodeHash 这四个字段，它们完整定义了以太坊账户的状态。

3. **EOA vs 合约账户的本质区别**：
   - EOA：有私钥，能主动发起交易
   - 合约账户：无私钥，只能被动响应

   这种设计使得智能合约既强大又安全。

4. **CALL vs DELEGATECALL 的关键区别**：
   - CALL：在目标合约的存储空间执行
   - DELEGATECALL：在调用者的存储空间执行

   理解这个区别对于掌握代理模式、可升级合约等高级模式至关重要。

5. **CREATE2 的革命性意义**：CREATE2 使得合约地址可预测，这为状态通道、反事实实例化（Counterfactual Instantiation）等 Layer 2 方案提供了基础。

---

## 🔗 实用示例 | Practical Examples

### EOA 地址生成示例

```
私钥: 0x1234567890abcdef...
↓ secp256k1
公钥: 0x04a1b2c3d4e5f6...（512位）
↓ Keccak-256
哈希: 0xabcdef1234567890...（256位）
↓ 取后20字节
地址: 0x1234567890abcdef1234567890abcdef12345678
```

### 函数选择器计算示例

```
函数签名: "transfer(address,uint256)"
↓ Keccak-256
哈希: 0xa9059cbb2ab09eb219583f4a59a5d0623ade346d962bcd4e46b11da047c9049b
↓ 取前4字节
选择器: 0xa9059cbb
```

### CREATE2 地址计算示例

```
地址 = keccak256(
  0xff,
  sender_address,
  salt,
  keccak256(init_code)
)[12:]  // 取后20字节
```

---

*更新日期 / Last Updated: 2026-03-18 | 课程：北大肖臻《区块链技术与应用》EP15*
