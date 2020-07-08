https://blog.iota.org/whos-in-who-s-out-a-rate-control-algorithm-for-the-tangle-c7b5ecf85677



Who’s In Who’s Out: a Rate Control Algorithm for the Tangle

Luigi Vigneri
Follow
Jan 18, 2019 · 5 min read

# Rate control in distributed ledgers

<!--
In most networks, there are circumstances where the incoming traffic load is larger than what the network can handle. If nothing is done to restrict the entrance of traffic, **bottlenecks** can slow down the entire network. Additionally, the buffer space at some nodes may be exhausted, leading to discarding some of the packets. Similar to a highway traffic jam, as the offered load increases, the actual network throughput decreases while packet delay becomes excessive. Therefore a mechanism to prevent some of the offered traffic from entering the network is necessary in order to avoid this type of **congestion**.
-->
たいていのネットワークでは、入ってくるトラフィック負荷がネットワークで処理できる量を超えている状況があります。トラフィックの流入を制限するために何もしなければ、**ボトルネック**によってネットワーク全体の速度が低下する可能性があります。さらに、一部のノードのバッファスペースが枯渇し、パケットの一部が廃棄されることもあります。高速道路の渋滞と同様に、負荷が増大すると、実際のネットワークのスループットは低下し、パケットの遅延は課題になります。そのため、このような**混雑**を回避するためには、要求されたトラフィックの一部がネットワークに入らないようにする仕組みが必要です。

<!--
A similar analysis can be applied to distributed ledgers, where the incoming traffic, i.e., transactions issued by the nodes of the network, exploits limited resources such as bandwidth, computational power, or disk space. Additionally, given the distributed nature of the network, malicious nodes may harm it through spam or distributed denial-of-service attacks. Hence, a transaction rate control mechanism is fundamental for distributed ledgers to function correctly. Traditional blockchains based on Proof-of-Work come with a built-in rate limitation enforced by the mining difficulty adjustment. Unfortunately, this solution leads to undesirable side effects such as mining races.
-->
同様の分析を分散型台帳にも適用することができます。ここでは着信トラフィック、すなわちネットワークのノードが発行したトランザクションが、帯域幅、計算能力、ディスク容量などの限られた資源を悪用します。さらに、ネットワークの分散した性質を考えると、悪意のあるノードはスパムや分散型サービス拒否攻撃によってネットワークに被害を与える可能性があります。したがって、分散型台帳が正しく機能するためには、トランザクションレート制御メカニズムが基本となります。Proof-of-Workに基づく従来のブロックチェーンには、マイニングの難易度調整によって強制されるレート制御が組み込まれています。残念ながら、この解決策は、マイニングレースのような好ましくない副作用をもたらします。

# Unique challenges in the Tangle

<!--
Conversely, the Tangle does not use Proof-of-Work to reach consensus. Hence, an explicit rate control mechanism is necessary. Beyond the standard requirement of anti-spam technique against malicious nodes, we want to design an algorithm that achieves a certain degree of **fairness** guaranteeing that nodes with low computational capabilities still have a non-negligible probability to have their transactions approved. As the reader may imagine, fairness adds complexity to an already non-trivial problem, but we believe it to be a fundamental requirement to speed up the technology adoption.
-->
逆に、TangleではProof-of-Workを使用してコンセンサスを得ることはありません。そのため、明示的なレート制御機構が必要となります。悪意のあるノードに対するスパム対策技術の標準的な要件を超えて、私たちは、計算能力の低いノードであっても取引が承認される確率が無視できないほど高いことを保証し、ある程度の**公平さ**を達成するアルゴリズムを設計したいと考えています。読者の方は想像されるかもしれませんが、公平さはすでに自明な問題に複雑さを加えますが、技術の採用を加速させるための基本的な要件であると考えています。

<!--
A possible way to tackle the rate control problem in the Tangle is to build a **reputation system** for the nodes that issue transactions. The rough idea is that reputation is hard to get, but easy to lose. When a node approves an invalid transaction, attempts to spam the network, or performs a similarly bad behavior, it risks being identified by other nodes. As a result, that node will be untrusted, and its transactions will not be approved with high probability. However, a reputation system is a general-purpose approach, hence not specifically targeted for rate control. Furthermore, given the substantial architectural changes needed, an exhaustive (and, therefore, long) study is required in order to avoid unexpected outcomes. For these reasons, in this post we investigate an alternative approach. In particular, we introduce a novel **adaptive rate control algorithm** based on the following ideas:
-->
Tangleにおけるレート制御の問題に取り組むために考えられる方法は、トランザクションを発行するノードのために**評価システム**を構築することです。ざっくりとした考えでは、評価を得るのは難しいが、失うのは簡単だということです。あるノードが無効なトランザクションを承認したり、ネットワークにスパムを送ろうとしたり、同様の悪い行いをすると、他のノードに特定されるリスクがあります。その結果、そのノードは信頼されなくなり。そのトランザクションは高い確率で承認されなくなります。しかし評価システムは汎用的なアプローチであり、特にレート制御を目的としたものではありません。さらに、アーキテクチャの大幅な変更が必要であることを考えると、予期せぬ結果を避けるためには、網羅的な（したがって、長い）研究が必要となります。これらの理由から、この記事では代替的なアプローチを検討します。特に以下のアイデアに基づいた新しい**適応的なレート制御アルゴリズム**を紹介します。

<!--
- some computational effort is required to issue a transaction;

- the computational effort needed to issue multiple transactions in a short time interval progressively increases;

- while fast nodes can issue more transactions more frequently, nodes with little computational power are still guaranteed that their transactions can be approved with high probability.
-->
- トランザクションを発行するためには、ある程度の計算負荷が必要です。

- 短い時間間隔で服須区のトランザクションを発行するには必要な計算量が徐々に増加します。

- 高速ノードはより頻繁にトランザクションを発行できますが、計算能力の低いノードでも、高い確率でトランザクションが承認されることを保証されています。

<!--
In the following paragraphs, we discuss the two main building blocks of the algorithm necessary to achieve the aforementioned objectives, i.e., (i) node accountability to assign a global identity to each node, and (ii) the actual adaptive rate control mechanism based on varying Proof-of-Work difficulty.
-->
以下の段階では、上述の目的を達成するために必要なアルゴリズムのうち、2つの主要な構成要素、すなわち、(i)各ノードにグローバルなアイデンティンティを割り当てるためのノードアカウンタビリティと、(ii)Proof-of-Workの難易度を変化せせることによって実際の適応レート制御メカニズムについて述べます。

# Proof-of-Identity

<!--
To implement a rate control mechanism in a distributed system, it is necessary to introduce **global node identities**. When each node has an identity, common public key cryptography can be used to sign a transaction and to link it to its issuing node in a tamper proof way. By introducing identities, a distributed system becomes vulnerable to Sybil attacks, where a malicious entity masquerades many counterfeit identities and uses them to overcome the rate control to launch a coordinated assault or spam the network.
-->
分散システムにレート制御機構を実装するためには、*global node identities*を導入する必要があります。各ノードがアイデンティティを持つと、共通公開鍵暗号を用いてトランザクションに署名したり、発行ノードとの間を改ざん防止の方法で結び付けたりできます。アイデンティティを導入することで、分散システムは悪意のあるエンティティが多数の偽のアイデンティティを偽装し、それらを利用してレート制御を克服して、協調攻撃を開始したり、ネットワークをスパム化したりするシビル攻撃に対して脆弱になります。
（訳注：脆弱になる？）

<!--
One way to make such an attack harder is the so-called resource (e.g., CPU power, stake, disk space) testing, where each identity has to prove the ownership of certain difficult-to-obtain resources. For our algorithm, since users store a certain amount of tokens (collateral), we propose a simplified version of Proof-of-Stake. Unlike the original idea, in our proposal collaterals do not leave the users’ possession and, thus, cannot be forfeited. Rather, they are a necessary requirement for each node identity. Any node with a minimum amount of such a collateral is allowed to issue transactions. The need for this minimum amount opens an interesting research question. On the one hand, a low threshold allows more users to issue transactions but it does not protect sufficiently against the creation of counterfeit identities. On the other hand, a large threshold would drastically reduce the number of potential nodes participating in the network at the cost of a larger security. We leave the discussion of this trade-off as a future work.
-->
このような攻撃をより困難にする方法の一つは、各IDが特定の入手困難なリソースの所有権を証明しなければならず、いわゆるリソース（CPUパワー、ステーク、ディスク容量など）をテストします。私たちのアルゴリズムでは、ユーザーが一定量のトークン（担保）を保持しているため、Proof-of-Stakeの簡易版を提案します。本提案では、当初のアイデアとは異なり、担保は利用者の手元から離れないため、没収されることはありません。むしろ、それは各ノードのアイデンティティに必要な要件です。このような最低限の担保を持つノードは、トランザクションの発行を許可されています。混載少量の必要性は、興味深い研究上の疑問を生みます。一方で閾値が低いと、より多くのユーザーがトランザクションを発行できるようになりますが、偽造アイデンティティの生成に対しては十分には保護されません。一方で、閾値を大きくすると、より大きなセキュリティを犠牲にして、ネットワークに参加する潜在的なノードの数を大幅に減らすことになります。このトレードオフについての議論は今後の課題とします。

<!--
Figure 1. Block diagram of the proposed adaptive rate control algorithm: first, a node receiving a transaction checks if the original sender is allowed to send issue transactions; then, it verifies whether it performed enough Proof-of-Work.
-->
図1．提案する適応レート制御アルゴリズムのブロック図：まず、トランザクションを受信したノードが、元の送信者がイシュートランザクションの送信を許可されているかチェックし、次に、それが十分なProof-of-Workを行ったかどうか検証します。

# Adaptive Rate Control Algorithm

<!--
In our algorithm (see Figure 1) a node can issue a transaction after solving a cryptographic puzzle, where the difficulty is a function of the collateral owned and of the number of transactions issued recently. In a pure Proof-of-Work-based architecture, a large value of the difficulty would prevent low-power nodes to issue transactions, which is not desirable especially in the context of Internet-of-Things; on the other hand, a small difficulty can easily lead to network congestion. Our proposed **adaptive Proof-of-Work** allows every node to issue transactions while penalizing spamming actions. A proper choice of the system parameters is required to guarantee a certain level of fairness between nodes.
-->
私たちのアルゴリズム（図１参照）では、ノードは暗号パズルを解いた後にトランザクションを発行することができ、難易度は所有する担保と最近発行されたトランザクション数の関数です。純粋なProof-of-Workベースのアーキテクチャでは、難易度の値が大きいと低消費電力ノードがトランザクションを発行できなくなるため、特にInternet-of-Thingsの文脈では好ましくありません。私たちが提案する。**adaptive Proof-of-Work**は、スパム行為にペナルティを与えながら、すべてのノードがトランザクションを発行することを可能にします。ノード間で一定レベルの公平性を保証するためには、システムパラメーターの適切な選択が必要です。

<!--
As an additional security measure, we require that the total number of transactions issued by a user is limited. Specifically, the larger the stake owned by a node, the higher the number of transactions the same node can issue. This threshold brings a twofold benefit: first, it ensures that even a user with infinite computational power cannot arbitrarily spam the network; second, a proper choice of the threshold can discourage Sybil attacks.
-->
さらに、セキュリティ対策として、ユーザーが発行できるトランザクションの総数を制御することを要求します。具体的には、ノードが所有するステークが大きいほど、同じノードが発行できるトランザクション数が多くなります。第一に、無限の計算能力を持つユーザーであっても、ネットワーク上で任意のスパム行為ができないことを保証し、第二に閾値を適切に選択することで、シビル攻撃を抑制することができます。

# Conclusions

<!--
The discrepancy between smaller general-purpose devices and optimized hardware with respect to the Proof-of-Work performance is in the order of magnitudes. Hence, any rate control based on Proof-of-Work would eventually leave smaller devices behind. Conversely, a purely stake-based system would lead to a centralization where only the “rich” parties can participate. In this blog post, we have discussed a rate control algorithm which combines the above two approaches: slow nodes or users with low collaterals can issue (a few) transactions at inexpensive prices, while at the same time faster users cannot spam the network due to a limitation on burst of transactions.
-->
Proof-of-Workの性能に関して、より小型の汎用デバイスと最適化されたハードウェアとの間には、けた違いの差があります。したがって、Proof-of-Workに基づくレート制御は、最終的には小型デバイスを置き去りにしてしまいます。逆に、純粋にステークベースのシステムでは「富裕層」だけが参加できる中央集権化になってしまいます。このブログ記事では、上記2つのアプローチを組み合わせたレート制御アルゴリズムについて議論してきました。：遅いノードや担保の低いユーザーは安価な価格で（多少の）トランザクションを発行でき、同時に早いユーザーはトランザクションのバースト制御のためにネットワークにスパムすることはできません。


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