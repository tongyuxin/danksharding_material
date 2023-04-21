# Danksharding_material

## Danksharding思路简介
  Danksharding的核心思想：中心化出块+去中心化的验证+抗审查性，具体而言：
* 通过数据可用性采用（DAS），大大降低了参与网络验证的成本，保持了网络验证的去中心化。DAS由纠删码和KZG承诺组成。
    * 采用纠删码使得随机下载一部分数据即可验证所有的数据可用性，并在必要时重建所有数据。Reed-Solomon对数据进行扩展，将数据插值为多项式，所以我们可以在其他地方对其进行评估。（例，通过最初的4个数据确定一个三次多项式，再增加4个数值，这些数值都位于一个多项式上。现在我们只需要确定任何50%的擦除编码数据是可用的，就可以重构出整个数据块。因此攻击者必须隐藏超过50%的数据块，才能成功的欺骗DAS节点，使其认为数据是可用的）
    * KZG承诺用于确保原始数据被正确扩展，纠删码编码正确。KZG承诺找到符合所有数据的最小次数的多项式，随后承诺该多项式。所以KZG承诺让我们可以对数据和数据扩展进行承诺，并证明他们落在同一个低次多项式上。
* 通过出块者-打包者分离（PBS），原先维护以太坊所有历史状态数据的全节点，被进一步划分为两个角色：出块者（proposer）和打包者（Builder）。专门的打包者把区块放在一起，并为验证者选择他们的区块出价。这不仅为大量数据包的传输提供了可能，也解决了MEV问题。
* 通过抗审查清单（Crlist），避免了交易被审查的可能性。
【分片1.0包括64个独立的委员会和发起人，可以允许每个分片单独出问题。通过更紧密的整合使我们能够一次性地确保完整的数据可用（DA）。数据在黑盒中仍然是“分片”的，但从实用的角度来看，分片更像大块的数据，唯一的分片体现在验证者不负责下载所有数据的这一事实】

## 阅读材料
* 官网介绍：https://ethereum.org/en/roadmap/danksharding/
* EIP4844: https://eips.ethereum.org/EIPS/eip-4844 【注意，PoC仍然在要做的列表里！】
* Proto-Danksharding常见问题解答：https://notes.ethereum.org/@vbuterin/proto_danksharding_faq
* Dankrad分片策略：https://notes.ethereum.org/@dankrad/new_sharding
* 对分片+ DAS方案的解释：https://hackmd.io/@vbuterin/sharding_proposal
* Dankrad,Proto,Vitalik对分片的讨论：https://www.youtube.com/watch?v=N5p0TB77flM
* “DankSharding”教育研讨会：https://www.youtube.com/watch?v=e9oudTr5BE4
