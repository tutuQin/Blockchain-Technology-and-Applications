密码学中的哈希函数、哈希碰撞、抗碰撞性（collision resistance）以及比特币中使用的 SHA-256 的简明介绍：

---

### 🧩 一、哈希函数（Hash Function）

**定义：**  
哈希函数是一种将任意长度的输入（消息）映射为固定长度输出（哈希值，digest）的函数。

**特点：**  
1. 输入可以是任意长度，输出固定长度（如256位）。
2. 相同输入总是得到相同的输出。
3. 不同输入得到相同输出的概率极低。
4. 哈希过程不可逆（不能从输出推回输入）。

---

### 🎯 二、哈希碰撞（Hash Collision）

**定义：**  
当两个不同的输入通过哈希函数得到了**相同的输出**时，就发生了**哈希碰撞（collision）**。

例子：
```text
H("hello") = 0x123456...
H("world") = 0x123456...  ← 碰撞
```

---

### 🛡️ 三、抗碰撞性（Collision Resistance）

**定义：**  
一个哈希函数是“抗碰撞的”，意味着要**找到两个不同的输入，使得它们哈希结果相同非常困难**（计算上不可行）。

哈希函数的安全性主要包括三个方面：
1. **Preimage Resistance（单向性）：** 给定 H(x)，难以找出 x。
2. **Second Preimage Resistance（第二原像抵抗）：** 给定 x1 和 H(x1)，难以找出 x2 ≠ x1 使得 H(x1) = H(x2)。
3. **Collision Resistance（抗碰撞性）：** 难以找到任何 x1 ≠ x2，使得 H(x1) = H(x2)。

---

### 🪙 四、比特币中的 SHA-256

**SHA-256：** 是 Secure Hash Algorithm 2（SHA-2）系列中的一种，由 NSA 设计，输出长度为 256 位（32 字节）。

**用途：**
1. **挖矿（Proof of Work）**：  
   - 挖矿者需要找到一个 nonce，使得 `SHA256(SHA256(BlockHeader))` 的结果小于某个目标值。
2. **交易哈希（Transaction Hashing）**：  
   - 每笔交易都会被哈希成一个唯一 ID。
3. **区块哈希（Block Hashing）**：  
   - 整个区块头部被双重哈希生成 block hash，用作区块标识。
4. **Merkle Tree 构建**：  
   - 每个交易被哈希，然后两两组合再次哈希，最终得到 Merkle Root，作为区块头的一部分。

```text
比特币挖矿核心：  
找一个 nonce，使得  
SHA256(SHA256(BlockHeader)) < Target
```

---

### 📌 示例：SHA-256 哈希

```bash
echo -n "hello" | openssl dgst -sha256
# 输出：2cf24dba5fb0a30e26e83b2ac5b9e29e1b161e5c1fa7425e73043362938b9824
```

---