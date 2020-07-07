https://blog.iota.org/iota-streams-alpha-7e91ee326ac0

IOTA Streams alpha

Jakub Cech
Follow
Apr 3 · 3 min read

<!--
We have been working on a new and vastly improved version of MAM (Masked Authenticated Messaging) for a couple of months now. Today, **we are releasing an alpha implementation**. Together with the release, and as described in this post, we are also **renaming MAM to IOTA Streams**. The implementation, written in Rust, allows you to test how IOTA Streams can be used and how it differs from previous versions of MAM. Please bear in mind that this is an early implementation, and it was mainly created to get feedback as we progress towards the final implementation. Find the repository here.
-->
私たちは数カ月前から、MAM(Masked Authenticated Messaging)の大幅に改良された新しいバージョンに取り組んできました。本日、**アルファ版の実装をリリースします**。このリリースと同時に、この記事で説明するように、**IOTA Streams**にMAMを再定義します。Rustで書かれたこの実装では、IOTA Streamsがどのように使えるのか、以前のMAMとどのように違うのかをテストすることができます。これは初期の実装であり、最終的な実装に向けて進んでいく中でフィードバックを得るために作成されたものです。レポジトリはこちら。

<!--
To summarize some of the changes, as compared to MAM v0 (thanks to Michele Nati):
-->
MAM v0と比較して、いくつかの変更点をまとめます（Michele Nati氏に感謝します）。

<!--
- **Cryptographic framework** — IOTA Streams is not just about channels.
 IOTA Streams is a framework for cryptographic applications. The Channels functionality, significantly extended from MAM v0, is now just one example of an application that can be implemented on top of IOTA Streams. For purposes where the Channel application isn’t the ideal solution, a different application can be built using the IOTA Streams framework.
-->
- **暗号フレームワーク** -- IOTA Streamsはチャネルだけではありません。
　IOTA Streamsは、暗号化アプリケーションのためのフレームワークです。MAM v0から大幅に拡張されたチャネル機能は、IOTA Streams上に実装できるアプリケーションの一例にすぎません。チャネルアプリケーションが理想的なソリューションではない場合には、IOTA Streamsフレームワークを使って別のアプリケーションを構築できます。

<!--
- **Channel application** — The IOTA Streams channels application has some novel features. For example, as before one Author can sign messages and multiple Subscribers can receive messages. Subscribers can now however also publish unsigned messages. In contrast, in MAM v0 only channel owners could publish messages.
-->
- **チャネルアプリケーション** -- IOTA Streamsのチャネルアプリケーションには、いくつかの新しい機能があります。例えば、以前と同様に、1人の著者がメッセージに署名し、複数の購読者がメッセージを受信できます。しかし、購読者は署名のないメッセージを公開することもできます。これとは対照的に、MAM v0では、チャネルの所有者のみがメッセージを公開することができました。

<!--
- **Message types** — In IOTA Streams, messages have a structure based on the header. In MAM v0, the message format was fixed, and if your use case required different message structures, you needed multiple channels for each structure. For example, you may have different message types for monitoring messages and alert messages. In IOTA Streams, you can publish both in the same channel, and applications that read the messages will distinguish them based on their specific headers.
-->
- **メッセージ型** -- IOTA Streamsでは、メッセージはヘッダにーに基づいた構造を持っています。MAM v0では、メッセージのフォーマットは固定されており、ユースケースの異なるメッセージ構造が必要な場合は、各構造に対して複数のチャネルが必要でした。例えば、モニタリングメッセージとアラートメッセージで異なるメッセージ型を持つことができます。IOTA Streamsでは、両方を同じチャネルで公開することができ、メッセージを読むアプリケーションは、特定のヘッダーに基づいてこれらを区別します。

<!--
- **Improved access control** — In MAM v0, you needed multiple channels to share various information with different parties. In IOTA Streams, you can apply a different cryptographic mechanism to each message based on its message type. All in one channel. This means that different messages have different access control rules based on their type. And different parties only access the information they have access to.
-->
- **アクセス制御の改善** -- MAM v0では、様々な情報を異なる関係者と共有するために複数のチャネルが必要でした。IOTA Streamsでは、メッセージ型に応じて、各メッセージに異なる暗号メカニズムを適用することができます。つまり、異なるメッセージは、その型に基づいて異なるアクセス制御ルールを持つことになります。そして、異なる当事者は、自分がアクセスできる情報のみにアクセスします。

<!--
- **Linking messages** — In MAM v0, all messages were independent, in IOTA Streams, messages can link to one another. This means that a message can link to another message containing supplementary information about the current message.
-->
- **リンクメッセージ** -- MAM v0では、すべてのメッセージは独立していましたが、IOTA Streamsでは、メッセージは互いにリンクできます。これはあるメッセージが、現在のメッセージに関する補足情報を含む別のメッセージにリンクできることを意味します。

<!--
- **Message sequencing** — In MAM v0, if you wanted to invalidate a message with a newer one, you needed to create a new channel, this increased the application level complexity. In IOTA Streams, you can amend previous messages in an existing channel, and while the older message remains in the Tangle to guarantee integrity, applications can directly retrieve only the newest, valid message. This makes replacing and changing information like credentials much simpler than before. You can update credentials linked to a digital identity, for example, without having to create a new channel and identity like you did with the previous MAM.
-->
- **メッセージのシーケンス** -- MAM v0では、メッセージを新しいメッセージで無効化するには、新しいチャネルを作成する必要があり、アプリケーションレベルでの複雑さが増していました。IOTA Streamsでは、既存のチャネル内の以前のメッセージを修正することができ、古いメッセージは完全性を保証するためにTangleに残りますが、アプリケーションは最新の有効なメッセージのみを直接取得できます。これにより、資格情報のような情報の置き換えや変更が依然よりもはるかに簡単になりました。例えば、デジタルIDにリンクされた資格情報を更新する場合、以前のMAMで行ったように新しいチャネルとIDを作成する必要はありません。

<!--
To test some of the functionality yourself, see the **Streams repository** on our Github. As we progress with the implementation and finalize the functionality, we will be working on more comprehensive examples and scenarios in our documentation.
-->
機能の一部を自分でテストするには、Githubの**Strems リポジトリ**を参照してください。実装が進み、機能が完成するにつれて、より包括的な例やシナリオをドキュメントにまとめていく予定です。

<!--
We’d like to take this opportunity to gather feedback, and then adjust the specification and implementation as necessary to then follow up with a full Rust and C implementations, as defined in our roadmap.
-->
この機会にフィードバックを集め、必要に応じて仕様や実装を調整し、ロードマップで定義されているRustとCの完全な実装をフォローしていきたいと考えています。

<!--
**We welcome you to have a look feedback and suggestions on our #streams-discussion channel on the IOTA Discord.**

Thanks to Vlad Semenov for his amazing work on IOTA Streams!
-->
IOTA Discordの#streams-discussionチャネルでのご意見・ご感想をお待ちしております。

IOTA Streamsでの素晴らしい仕事をしてくれたVlad Semlenovに感謝します。


IOTA
Official IOTA Foundation blog
Follow

1.99K 





Iota
Dlt
Research And Development
Rust
Iotastreams

1.99K claps


Written by
Jakub Cech
Follow
Director of Engineering @IOTA Foundation


IOTA
Follow
Official IOTA Foundation blog
