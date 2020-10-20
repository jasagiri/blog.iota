https://blog.iota.org/iota-streams-update-september-2020-c3b8668e231e

# IOTA Streams Update — September, 2020
Jonathan Shaffer
Jonathan Shaffer
Follow
Sep 19 · 4 min read
Image for post
Image for post

<!--
Since our *last major update* announcing IOTA Streams as the evolution of Masked Authenticated Messaging (MAM), we’ve made substantial progress on #IOTAStreams and now invite the community to test some of its new functionality, in preparation for the beta release.
-->
*最後のメジャーアップデート*でIOTA StreamsをMasked Authenticated Messaging(MAM)の進化系として発表して依頼、#IOTAStreamsではかなりの進歩を遂げてきました。

<!--
IOTA Streams is a framework for sending secure messages and data streams. This provides a universal method for devices to communicate in a secure and private manner on the Tangle. IOTA Streams has been rewritten from the ground up to allow a lot more flexibility, functionality and ease of use.
-->
IOTA Streamsは、セキュアなメッセージやデータストリームを送信するためのフレームワークです。これにより、デバイスがTangle上で安全かつプライベートな方法で通信するための普遍的な方法を提供します。IOTA Streamsは、より多くの柔軟性、機能性、使いやすさを可能にするために、ゼロから書き直されています。

<!--
We are now releasing a major update for IOTA Streams. As a note, the progression of IOTA Streams out of Alpha and into Beta is planned to occur with the transition of the IOTA protocol through Chrysalis Phase 2. The improvements in this update are:
-->
IOTA Streamsのメジャーアップデートをリリースします。注意点として、IOTA Streamsのアルファ版からベータ版への移行は、Chrysailsフェーズ２でのIOTAプロトコルの移行に合わせて行われる予定です。今回のアップデートでの改善点は以下のとおりです。

<!--
- The Rust based core library is now complete
- C Bindings have been provided for easier compatibility with other languages
- The codebase has been completely converted to binary resulting in an impressive size reduction.
- The Merkle Tree Signature Scheme (MSS) has been replaced with Ed25519 signature scheme and NTRU key encapsulation has been replaced with X25519 key exchange. The MSS was much too wasteful and inefficient in some use cases. With binary, Ed25519 is much more lightweight for embedded applications resulting in a drastic improvement in performance and a considerable memory reduction.
- Single Branch and Multi-Branch Sequencing has been implemented in this release. This functionality should allow for existing MAM implementations to migrate over to Streams much easier due to full compatibility with previous MAM capabilities.
- Core functionality for no-std has been implemented and should be completed after this release candidate is finalized later this month.
- An incompatibility issue with Hornet Nodes has been addressed allowing ease of integration for Streams with Hornet Nodes.
-->
- Rustベースのコアライブラリが完成しました。
- 他の言語との互換性を高めるために、Cのバインディングが提供されています。
- コードベースは完全にバイナリに変換されており、その結果、サイズが大幅に縮小されています。
- Merkle Tree Signature Schema(MSS)はEd25519署名スキームに置き換えられ、NTRU鍵カプセル化はX5519鍵交換に置き換えられました。MSSは無駄が多く、ユースケースによっては効率が悪かったです。バイナリでは、Ed25519は組み込みアプリケーションのために遥かに軽量化されており、パフォーマンスの大幅な改善と大幅なメモリの削減に繋がります。
- シングルブランチとマルチブランチシーケンスは、このリリースで実装されています。この機能は、以前のMAM機能との完全な互換性のため、既存のMAM実装がStreamsへの移行をより簡単に行うことを可能にしています。
- no-stdのコア機能が実装されており、このリリース候補が今月下旬に最終決定された後に完成する予定です。
- Hornet Nodesとの非互換性の問題が解決され、Hornet NodeとStreamsの統合が容易になりました。

<!--
This update brings massive improvements in efficiency to IOTA Streams on it’s road to being enabled as a general embedded application for use in IoT solutions. Current benchmarking estimates put the size reduction of the new Streams library to *a nearly 10X reduction in library size* while having *a near 100X improvement in performance* based on resource constraints and processing time required.
-->
今回のアップデートにより、IOTA Streamsの効率性が大幅に向上し、IoTソリューションで使用する一般的な組み込みアプリケーションとしての利用が可能になります。現在のベンチマークでは、新しいStreamsライブラリのサイズ縮小は、リソースの成約と必要な処理時間に基づいて、パフォーマンスが１００倍近く向上している一方で、ライブラリのサイズは１０倍近く縮小しています。

<!--
The switch to no-std enables the use of IOTA Streams in low power embedded devices, and also results in significant further size improvements, currently estimated at a 4–5x size reduction. For more information on no-std you can read more in The Embedded Rust Book and to further detail the importance of enabling no-std and it’s relevance to integrating IOTA Streams with embedded devices you can read more in Rust RFC1184.
-->
no-stdへの切り替えにより、低消費電力の組み込みデバイスでIOTA Streamsを使用することが可能になりました。また、no-stdを有効にすることの重要性や、IOTA Streamsを組み込みデバイスに統合することとの関連性についてはRust RFC1184を参照してください。

<!--
To note, one of the important improvements notates a feature known as Sequencing. This is a new feature that was not previously enabled on MAM, but helps to cover many of the utilities of MAM while adding more capabilities. Sequencing is a method for mapping and ordering data in a channel. There are two core versions of sequencing:
-->
注意すべきは、重要な改善点の一つとして、シーケンシングとして知られている機能があります。これは、これまでMAMでは有効になっていなかった新機能ですが、より多くの機能を追加しながら、MAMのユーティリティの多くをカバーするのに役立ちます。シーケンシングは、チャネル内のデータをマッピングして順序付けする方法です。シーケンシングには２つのコアバージョンがあります。

<!--
*Single Branch* — In a single branch channel, all messages will be incrementally sent to a single branch by all publishers within the channel. Each time a publisher posts a message into the chain, all participants increment the sequence state uniformly. This allows for easy transmission of data between directly connected devices (i.e. a subscription to sensor streams) where all data posted is relevant to all parties involved. When looking for the next message, a message identifier can be generated for each public key using the next anticipated sequence state. If the message is found and verified, that sequence state is updated and the next message searched for. For a visual of what this looks like reference the below diagram.
-->
*シングルブランチ* - シングルブランチチャネルでは、チャネル内のすべてのパブリッシャーが、全てのメッセージを１つのブランチにインクリメントして送信します。パブリッシャーがチェーンにメッセージを投稿するたびに、すべての参加者が一様にシーケンス状態をインクリメントします。これにより、投稿されたすべてのデータが関係者全員に関連する直接接続されたデバイス間（すなわち、センサーストリームへのサブスクリプション）でのデータ送信が容易になります。次のメッセージを探すとき、次の予想されるシーケンス状態を使用して、各公開鍵に対してメッセージ識別子を生成できます。メッセージが見つかり検証されると、そのシーケンス状態が更新され、次のメッセージが検索されます。これがどのように見えるかについては、以下の図を参照してください。

<!--
*NOTE*: This is relevant to older MAM designs, as we can now reference previous messages in a message chain.
-->
*注*：これは古いMAMデザインに関連するもので、メッセージチェーン内の以前のメッセージを参照できるようになりました。
Image for post
Image for post

<!--
*Multi-Branch* — More complex channel configurations use a branch as a point of reference, called the sequencing branch to map individual publishers to the one or more messaging branches found in the channel. This allows for publishers/subscribers to use the sequencing branch as a reference to navigate the messaging branch(es) to easily find the messages from a specific publisher.
-->
*マルチブランチ* - より複雑なチャネル構成では、シーケンシングブランチと呼ばれる参照点としてブランチを使用し、個々のパブリッシャーをチャネル内の１つ以上のメッセージブランチにマッピングします。これにより、パブリッシャー/サブスクライバーはシーケンスブランチを参照してメッセージブランチを移動し、特定のパブリッシャーからのメッセージを簡単に見つけることができます。
Image for post
Image for post

<!--
More updated information and tutorials can be found in *[the developer documentation for IOTA Streams](https://docs.iota.org/docs/iota-streams/1.1/overview)*, including reference material for further information on the new Ed25519 signature scheme and X25519 key exchange integrations.
-->
新しいEd25519署名スキームとX125519鍵交換の統合に関する詳細な情報のための参考資料を含む、より更新された情報とチュートリアルは*the developer documentation for IOTA Streams](https://docs.iota.org/docs/iota-streams/1.1/overview)*で見つけられます。

<!--
To test some of the functionality yourself, you can check out the develop branch of the *Streams repository* on our Github. As we progress with the implementation and finalize the functionality, we will be working on more comprehensive examples and scenarios in our documentation.
-->
機能の一部を自分でテストするには、Githubの*Streamsリポジトリ*のdevelopブランチをチェックしてください。実装が進み、機能が完成するにつれて、より包括的な例やシナリオをドキュメントにまとめていく予定です。

<!--
We will also be releasing much more information and material regarding IOTA Streams later this month.
-->
また、今月下旬にはIOTA Streamsに関する多くの情報や資料を公開する予定です。

<!--
We’d like to take this opportunity to gather feedback, and then adjust the upcoming specification and implementation as necessary, as defined in our *roadmap*. We also welcome others in the community to help develop the necessary Go, JavaScript and Python bindings. Please take the time to fill out the short survey that can be found *here* with input, comments, and feedback on IOTA Streams.
-->
この機会にフィードバックを集め、必要に応じて仕様や実装を調整したいと思います。また、必要なGo、JavaScript，Pythonバインディングの開発に協力していただける方のご参加もお待ちしております。IOTA Streamsに関するご意見、ご感想、などをお寄せください。

<!--
As always, we welcome your comments and questions either here on Medium or in the #streams-discussion or #streams-dev channels on *Discord*. To keep track of future updates, you can also subscribe to the IOTA Newsletter *here*.
-->
ご意見やご質問は、Mediumや*Discord*の#streams-discussionや#streams-devチャンネルでお待ちしております。今後の更新情報を確認するために、IOTA Newsletterを購読できます。

    Iota
    Research And Development
    Rust
    Iotastreams
    Techupdates

Jonathan Shaffer

Written by
Jonathan Shaffer
Follow
Electrical Engineer @ IOTA Foundation
IOTA
IOTA
Follow
Official IOTA Foundation blog