https://blog.iota.org/iota-research-status-update-june-2020-f0fbf9df0a4b

IOTA Research Status Update June 2020

Serguei Popov
Follow
Jun 18 · 5 min read

<!--
We have a few exciting status updates to share with everyone this month: First, the new GoShimmer release v0.2.0 is planned for the end of June. We consider this release to be a significant milestone, as it will support value transactions and conflict resolution via FPC for the first time. It will also include updates such as a different transaction layout, UTXO, support for “parallel-reality” ledger states, binary (encoding, cryptographic signatures and hash functions), new APIs and more. GoShimmer is designed with modularity at its core, which has greatly simplified the process of enriching it with these additional features and modules.
-->
今月はいくつかのエキサイティングなステータスアップデートを皆さんと共有したいと思います。まず、新しいGoShimmerのリリースv0.2.0が6月末に予定されています。このリリースは重要なマイルストーンと考えており、FPCを介した価値取引と競合解決を初めてサポートします。また、異なるトランザクションレイアウト、UTXO、「パラレルリアリティ」台帳状態のサポート、バイナリ（エンコーディング、暗号署名、ハッシュ関数）、新しいAPIなどのアップデートも含まれています。GoShimmerはモジュール性を核に設計されており、これらの追加機能やモジュールを使ってGoShimmerを充実させるプロセスを大幅に簡略化しています。

<!--
Next, we’re happy to report that we have published a paper on integrating FPC and mana, to be presented at FTC2020. We’ve also submitted two networking papers, and our dRNG paper is being polished for submission.
-->
次に、FTC2020で発表予定のFPCとmanaの統合に関する論文を発表しましたのでご報告します。また、2つのネットワーキング論文を提出し、dRNGの論文は提出に向けて磨きをかけています。

<!--
Finally, we are pleased to report that the positive feedback loop between Research and Engineering has been strengthened, with input from each team helping in an iterative refinement process of the specifications. Most of the specifications have been improved as a result of this interaction, and we are excited to see the progress of the specifications across the board to a very good stage. Specific updates from each of our groups follow below.
-->
最後に、研究部門とエンジニアリング部門の間にポジティブなフィードバックループが強化され、各チームからのインプットが仕様の反復的な改良プロセスに役立っていることを報告します。この相互作用の結果、ほとんどの仕様が改善されており、全体的に非常に良い段階まで仕様が進んでいるのを確認できることを楽しみにしています。以下、各グループからの具体的なアップデートをご紹介します。

・・・

<!--
**GoShimmer Implementation**. The team has finished implementing and testing the parallel-reality based ledger state that will be part of the next GoShimmer release in its branch-based form. We believe that this new concept for managing the ledger state will be a very good fit for our decentralized network and will be one of the main subjects to assess after the new release. The analysis server has been enriched with a brand new section showing the overall network consensus, specifically a real-time update on the FPC outcome on each conflict. These results will also be stored on a database so that, together with our community, we will gather enough experimental data to compare with our previous results obtained by means of simulations. Moreover, the autopeering section has been improved on both the frontend and backend side.
-->
**GoShimmer実装**。チームは、次のGoShimmerリリースの一部となるパラレルリアリティベースの台帳状態を、そのブランチベースの形で実装し、テストを終えました。この台帳状態を管理するための新しいコンセプトは、私たちの分散型ネットワークに非常に適しており、新しいリリース後に評価すべき主要な課題の一つになると確信しています。解析サーバーは、ネットワーク全体のコンセンサスを示す新しいセクションで強化され、特に各競合のFPCの結果をリアルタイムで更新しています。これらの結果はデータベースに保存され、私たちのコミュニティと一緒に、[シミュレーション](https://arxiv.org/abs/1911.08787)によって得られた以前の結果と比較するのに十分な実験データを収集することができます。さらに、オートピアリングの部分はフロントエンドとバックエンドの両方で改善されています。

<!--
This month we have also been working on the new APIs for issuing value transactions and retrieving the balance of a given address. These APIs will be the core of a very simple wallet we are currently working on.
-->
今月は、値トランザクションの発行や、指定されたアドレスの残高を取得するための新しいAPIにも取り組んできました。これらのAPIは、現在取り組んでいる非常にシンプルなウォレットの中核になります。

<!--
As everything is now based on binary, we have developed a new configurable Proof of Work (PoW) library that will, in future and iterative releases, shift towards our adaptive PoW.
-->
現在、すべてがバイナリをベースにしているため、将来の反復リリースで[適応PoW](https://blog.iota.org/whos-in-who-s-out-a-rate-control-algorithm-for-the-tangle-c7b5ecf85677)に移行する新しい設定可能な作業証明（PoW）ライブラリを開発しました。

<!--
Finally, a large amount of our time has been spent on developing and improving both unit and integration tests. Although this task can be (and it has been!) tedious, it has helped us tremendously to be sure not only that the code works as we expect, but also to improve some bits and pieces and to learn more about the code written by other team members.
-->
最後に、大量の時間をユニットテストと統合テストの両方の開発と改善に費やしました。この作業は退屈な作業ですが、コードが期待通りに動作することを確認するだけでなく、いくつかの部分を改善したり、他のチームメンバーが書いたコードについてより深く知ることができました。

<!--
**FPC**. We have just published a conference paper on how mana is implemented in FPC; the paper will be presented at FTC2020. Moreover, we finished a short research note that investigates effects that may arise from weighted voting such as loss of anonymity, centralization, and scalability while discussing their relevance to protocol design and implementation.
-->
**FPC**。この[論文](https://arxiv.org/abs/2006.00928)はFTC2020で発表される予定です。また匿名性の損失、集中化、スケーラービリティなど、加重投票によって生じる可能性のある影響を調査し、プロトコル設計や実装との関連性を議論した短い研究ノートを完成させました。

<!--
**Networking**. Two manuscripts have been submitted and are currently under review for a top-level international conference: (i) “On Congestion Control for Distributed Ledgers in Adversarial IoT Networks” presents our current proposal to deal with network congestion, and shows the results of our simulations; (ii) “Preventing Denial of Service Attacks in IoT Networks through Verifiable Delay Functions” describes how verifiable delay functions can be used to replace PoW as a rate-limiting mechanism, and shows an actual implementation on Raspberry Pi and standard laptops.
-->
**ネットワーキング**。2つの論文が提出され、現在、最上位の国際会議で審査中です。(i)[「敵対IoTネットワークにおける分散型台帳の渋滞制御について」](https://arxiv.org/abs/2005.07778)はネットワークの渋滞に対処するための現在の提案を提示し、シミュレーションの結果を示しています。(ii)[「検証可能な遅延機能によるIoTネットワークでのサービス拒否攻撃の防止」](https://arxiv.org/abs/2006.01977)では、検証可能な遅延機能を利用してレート制御アルゴリズムとしてPoWを置き換える方法を説明し、Raspberry Piと標準のラップトップで実際の実装を示します。

<!--
Additionally, we are working on the theoretical validation of our congestion control algorithm by analyzing the buffer dynamics through queueing theory models, and we are generalizing our proposal for transactions of different sizes and types. As for verifiable delay functions, we are actively studying multi-exponentiation techniques to speed up computation and verification time, especially in low-power devices.
-->
さらに、キューイング理論モデルを用いてバッファダイナミクスを解析し、混雑制御アルゴリズムの理論的検証を行っており、規模や種類の異なるトランザクションに対して提案を一般化しています。また、検証可能な遅延関数について、特に低消費電力デバイスでの計算・検証時間の高速化を目的のして、多値化技術の研究を積極的に行っています。

<!--
**dRNG**. With the specification of dRNG module ready, we are currently focused on writing articles for peer-reviewed academic journals. We hope that publishing our results will help us improve our ideas and promote them. We decided that we are going to prepare two articles. The first one focuses on the committee selection and random number publication in the Tangle. The second one is devoted to improvements to security and liveness.
-->
*dRNG*。dRNGモジュールの仕様が整ったことで、現在は査読付き学術誌への論文執筆に注力しています。成果を公開することで、アイデアの改善やプロモーションに役立てたいと考えています。そこで2つの記事を用意することにしました。1本目は、Tangleでの委員会選定と乱数公開に焦点を当てています。2つ目は、セキュリティと活気の改善に専念しています。

<!--
**Mana and Autopeering**. We now have good drafts of the mana and autopeering specifications, which is an exciting step. After the engineering department reviews them, we will make some final revisions and then the specifications will be finished. The engineering team will then be able to implement these solutions.
-->
*Manaとオートピアリング*。manaとオートピアリングの仕様書の原案ができました。エンジニアリング部門がそれらをレビューした後、最終的な修正を行い、仕様書は完成します。その後、エンジニアリングチームはこれらのソリューションを実装することになります。

<!--
We also refined some ideas about mana, and we decided to add a feature that will enable nodes to “refresh” their mana, even if it was connected to funds held in cold storage. This will increase the utility of mana, and also help secure the system.
-->
また、manaに関するアイデアをいくつかを洗練させ、コールドストレージに保管されている資金につながっていたとしても、ノードがmanaを「リフレッシュ」できるようにする機能を追加することにしました。これによりmanaの有用性が高まり、システムの安全性の確保にも貢献します。

<!--
As the specifications near completion, the first phase of this group’s project is really winding down. We hope to start to shift our focus to writing up our results and also researching the best parameters. This work, although important, is not as pressing as the specifications since it is not blocking engineering’s ability to begin coding.
-->
仕様書が完成に近づき、このグループの第一期のプロジェクトもいよいよ佳境に入ってきました。そろそろ結果を書き上げることや、最適なパラメーターの研究に焦点を当てていきたいと考えています。この作業は重要ではありますが、エンジニアのコーディング開始を妨げるものではないので、仕様書ほど急務ではありません。

<!--
**Protocol**. This month the team finalized the research on orphanage and finality. We also revisited the recent research on solidity to see how it would interact with voting and other checks that depend on the past, hence we decided that solidification on the Value Tangle should not be enforced, but required to be eligible for tip selection and voting.
-->
今月、チームはorphanageと確率性に関する研究をまとめました。また、私たちは最近の堅実性に関する堅実性の研究を再検討し、投票や過去に依存する他のチェックとどのように相互作用するかを確認しました。そのため、私たちは価値Tangleでの堅実性は強制されるべきではなく、チップの選択や投票の資格を得るために必要であると決定しました。

<!--
With the research on the protocol nearly concluded, the specs are being written and advancing smoothly. They will be concluded in the coming days and will be passed off to the engineering team for their feedback.
-->
プロトコルの研究がほぼ終了したため、仕様書を作成しており、順調に進んでいます。近日中に完成し、エンジニアリングチームにフィードバックされる予定です。

<!--
We look forward to the coming GoShimmer release, and we hope that you are able to participate in the early community testing. Until our next monthly update, you can stay up to date with the IOTA Research team in the #tanglemath channel on our Discord. You are also welcome to follow and participate in our technical discussions on our public forum: IOTA.cafe.
-->
GoShimmerのリリースを楽しみにしています。次回の月例アップデートまで、IOTA Researchチームの最新情報はDiscordの#tanglemathチャネルで確認できます。また、公開フォーラム:IOTA.cafeでの技術的な議論をフォローしたり、参加することも歓迎します。


Research And Development
Iota
Coordicide
Goshimmer
Techupdates

1.7K claps






Written by
Serguei Popov
Follow
mathematician


IOTA
Follow
Official IOTA Foundation blog