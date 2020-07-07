https://blog.iota.org/whos-in-who-s-out-a-rate-control-algorithm-for-the-tangle-c7b5ecf85677



Who’s In Who’s Out: a Rate Control Algorithm for the Tangle

Luigi Vigneri
Follow
Jan 18, 2019 · 5 min read


Rate control in distributed ledgers
In most networks, there are circumstances where the incoming traffic load is larger than what the network can handle. If nothing is done to restrict the entrance of traffic, bottlenecks can slow down the entire network. Additionally, the buffer space at some nodes may be exhausted, leading to discarding some of the packets. Similar to a highway traffic jam, as the offered load increases, the actual network throughput decreases while packet delay becomes excessive. Therefore a mechanism to prevent some of the offered traffic from entering the network is necessary in order to avoid this type of congestion.
A similar analysis can be applied to distributed ledgers, where the incoming traffic, i.e., transactions issued by the nodes of the network, exploits limited resources such as bandwidth, computational power, or disk space. Additionally, given the distributed nature of the network, malicious nodes may harm it through spam or distributed denial-of-service attacks. Hence, a transaction rate control mechanism is fundamental for distributed ledgers to function correctly. Traditional blockchains based on Proof-of-Work come with a built-in rate limitation enforced by the mining difficulty adjustment. Unfortunately, this solution leads to undesirable side effects such as mining races.
Unique challenges in the Tangle
Conversely, the Tangle does not use Proof-of-Work to reach consensus. Hence, an explicit rate control mechanism is necessary. Beyond the standard requirement of anti-spam technique against malicious nodes, we want to design an algorithm that achieves a certain degree of fairness guaranteeing that nodes with low computational capabilities still have a non-negligible probability to have their transactions approved. As the reader may imagine, fairness adds complexity to an already non-trivial problem, but we believe it to be a fundamental requirement to speed up the technology adoption.
A possible way to tackle the rate control problem in the Tangle is to build a reputation system for the nodes that issue transactions. The rough idea is that reputation is hard to get, but easy to lose. When a node approves an invalid transaction, attempts to spam the network, or performs a similarly bad behavior, it risks being identified by other nodes. As a result, that node will be untrusted, and its transactions will not be approved with high probability. However, a reputation system is a general-purpose approach, hence not specifically targeted for rate control. Furthermore, given the substantial architectural changes needed, an exhaustive (and, therefore, long) study is required in order to avoid unexpected outcomes. For these reasons, in this post we investigate an alternative approach. In particular, we introduce a novel adaptive rate control algorithm based on the following ideas:
some computational effort is required to issue a transaction;
the computational effort needed to issue multiple transactions in a short time interval progressively increases;
while fast nodes can issue more transactions more frequently, nodes with little computational power are still guaranteed that their transactions can be approved with high probability.
In the following paragraphs, we discuss the two main building blocks of the algorithm necessary to achieve the aforementioned objectives, i.e., (i) node accountability to assign a global identity to each node, and (ii) the actual adaptive rate control mechanism based on varying Proof-of-Work difficulty.
Proof-of-Identity
To implement a rate control mechanism in a distributed system, it is necessary to introduce global node identities. When each node has an identity, common public key cryptography can be used to sign a transaction and to link it to its issuing node in a tamper proof way. By introducing identities, a distributed system becomes vulnerable to Sybil attacks, where a malicious entity masquerades many counterfeit identities and uses them to overcome the rate control to launch a coordinated assault or spam the network.
One way to make such an attack harder is the so-called resource (e.g., CPU power, stake, disk space) testing, where each identity has to prove the ownership of certain difficult-to-obtain resources. For our algorithm, since users store a certain amount of tokens (collateral), we propose a simplified version of Proof-of-Stake. Unlike the original idea, in our proposal collaterals do not leave the users’ possession and, thus, cannot be forfeited. Rather, they are a necessary requirement for each node identity. Any node with a minimum amount of such a collateral is allowed to issue transactions. The need for this minimum amount opens an interesting research question. On the one hand, a low threshold allows more users to issue transactions but it does not protect sufficiently against the creation of counterfeit identities. On the other hand, a large threshold would drastically reduce the number of potential nodes participating in the network at the cost of a larger security. We leave the discussion of this trade-off as a future work.


Figure 1. Block diagram of the proposed adaptive rate control algorithm: first, a node receiving a transaction checks if the original sender is allowed to send issue transactions; then, it verifies whether it performed enough Proof-of-Work.
Adaptive Rate Control Algorithm
In our algorithm (see Figure 1) a node can issue a transaction after solving a cryptographic puzzle, where the difficulty is a function of the collateral owned and of the number of transactions issued recently. In a pure Proof-of-Work-based architecture, a large value of the difficulty would prevent low-power nodes to issue transactions, which is not desirable especially in the context of Internet-of-Things; on the other hand, a small difficulty can easily lead to network congestion. Our proposed adaptive Proof-of-Work allows every node to issue transactions while penalizing spamming actions. A proper choice of the system parameters is required to guarantee a certain level of fairness between nodes.
As an additional security measure, we require that the total number of transactions issued by a user is limited. Specifically, the larger the stake owned by a node, the higher the number of transactions the same node can issue. This threshold brings a twofold benefit: first, it ensures that even a user with infinite computational power cannot arbitrarily spam the network; second, a proper choice of the threshold can discourage Sybil attacks.
Conclusions
The discrepancy between smaller general-purpose devices and optimized hardware with respect to the Proof-of-Work performance is in the order of magnitudes. Hence, any rate control based on Proof-of-Work would eventually leave smaller devices behind. Conversely, a purely stake-based system would lead to a centralization where only the “rich” parties can participate. In this blog post, we have discussed a rate control algorithm which combines the above two approaches: slow nodes or users with low collaterals can issue (a few) transactions at inexpensive prices, while at the same time faster users cannot spam the network due to a limitation on burst of transactions.


Blockchain
Algorithms
Tangle
Antispam
Research And Development

1.7K claps






Written by
Luigi Vigneri
Follow



IOTA
Follow
Official IOTA Foundation blog