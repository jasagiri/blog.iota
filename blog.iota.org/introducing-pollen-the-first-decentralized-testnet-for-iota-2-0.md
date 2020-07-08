https://blog.iota.org/introducing-pollen-the-first-decentralized-testnet-for-iota-2-0-349f63f509a1

Introducing Pollen: the First Decentralized Testnet for IOTA 2.0

IOTA Foundation
Follow
Jun 30 · 6 min read

<!--
After years of intensive research, rigorous testing, and tireless efforts by our engineers, we are proud to finally be able to invite everyone to participate in this momentous milestone for the IOTA project. Pollen marks the beginning of the world’s first truly decentralized, scalable, and fee-less Distributed Ledger, which has been IOTA’s promise since day one. Pollen is the first phase in IOTA’s [three-part release strategy](https://blog.iota.org/iota-2-0-introducing-pollen-nectar-and-honey-de7b9c4c8199) that will culminate in our coordinator-less, production-ready network: IOTA 2.0. Pollen is a rapidly developing research testbed where the community, researchers and engineers can test and validate the concepts of [IOTA 2.0](https://blog.iota.org/a-guide-to-upcoming-iota-2-0-coordicide-terminology-856872d7bbfc).
-->
何年にもわたる集中的な研究、厳格なテスト、エンジニアのたゆまぬ努力の末、ついにIOTAプロジェクトの記念すべきマイルストーンに皆様を招待できることを誇りに思います。Pollenは、IOTAが初日から約束していた、世界初の真に分散化され、スケーラブルで、手数料のかからない分散型台帳の始まりを示します。Pollenは、IOTAの[３つのリリース戦略](https://blog.iota.org/iota-2-0-introducing-pollen-nectar-and-honey-de7b9c4c8199)の第一段階で、コーディネーターレスで生産準備の整ったネットワーク、IOTA2.0を完成させます。Pollenは、コミュニティ、研究者、エンジニアがIOTA2.0のコンセプトをテストし、検証できる、急速に発展しているテスト環境です。

<!--
**You can download the new release and see the full changelog here.**
-->
**新しいリリースをダウンロードして、完全な変更履歴を見ることができます。**

<!--
Pollen represents a major upgrade with respect to the previous Alphanet v0.1.3 release. We roughly count 60000 additions and 25000 deletions to the codebase. We have built the foundation for a functional coordinator-less network. From here, iterative improvements to the code will transform Pollen into the final, feature-complete release candidate for IOTA 2.0.
-->
Pollenは以前のAlphanet v0.1.3からのメジャーアップグレードです。コードベースへの追加はおよそ60000件、削除は25000件です。私たちは、機能的なコーディネーターレスネットワークのための基礎を構築しました。ここから、コードへの反復的な改良により、PollenはIOTA2.0のための最終的で機能的に完全なリリース候補へと変化していきます。

<!--
Today’s release includes the following main feature updates:
-->
本日のリリースで、以下のような主な機能のアップデートが行われています。

<!--
- Fast Probabilistic Consensus — IOTA’s new consensus algorithm for a decentralized network. You can read the [research paper here](https://arxiv.org/abs/1905.10895).

- Value Transactions — network participants can now use an automated faucet to receive tokens, send value transactions (via a wallet) and test conflict resolution on the network.

- Tokenized Assets — individuals can now ‘color’ IOTA tokens with different attributes that represent real-world assets such as buildings, IoT devices, or even company equity.

- Prometheus and Grafana integration — node operators can now monitor several metrics by enabling a Grafana dashboard.

- Feeless dApps — this release includes a future capability for the IOTA ecosystem: the development of feeless decentralized applications.
-->
- 高速確率的コンセンサス -- 分散型ネットワークのためのIOTAの新しいコンセンサスアルゴリズム。研究論文は[こちら](https://arxiv.org/abs/1905.10895)から読むことができます。

- Value Transactions -- ネットワーク参加者は、自動化されたfaucetを使ってトークンを受取、value transactionを（ウォレットを介して）送信し、ネットワーク上での紛争解決をテストできるようになりました。

- トークン化されたアセット -- 個人は、建物、IoTデバイス、あるいは企業の株式など、現実世界の資産を表す様々な属性を持つIOTAトークンに「色」を付けられるようになりました。

- PrometheusとGrafanaの統合 -- ノードオペレーターは、Grafanaダッシュボードを有効にすることで、いくつかのメトリクスを監視できるようになりました。

- Feeless dApps -- このリリースは、IOTAエコシステムの将来的な機能であるFeeless分散型アプリケーションの開発が含まれています。

<!--
We have also improved previously released features from the last version of the Alphanet. These include improved stability and instrumentation of both the autopeering and the gossip modules. We have built an enriched dashboard with a brand new Tangle explorer and visualizer. The analysis-server has been refactored from the ground up to support not only the visualization and analysis of the autopeering network but also the real-time update of the Fast Probabilistic Consensus protocol in action.
-->
また、前回のバージョンのAlphanetから以前にリリースされている機能を改良しています。これには、オートピアリングと噂モジュールの安定性と計測機能の改善が含まれます。私たちは、新しいTangleエクスプローラーとビジュアライザーを使って、充実したダッシュボードを構築しました。分析サーバーはオートピアリングネットワークの可視化と分析だけでなく、高速確率的コンセンサスプロトコルのリアルタイム更新もサポートするように一からリファクタリングされています。

<!--
Our interest in this testnet will focus on the overall behavior of the network rather than on its raw performance and user experience. We will gradually work on optimizations and improvements in future iterations. From an implementation point of view, the newly introduced components are still in their infancy (e.g. wallet library, FPC) and several components are not yet optimized (e.g. gossip). Please note that until local snapshots are implemented, we will reset the network from time to time to prevent the database from growing too much and to introduce potential breaking changes.
-->
このテストネットへの関心は、生のパフォーマンスやユーザーエクスペリエンスよりも、ネットワークの全体的な動作に焦点を当てています。今後のイテレーションでは、徐々に最適化と改善に取り組んでいく予定です。実装の観点からは、新しく導入されたコンポーネントはまだ初期段階にあり（例：ウォレットライブラリ、FPC）、いくつかのコンポーネントはまだ最適化されていません（例：噂）。ローカルスナップショットが実装されるまでは、データベースが大きくなりすぎないように、また潜在的な破壊的な変更を導入するためとに、時々ネットワークをリセットすることに注意してください。

<!--
With this new release, we have introduced a new architecture, made up of three separate layers: the network, communication, and application layers. This new architecture will provide support for future features like Tokenization, Scalable Smart Contracts, Feeless dApps and Sharding.
-->
この新しいリリースでは、ネットワーク、通信、アプリケーションの3つのレイヤーで構成される新しいアーキテクチャを導入しました。この新しいアーキテクチャは、トークン化、スケーラブルなスマートコントラクト、Feeless dApps、シャーディングなどの将来の機能をサポートします。

<!--
There are parallels between our layers and the top layers of the OSI model, though we caution the reader from deep comparisons. The network layer manages connections and packet transmission between nodes. The communication layer creates a standardized platform for storing and communicating information. Developers are then free to design decentralized applications on the application layer while abstracting away the lower layers. To learn more about this, you can refer to our [“A Guide to Upcoming IOTA 2.0 Terminology”](https://blog.iota.org/a-guide-to-upcoming-iota-2-0-coordicide-terminology-856872d7bbfc) blogpost.
-->
我々のレイヤーとOSIモデルのトップレイヤーの間には類似性がありますが、深い比較はしないよう注意してください。ネットワーク層は、ノード間の接続とパケット伝送を管理します。communication層は、情報の保存と通信のための標準化されたプラットフォームを作成します。開発者は、改装を抽象化しながら、アプリケーション層で分散型アプリケーションを自由に設計することができます。これについての詳細は、ブログ記事「[A Guide to Upcoming IOTA 2.0 Terminology](https://blog.iota.org/a-guide-to-upcoming-iota-2-0-coordicide-terminology-856872d7bbfc)」を参照してください。

<!--
Pollen’s core is comprised of these features:

- **New Message Layout** — Each message contains the parents’ hashes, issuing information (issuing node ID, timestamp, etc), a payload, the PoW, a nonce and signature of the issuing node.

- **Binary** — As everything is now binary, we have developed a new configurable Proof of Work (PoW) library that will, in future and iterative releases, shift towards our [adaptive PoW](https://blog.iota.org/whos-in-who-s-out-a-rate-control-algorithm-for-the-tangle-c7b5ecf85677) mechanism. We have integrated support for traditional public-key cryptography based on elliptic curves (e.g., Ed25519 and BLS) as well as binary hash functions such as SHA-256, SHA-512 and Blake2b.

- **Ledger State & UTXO** — This GoShimmer version ships with a completely new ledger state based on an extended version of UTXO — the parallel-reality based ledger state. By decoupling consensus and the tracking of balances we enable an unmatched level of flexibility and massively reduce the message complexity by only voting on conflicts.

- **FPC** — The Fast Probabilistic Consensus protocol drives the consensus of our test network. For this first “vanilla” version of the protocol, we are letting nodes trigger FPC in case there are conflicts detected during solidification. The initial opinions are based on arrival times of messages. However, new nodes coming online will not receive messages in the correct order and so may come to the wrong opinion. In future releases, we will add a synching mechanism that will prevent these discrepancies.

- **Randomness** — The randomness used by FPC is generated locally by each node based on the unix-timestamp. More specifically, each minute is divided into epochs of 5 seconds. Clearly, the random number sequence generated by this method is predictable and thus insecure. However, its simplicity and independence from the network or any other component make it very suitable for an initial test of the FPC behavior. The next iteration will rely on a community-based committee dRNG.

- **Local Dashboard** — We have enriched the dashboard by adding a brand new Tangle explorer, Tangle Visualizer and Faucet.

- **Grafana dashboard via Prometheus** — Each node operator can enable the Prometheus plugin and use Grafana to display metrics on network traffic, autopeering status, FPC statistics and more.

- **Network delay app** — We will periodically broadcast a specific network-delay message to the entire network. This will trigger the nodes receiving it to send the timestamp of reception to a central logger, so that we can periodically assess the average network-wide delay and use this information to optimize the tuning of FPC parameters.

- **Wallet library** — We provide a very basic wallet library so that developers and testers can move tokens around. Feel free to contribute with a Wallet UI based on this library.

- **Faucet app** — The GoShimmer dashboard ships with a Faucet section so that you can request tokens to a given address.

- **Client library & API** — Testers, developers and node operators can interact with a GoShimmer node via its Client library and/or API. To learn more about this, you can refer to our [wiki page](https://github.com/iotaledger/goshimmer/wiki/Client-Lib:-Interaction-with-layers).

- **Analysis-server** — We have also improved the analysis server. This shows the overall network status and has a brand new section showing the overall network consensus — a real-time update on the FPC outcome on each conflict. These results are stored on a database so that, together with our community, we can gather enough experimental data to compare with our previous results obtained through [simulations](https://arxiv.org/abs/1911.08787).
-->
Pollenのコアはこれらの機能で構成されています。

- **新しいメッセージレイアウト** -- 各メッセージには、親のハッシュ、発行情報（発行ノードID、タイムスタンプ等）、payload、PoW、nonce、発行ノードの署名が含まれています。

- **バイナリ** -- すべてがバイナリになっているため、将来の反復リリースで[適応PoWメカニズム](https://blog.iota.org/whos-in-who-s-out-a-rate-control-algorithm-for-the-tangle-c7b5ecf85677)に移行する新しく構成可能な作業証明（PoW）ライブラリを開発しました。楕円曲線（Ed25519やBLSなど）に基づく従来の公開鍵暗号化とSHA-256、SHA-512、Blake2bなどのバイナリハッシュ関数のサポートを統合しました。

- **台帳状態とUTXO** -- このGoShimmerバージョンには、UTXOの拡張バージョンに基づく完全に新しい台帳状態（パラレルリアリティベースの台帳状態）が付属しています。コンセンサスとバランスの追跡を分離することにより、比類のないレベルの柔軟性を実現し、競合についてのみ投票することでメッセージの複雑さを大幅に軽減します。

- **FPC** -- 高速確率的コンセンサスプロトコルは、テストネットワークのコンセンサスを促進します。このプロトコルの最初の「素の」バージョンでは、凝固中に競合が検出された場合にノードにFPCを発動させます。最初の意見はメッセージの到着に基づいています。ただし、オンラインになる新しいノードは正しい順序でメッセージを受信しないため間違った意見になる可能性があります。今後のリリースでは、これらの不一致を防ぐ同期メカニズムを追加します。

- **ランダムネス** -- FPCが使用するランダムネスは、UNIXタイムスタンプに基づいて各ノードによってローカルに生成されます。より具体的には、各分は5秒のエポックに分割されます。明らかにこの方法で生成された乱数列は予測可能であるため、安全ではありません。ただし、その単純さとネットワークまたは他のコンポーネントからの独立性により、FPC動作の初期テストには非常に適しています。次のイテレーションは、コミュニティベースの委員会dRNGに依存します。

- **ローカルダッシュボード** -- 新しいTangleエクスプローラー、Tangleビジュアライザー、Faucetを追加して、ダッシュボードを強化しました。

- **Prometheusを介したGrafanaダッシュボード** -- 各ノードオペレーターは、Prometheusプラグインを有効にし、Grafanaを使用して、ネットワークトラフィック、自動ピアリング状態、FPC統計などに関するメトリックを表示できます。

- **ネットワーク遅延アプリ** -- 特定のネットワーク遅延メッセージを定期的にネットワーク全体にブロードキャストします。それを受信するノードが起動され、受信のタイムスタンプが中央ロガーに送信されます。これにより、ネットワーク全体の平均遅延を定期的に評価し、この情報を使用してFPCパラメーターの調整を最適化できます。

- **ウォレットライブラリ** -- 開発者とテスターがトークンを移動できるように、非常に基本的なウォレットライブラリを提供しています。このライブラリに基づいたウォレットUIで貢献してください。

- **Faucetアプリ** -- GoShimmerダッシュボードにはFaucetセクションが付属しているため、特定のアドレスにトークンをリクエストできます。

- **クライアントライブラリとAPI** -- テスター、開発者、ノードオペレーターは、クライアントライブラリやAPIを介してGoShimmerノードとやりとりできます。詳細についてはwikiページを参照してください。

- **分析サーバー** -- 分析サーバーも改善しました。これは、全体的なネットワークステータスを示し、全体的なネットワークコンセンサスを示す新しいセクションがあります。つまり、各競合のFPC結果のリアルタイムな更新です。これらの結果はデータベースに保存されるため、コミュニティとともに、シミュレーションで得られた以前の結果を比較するのに十分な実験データを収集できます。

<!--
We have written a wiki to give the community an opportunity to test out and learn more about this version of the Pollen Testnet:

- Client Library
- [Interaction with layers (HTTP API)](https://github.com/iotaledger/goshimmer/wiki/Client-Lib:-Interaction-with-layers)
- Tutorials
- [Setup a GoShimmer node](https://github.com/iotaledger/goshimmer/wiki/Setup-up-a-GoShimmer-node-(Joining-the-pollen-testnet))
- [Setup monitoring dashboard](https://github.com/iotaledger/goshimmer/wiki/Setting-up-Monitoring-Dashboard)
- [Writing a dApp](https://github.com/iotaledger/goshimmer/wiki/How-to-create-a-simple-dApp)
- [Obtain tokens from the faucet](https://github.com/iotaledger/goshimmer/wiki/How-to-obtain-tokens-from-the-faucet)
- [Use the wallet library](https://github.com/iotaledger/goshimmer/wiki/The-wallet-library)
- Concepts
- [Glossary](https://github.com/iotaledger/goshimmer/wiki/Glossary)
- [Layers](https://github.com/iotaledger/goshimmer/wiki/Layers)
-->
コミュニティでPallenテストネットのこのバージョンをテストして詳細を学ぶ機会を与えるためにwikiを作成しました。

- クライアントライブラリ
- レイヤーと相互作用 (HTTP API)
- チュートリアル
- GoShimmerノードのセットアップ
- 監視ダッシュボードのセットアップ
- dAppの作成
- faucetからトークンを入手する
- ウォレットライブラリを使用する
- コンセプト
- 用語集
- レイヤー

<!--
With our next major release, called Nectar, the remaining components (such as mana, rate control, adaptive PoW, just to mention a few) will be released onto our test network for a fully functional, incentivized testnet.
-->
Nectarと呼ばれる次のメジャーリリースでは、残りのコンポーネント（mana、　レートコントロール、適応型PoWなど）が完全に機能するインセンティブテストネットのテストネットワークをリリースします。

<!--
Pollen is a major milestone for IOTA 2.0. It is a substantial step in testing the core ideas of IOTA’s fully decentralized network.
-->
PollenはIOTA2.0の主要なマイルストーンです。これはIOTAの完全に分散化されたネットワークのコアアイデアをテストする上で重要なステップです。

<!--
We look forward to taking you with us on this exciting journey with Pollen and we hope you will enjoy the development of this project as much as we do. As always, we welcome your comments and questions either here on Medium or in the #tanglemath channel on our Discord. You can also join in the #goshimmer-discussion on Discord.
-->
Pollenとエキサイティングな旅にご参加いただけることを楽しみにしています。このプロジェクトの開発を私たちと同じように楽しんでいただければ幸いです。いつものように、私たちは、ここMediumまたはDiscordの#tanglemathチャネルであなたのコメントと質問を歓迎します。Discordの#goshimmer-discussionに参加することもできます。


Iota
Techupdates
Pollen
Testnet
Honey

2.9K claps






Written by
IOTA Foundation
Follow
The IOTA Foundation was established in Germany in 2017 to support the development of the IOTA platform and related technologies.


IOTA
Follow
Official IOTA Foundation blog

