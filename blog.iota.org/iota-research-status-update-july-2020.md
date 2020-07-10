https://blog.iota.org/iota-research-status-update-july-2020-5a863a1dfae6

IOTA Research Status Update July 2020
Serguei Popov
Serguei Popov
Follow
Jul 10 · 4 min read


<!--
This month, we were honored to release Pollen, the first testnet version of IOTA 2.0 to include Fast Probabilistic Consensus, the consensus mechanism for the post-Coordicide IOTA. Work continues on the finalization and further integration of our research specifications into future updates, with a major milestone this month being the finalized version of two types of mana implementations.
-->
今月は、Coordicide後のIOTAコンセンサスアルゴリズムであるFast Probabilistic Consensusを含むIOTA2.0の最初のテストネット版であるPollenをリリースできたことを光栄に思います。私たちの研究仕様の最終化と将来のアップデートへのさらなる統合に向けて作業が続けられており、今月の大きなマイルストーンは、2種類のマナ実装の最終バージョンです。

<!--
Below are the updates from several of our research groups.
-->
以下、いくつかの研究グループから最新情報を紹介します。

<!--
*GoShimmer Implementation*. Last week, we released [Pollen](https://blog.iota.org/introducing-pollen-the-first-decentralized-testnet-for-iota-2-0-349f63f509a1), our first fully decentralized testnet based on GoShimmer v0.2.0. Pollen represents a major upgrade with respect to the previous Alphanet v0.1.3 release. We count roughly 60,000 additions and 25,000 deletions to the [codebase](https://github.com/iotaledger/goshimmer). Some of the newly added features include:
-->
*GoShimmerの実装*。先週、私たちはGoShimmer v0.2.0をベースにした最初の完全分散型テストネットである[Pollen](https://blog.iota.org/introducing-pollen-the-first-decentralized-testnet-for-iota-2-0-349f63f509a1)をリリースしました。Pollenは以前のAlphanet v0.1.3からの大幅なアップグレードです。私たちは[codebase](https://github.com/iotaledger/goshimmer)に約60,000の追加と25,000の削除を行いました。新しく追加された主な機能は以下の通りです。

<!--
- Fast Probabilistic Consensus (FPC) — IOTA’s new consensus algorithm for a fully decentralized network. You can read the [research paper here](https://arxiv.org/abs/1905.10895).
-->
- Fast Probabilistic Consensus (FPC) -- 完全な分散型ネットワークのためのIOTAの新しいコンセンサスアルゴリズム。[研究論文はこちら]((https://arxiv.org/abs/1905.10895))。

<!--
- Value Transactions — network participants can now use an automated faucet to receive tokens, send value transactions (via a wallet) and test conflict resolution on the network.
-->
- 価値トランザックション -- ネットワークの参加者は、自動化されたfacetを使用してトークンを受け取り、価値トランザクションを送信（ウォレット経由）し、ネットワーク上での競合解決をテストできるようになりました。

<!--
- Tokenized Assets — individuals can now ‘color’ IOTA tokens with different attributes that represent real-world assets such as property, IoT devices, or even company equity.
-->
- トークン化された資産 -- 個人は、財産、IoTデバイス、または会社の株式など、現実世界の資産を表す様々な属性を持つIOTAトークンを「カラー化」できます。

<!--
- Prometheus and Grafana integration — node operators can now monitor several metrics by enabling a Grafana dashboard.
-->
- PrometheusとGrafanaの統合 -- ノードオペレーターは、Grafanaダッシュボードを有効にして、複数のメトリクスを監視できるようになりました。

<!--
- Feeless dApps — this release includes a future capability for the IOTA ecosystem: the development of feeless decentralized applications.
-->
- 報酬無しdApps -- このリリースには、IOTAエコシステムのための将来の機能が含まれています。

<!--
Our amazing community has responded with a lot of engagement and enthusiasm. Testers are helping us find bugs and providing valuable feedback. We have already fixed some of them with the minor release [v0.2.1](https://github.com/iotaledger/goshimmer/releases/tag/v0.2.1) and we are currently working on some other improvements that we will shortly release.
-->
私たちの素晴らしいコミュニティは、多くの関与と熱意をもって対応してくれました。テスターの皆さんは、私たちがバグを見つけ、貴重なフィードバックを提供するのを手伝ってくれています。すでにマイナーリリース[v0.2.1](https://github.com/iotaledger/goshimmer/releases/tag/v0.2.1)でいくつかのバグを修正しています。

<!--
*Mana and Autopeering*. This group’s primary research goals have been accomplished. The mana specification has been revised and will be finalized by the next monthly update. We actually have two variants on how to do mana, and because of the modular nature of the protocol, either one would work. Thus we can leave the final decision about the final mana till later.
-->
*Manaとオートピアリング*。このグループの主要な研究目標は達成されました。manaの仕様は修正されており、次回の月次更新までには最終的なものとなる予定です。実際には、manaを行うには２つの方法があり、プロトコルのモジュール化された性質のため、どちらでも動作します。したがって、最終的なmanaについての決定は後回しにできます。

<!--
The autopeering specifications are also almost complete, and they should also be done by the next update. The only thing left to do is to type and publish the results of our simulations. However, we will start this task once the specifications are complete.
-->
オートピアリングの仕様もほぼ完成しており、次回のアップデートまでにはこれも完了しているはずです。後は、シミュレーションの結果を入力して公開するだけです。ただし、この作業は仕様書が完成してから開始する予定です。

<!--
*Networking*. This month, the main focus of the team was on the specifications for rate and congestion control. A preliminary version of these documents is ready, including implementation details. From an algorithmic perspective, our scheduler now also allows fairness in terms of delay, where propagation time for messages is independent of the mana of the issuing nodes (mana only determines nodes throughput).
-->
*ネットワーク*。今月は、レートと輻輳制御の仕様書が中心でした。これらのドキュメントの予備版が完成し、実装の詳細を含めた準備が整いました。アルゴリズムの観点から、メッセージの伝播時間が発行ノードのmanaに依存しない（manaはノードのスループットを決定するだけです）という、遅延の面でも公平性を保つことができるようになりました。

<!--
Additionally, we have started investigating the possibility of having an adaptive global throughput which depends on the health of the nodes (the health of the nodes can refer to their capacity of process messages successfully without being overloaded or falling out of sync).
-->
さらに、ノードの健全性に依存する適応的なグローバルスループットを持つ可能性の調査を開始しました。（ノードの健全性とは、過負荷や同期が取れなくてもメッセージを正常に処理できる能力のことを指します）。

<!--
*dRNG*. In the last few weeks, dRNG group focused on writing peer-reviewed academic papers summarizing our results. We proudly inform you that the first paper about committee selection in DAG distributed ledgers is ready for submission. The second one in which we describe a robust random number beacon should shortly follow.
-->
*dRNG*。ここ数週間、dRNGグループは、私たちの成果をまとめた査読付き学術論文の執筆に注力してきました。DAG分散型台帳における委員会選択に関する最初の論文の投稿準備が整ったことをお知らせします。堅牢な乱数ビーコンを記述した第二報がまもなく投稿される予定です。

<!--
*Protocol*. This month we concluded all research for the protocol specifications and went over it to check if all questions were properly answered. The specification draft is close to completion too!
-->
*プロトコル*。今月はプロトコル仕様書の調査をすべて終了し、疑問点がきちんと解消されているかどうかを確認しました。仕様書案も完成に近づいています。

<!--
We also went to give a theoretical review of the specifications of Chrysalis regarding the modules that were developed by the Protocol Group. The discussions on Chrysalis will still go on for the next few weeks and after that, we should shift our work to review the Coordicide specifications.
-->
また、プロトコルグループで開発されたモジュールについて、Chrysalisの仕様の理論的な見直しを行いました。Chrysalisの議論は今後数週間はまだ続きますが、それ以降はCoordicideの仕様の見直しに業務をシフトしていく必要があります。

<!--
*Specifications*. Besides GoShimmer, our department has also recently been making great progress on the technical specifications for all the components of the protocol. These specifications are the blueprints from which the engineering department will build the node software. Thus upon completing these specifications, research will transfer the Coordicide project to engineering for production.
-->
*仕様書*。GoShimmer以外にも、最近ではプロトコルを構成するすべてのコンポーネントの技術仕様書の作成にも力を入れています。これらの仕様書は、エンジニアリング部門がノードソフトウェアを構築するための設計図となります。これらの仕様書が完成した後、Coordicideの研究は工学部門に移管されて生産されることになります。

<!--
Each author is close to completing a good draft of each specification, representing the end of the first phase of specification. Here are the next steps which will be completed over the next few months:
-->
各作成者は、仕様の第一フェースの終わりを表す、各仕様の優れたドラフトを完成されるところです。数カ月以内に完了するステップは次の通りです。

<!--
- Everyone will read each specification and look for errors, both technical and linguistic. We need to make sure that the documents coherently overlap and cover all aspects of the protocol.
-->
全員がそれぞれの仕様書を読み、技術的にも用語的にも誤りがないかを探します。私たちは文書が首尾一貫して重複し、プロトコルのすべての側面をカバーしていることを確認する必要があります。

<!--
- Next, we need to synchronize the language and the format across all the specifications. Parameters and variables often span several modules of the protocol. We need to make sure these names are all consistent.
-->
次に、すべての仕様で言語とフォーマットを同期させる必要があります。パラメーターや変数は、プロトコルのいくつかのモジュールにまたがっていることがよくあります。これらの名前がすべて一貫していることを確認する必要があります。

<!--
Now that travel restrictions are easing across Europe, our researchers will be able to meet in person and discuss these next steps, expediting the process.
-->
ヨーロッパ全域で渡航制限が緩和され、研究者が直接会って次のステップについて話し合えるようになり、プロセスが迅速化されます。

<!--
- Until our next monthly update, you can stay up to date with the IOTA Research team in the #tanglemath channel on our Discord. You are also welcome to follow and participate in our technical discussions on our public forum: IOTA.cafe.
-->
次回の月次更新までは、Discordの#tanglemathチャネルでIOTA Researchチームの最新情報をお届けします。また、公開フォーラム：iota.cafeでの技術的な議論も歓迎します。

Iota
Research And Development
Pollen
Techupdates
Goshimmer
1.2K claps



Serguei Popov
WRITTEN BY

Serguei Popov
Follow
mathematician
IOTA
IOTA
Follow
Official IOTA Foundation blog
