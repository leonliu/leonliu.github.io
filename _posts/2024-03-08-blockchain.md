---
title: "Blockchain 技术简介"
date: 2024-03-08
---
## 区块链的前世今生

区块链（blockchain）：是分布式数据存储、点对点传输、共识机制、加密算法等计算机技术的新型应用模式。
![blockchain history](/assets/img/blockchain-history.png)

## 区块链核心概念

区块链是一种去中心化的记录技术.

* 维护一条不断增长的记录链条，只能添加记录，发生过的记录不可篡改
* 去中心化（多中心化），无需集中的控制而能达成共识，实现上尽量分布式
* 通过密码学机制来确保交易无法抵赖和破坏，并尽量保护用户信息和记录的隐私性

![blockchain](/assets/img/blockchain-flow.png)

基本概念

* 交易（Transaction）：一次操作，这个操作导致账本状态的一次改变，比如添加一条记录
* 区块（Block）：记录一段时间内发生的所有交易和状态结果，是对当前账本状态的一次共识
* 链（Chain）：由一个个区块按照发生顺序串联而成，是整个状态变化的日志记录

区块（Block）- 以比特币区块为例。区块主要包括4字节区块大小，80字节区块头，其中有上一个区块头的
SHA256 hash值，这样把已经提交的区块“链接”起来，另外所有已经提交的区块无法再做改动，否则hash值
将发生变化。

![block](/assets/img/block-arch.png)

以下为一个实际的block的例子。

![example](/assets/img/block-example.png)

各种“链”，公有链，联盟链，私有链。区块链按照访问管理权限划分：

* 公有链：完全开放，开源系统，匿名，节点之间无需公开身份，无需彼此信任
* 私有链：普通用户智能查询和交易，不能记录和验证
* 联盟链：与私有链类似，多用于机构之间的数据共享协作，普通用户无权记录和验证；

## 区块链涉及的技术领域

区块链涉及分布式、密码学、心理学、经济学、博弈论等领域的技术。

![technology](/assets/img/blockchain-tech.png)

### P2P网络

***P2P网络 – 中央服务网络***

![p2p central](/assets/img/p2p-net.png)

网络模型：

* Server通讯，查询peer信息
* Peer直连，传送数据

中央服务网络的优点：

* 查询高效
* 带宽使用较少
* 不需要维护每个节点的信息

中央服务网络的缺点：

* Server是单点，容灾性不好
* 可扩展性不好，受server限制

***P2P网络 – 完全对等网络***

![p2p peer](/assets/img/p2p-peer.png)

网络模型：

* peer信息查询广播到相邻节点
* 随机圈定相邻节点

完全对等网络的优点：

* 无单点问题
* 只需要维护有限个节点（邻居）的信息

完全对等网络的缺点：

* 查询慢
* 广播方式消耗带宽

***P2P网络 – 层级式网络***

![p2p hierarchy](/assets/img/p2p-hierarchy.png)

网络模型：

* 网络中选出一组超级节点来负责查询等
* 超级节点负责维护所在分组的叶子节点的信息
* 超级节点之间互联

层级网络的优点：

* 查询快

层级网络的缺点：

* 超级节点发生掉线时需要重新配置

***P2P网络 – 分布式哈希（DHT）网络***

![p2p DHT](/assets/img/p2p-dht.png)

网络模型：

* 也叫做结构化P2P网络
* 提供可靠的性能保证
* 如果内容存在，能够确保在DHT网络上可以找到

DHT网络的优点：

* 查询快
* 只需维护有限的节点信息

DHT网络的缺点：

* 容错能力有限

***P2P网络 - BitTorrent***

![bittorrent](/assets/img/bittorent.png)

* 种子（torrent file）：记录文件的大小，名字，分段大小，分段的hash等描述信息，以及tracker的IP地址，url等信息；
* peer：p2p的对端，分为initial seeder（有完整的文件），seeder（即上传也下载），leecher（吸血鬼，只下载不上传）
* tracker：维护peer的状态信息，统计记录哪个peer有哪些文件的分段资源可供下载

Bittorrent的资源共享机制

![bittorrent share](/assets/img/bittorent-packet.png)

* Leecher下载种子文件（.torent），找到tracker
* Leecher开始从initial seeder那里下载分段
* 当leecher完成文件下载后，自动成为seeder，开始贡献下载资源

Bittorrent的网络交互流程

![bittorrent handshake](/assets/img/bittorent-flow.png)

### 分布式系统

***分布式系统的一致性问题***

![consistence](/assets/img/accordance.png)

***怎样保证这样一个不靠谱的网络中大家处理的结果是一致的？***

分布式系统的共识算法：解决对某个提案，大家达成一致意见的过程。

![algorithm](/assets/img/pow.png)

***Paxos算法***：1990年由Leslie Lamport（这尊大神对一致性问题解决影响深远）提出，大神喜欢
以故事的形式来描述算法。

“古希腊Paxon岛上有一堆法官在一个大厅内对一个议案进行表决，如何达成统一的结果。他们之间通过服务生
来传递纸条，但法官可能离开或进入大厅，服务人员可能偷懒去睡觉。”

算法比较难懂，简单的说就是分两阶段提交提案，当提案获得超过一半支持时，发送提案结果给所有人确认。
Paxos能保证在超过1/2的正常节点存在时，系统能达成共识。

Raft算法是Paxos算法的一种简化实现，主要是简化过程为leader选举，之后由leader强制系统更新最新
的信息；

***拜占庭将军问题（又是Lamport编的一个故事）***

“拜占庭是古代东罗马帝国的首都，有一次拜占庭的将军们分别率领军队共同围困一座城市，战役进入僵局需
要决定继续进攻还是撤退，需要将军们投票确定，将军们通过信使传递信息，然而将军们中间可能有叛徒，
该如何达成一致的行动？”

***PBFT算法***：分3个阶段达成共识，只要系统中有2/3的节点是正常工作的，则可以保证一致性；

***PoW算法***：比特币的区块链网络提出的算法，博弈论的绝妙应用。

* 限制一段时间内整个网络中出现提案的个数（每隔10分钟允许提交一个区块），同时设定难度指标，以增加提案成本；
* 放宽对最终一致性的要求，约定好大家都确认并沿着已知最长的链进行拓宽；
* 即便有人试图恶意破坏，也要付出超过全比特币网络一半的算力，概率上基本没人有这个能力（51%攻击）

***PoS算法***

PoS（Proof of Stake）：权益证明，2013年被提出，类似现实生活中的股东机制，拥有股份越多的人越
容易获取记账权。

PoS通过保证金（可以是代币、资产等具备价值属性的物品）来对赌一个合法的区块成为最新的通过认证的区块，
收益为保证金的利息和交易服务费。保证金越多，则获得记账权的概率越大。

在PoW中，算力竞争导致大量资源被浪费，PoS试图解决这个问题，作弊者的保证金可能会被罚没。

DPoS（Delegated PoS）：授权权益证明机制，类似股东选举董事会。比特币持有者们投票选举出代理，由
这些被选举出的代理们来验证交易和维护区块链。DPoS维护一个用不散场的“股东大会”，持续淘汰不满足条件
的代理和选举新的代理。代理们添加区块不再需要进行算力的竞争，而是轮流排期。

![PoW & PoS](/assets/img/pos.png)

最终还是经济利益之手控制一切，参与PoW计算竞赛的人，将付出硬件、电力、维护的成本，当没有成为第一个
计算出的幸运儿，或者不是在最长链上提交，所有成本将付之东流。发现问题没有？存在巨大的算力浪费！！！

***比特币挖矿的难度在哪里？***

如果仅仅计算区块的hash，是没有难度的，例如以下伪码：

Hash（上一个区块的hash值，交易记录集） = 455748ADE

因此比特币系统引入一个随机数，也就是nonce，且要求计算结果必须以若干0开头，增加计算难度：

Hash（上一个区块的hash值，交易记录集，随机数） = 0000aFD635BCD

这是个猜谜的过程，计算量是16的n次方，n是开头0的个数

### 密码学与安全技术

一个典型交易过程

![trade](/assets/img/trade.png)

***哈希算法***

Hash算法将任意长度的二进制值映射为较短的固定长度的二进制值，也即hash值。区块链中大量使用hash算法。

* 区块链中节点的地址、公钥、私钥的计算；
* 莫克尔树（Merkle Tree）的计算；
* 挖矿，PoW中的hash计算；
* 比特币中的布隆过滤器（Bloom Filter），基于hash函数快速查找；

哈希有四个作用

* 简化信息，哈希后的信息变短了
* 标识信息，可以用哈希值来标识原始信息，也即摘要
* 隐匿信息，账本记录哈希值，原始信息被隐匿
* 验证信息，交易双方可以用哈希值来验证原始信息

回到比特币区块的格式，除第一个区块外，每个区块头包含了上一个区块的hash，间接的包含了上一个区块的
信息，这样只需要验证最后一个区块，就等于验证了整个区块链账本。

***Merkle树***

Merkle树是一个hash二叉树，在比特币区块链中用于保存交易信息：

* 底层数据Tx的任何变动，都会逐级传递到父亲节点，直到树根；
* 由于hash树的特性，Merkle树特别适合快速比较大量数据，两个Merkle树根相同，则所代表的数据相同；
* 如果T1的数据被修改，会影响到N1，N4和Root，因此可以快速定位修改；
* 零知识证明，如果要证明某个区块包含T1，只需要公布N0，N1，N4，Root，T1的拥有者就可以很容易检测T1存在，但不必知道T0，T2和T3。

![Merkle](/assets/img/merkle.png)

***非对称加密算法***

非对称加密算法中，加密和解密使用不同的规则（密钥）

* 乙方生成两把密钥（公钥和私钥），公钥是公开的，任何人都可以获得，私钥则是保密的；
* 甲方获取乙方的公钥，然后用它对信息加密；
* 乙方得到加密后的信息，用私钥解密；
* 非对称加密算法的安全性通常基于数学问题来保障，例如大数因子分解、离散对数、椭圆曲线等；
* 代表算法有RSA、EIGamal、ECC等，其中RSA算法是目前最广泛使用的非对称加密算法；

对称加密算法中，加密和解密使用的是相同的规则（密钥）

* 分组密码和序列密码，前者将明文切分为定长数据来加密，后者只对一个字节进行加密，且密码不断变化
* 代表算法有DES、3DES、AES、IDEA等；

***RSA算法***

RSA算法的过程：

* 选择两个质数p和q
* 计算p和q的乘积n(n = pq)
* 从小于n的整数集合中随机选取e，e就是加密的公钥，e ∈ Zn
* 选择小于n的一个整数d，满足ed = 1 (mod Φ(n))，d就是私钥
* 公钥和私钥确定后，加密消息m，得到加密后的信息c，c = me (mod n)
* 解密c的公式为：m = cd (mod n)

RSA算法的可靠性：已知公钥n和e，破解出d的难度有多大？

* 根据ed = 1 (mod Φ(n))，要解出d，需要知道e和Φ(n)
* 根据欧拉定理，Φ(n) = (p-1)(q-1)，只有知道p和q才能算出Φ(n)
* 因为n = pq，问题变成因数分解n，大整数的因数分解只能暴力穷举计算，只要n取值足够大，d是安全的

相反，如果我们用私钥加密，公钥解密，这就是数字签名：经过私钥加密的信息，只有配对的公钥能够解密，
通过这种方式证明信息来源的合法性。

***数字签名***

小芳要给小明发一个合同文件，小明如何确认合同的内容是没有经过篡改的，且收到的合同就是小芳发来的？
– 数字签名解决了这个问题

![digital signature](/assets/img/signature.png)

***比特币中的公钥、私钥和数字签名***

比特币中的私钥p由钱包软件随机生成，公钥（比特币地址）a由私钥随机生成

![bitcoin sign](/assets/img/sign.png)

***比特币交易的安全验证***

![bitcoin security](/assets/img/verify.png)

***智能合约***

智能合约就是在计算机系统上，当满足一定条件时，可以被自动执行的合约。

![smart contract](/assets/img/smart-contract.png)
