https://blog.iota.org/iota-stronghold-6ce55d311d7c

# Introducing IOTA Stronghold
Daniel Thompson-Yvetot
Daniel Thompson-Yvetot
Follow
Jul 30 · 6 min read
Image for post
Image for post
<!--
*Stronghold is a collection of multipurpose libraries for securely managing passwords, personal data, and private keys.*
*The Official Repository: https://github.com/iotaledger/stronghold.rs*
-->
*Strongholdは、パスワードや個人情報、秘密鍵を安全に管理するための多目的ライブラリです。*
*公式レポジトリ：https://github.com/iotaledger/stronghold.rs*

<!--
The internet can be a dangerous place, and 2020 seems to be a year where literally anything goes. Whether deep-fakes, DDoS attacks, ransomware, clipboard leaks, zoom insecurity or the dark-patterns of browser fingerprinting — these risks touch all of our digital lives each and every day. At the IF, we are painfully aware of the extent to which third-party dependencies can introduce risks.
-->
インターネットは危険な場所である可能性があり、2020年は文字通り何でもありの年になりそうです。ディープフェイク、DDoS攻撃、ランサムウェア、クリップボード漏洩、zoomの安全性の欠如、ブラウザのフィンガープリントの暗黒パターンなど、これらのリスクは毎日、私達のデジタルライフのすべてに関係しています。IFでは、サードパーティの依存関係がリスクをもたらす可能性があることを痛感しています。

<!--
What we have learned from the perpetual attacks on our ecosystem is that security must be a guiding principle in Distributed Ledger Technologies, not an afterthought. We need to be vigilant about our entire stack and operations. The mindset of “security-first” must affect not only our practices but also drive our software design decisions.
-->
エコシステムへの永続的な攻撃から学んだことは、セキュリティは後付ではなく、分散型レジェンド・テクノロジーズの指針となる原則でなければならないということです。私達はスタック全体とオペレーションを警戒しなければなりません。「セキュリティ第一主義」の考え方は、私達の実践に影響を与えるだけでなく、ソフトウェア設計の決定にも影響を与えなければなりません。

<!--
As a foundation committed by charter to the dual notions of contributing to open-source and furthering education, we are morally compelled to put our energies into improving the greater good — not merely our own lot.
-->
オープンソースへの貢献と教育の発展という２つの概念にコミットしている財団として、私達は道徳的に、自分たちの利益だけではなく、より大きな利益を向上させるためにエネルギーを注ぐことを余儀なくされています。

<!--
In this context of being a “good digital citizen”, the best thing we can do is to offer a means to enhance the security posture of all types of software, including cryptocurrencies, distributed ledger technologies, and even financial infrastructure like exchanges and custody wallets. Specifically, we seek to strengthen the working environment for developers, enhance the security of applications, and give everyone better options for securely storing and safely using high-value digital secrets.
-->
このような「良きデジタル市民」を目指す中で、私達ができることは、暗号通貨や分散型台帳技術、更には取引所やカストディ・ウォレットなどの金融インフラを含むあらゆるソフトウェアのセキュリティ耐性を強化するための手段を提供することです。具体的には、開発者の作業環境を強化し、アプリケーションのセキュリティを強化し、価値の高いデジタルシークレットを安全に保管し、安全に利用するためのより良い選択肢を誰にでも提供することを目指しています。

<!--
There are many challenges involved in securely managing digital secrets like passwords, vehicle access codes, and wallet seeds:
-->
パスワード、車両のアクセスコード、ウォレットのシード等のデジタル秘密を安全に管理するためには、多くの課題があります。

<!--
- High-value secrets like private keys need to be encrypted at rest, using modern and secure algorithms
- Such secrets need to be purged from device memory immediately after use
- Users must be able to configure systems to their security needs
- Applications need to run on any type of hardware from phones to cars, where possible leveraging Trusted Execution Environments.
- Must be extensible with hardware security like Yubikey and Ledger Nano
- Must use as few external dependencies as possible
- Must be fully audited by third-party security professionals
- The underlying libraries need to be managed by a reliable and active maintainer
-->
- 秘密鍵のような高価値の秘密は、最新の安全なアルゴリズムを使用して、平常時に暗号化する必要があります。
- このような秘密は、使用後すぐにデバイスのメモリから削除する必要があります。
- ユーザーは、セキュリティのニーズに合わせてシステムを構成できなければなりません。
- アプリケーションは、携帯電話から自動車まで、あらゆる種類のハードウェア上で動作する必要があり、可能であれば、Trusted Execution Environmentsを活用する必要があります。
- YubikeyやLedger Nanoのようなハードウェア・セキュリティで拡張可能である必要があります。
- 可能な限り少ない外部依存関係を使用する必要があります。
- 第三者のセキュリティ専門家による完全な監査を受けている必要があります。
- 基礎となるライブラリは、信頼性の高いアクティブなメンテナによって管理される必要があります。

<!--
We spent some time investigating existing projects, but unfortunately, we couldn’t tick all the boxes and decided to forge ahead and build the Stronghold to secure all of the above.
-->
既存のプロジェクトの調査に時間を費やしましたが、残念ながら全ての箱にはチェックを入れることができず、上記のすべてを確保するために、先に進んでStrongholdをビルドすることにしました。

## Stronghold, in a nutshell
<!--
Stronghold is a secure software implementation with the sole purpose of isolating digital secrets from exposure to hackers and accidental leaks. It uses versioned, file-based snapshots with double-encryption that can be easily backed up and securely shared between devices. Written in Rust, it has strong guarantees of memory safety and process integrity. The high-level developer-friendly libraries integrate the IOTA protocol and serve as a reference implementation for anyone looking for inspiration or best-in-class tooling. The low-level libraries have no notion of cryptocurrency embedded within them and can be used in their entirety without the high-level libraries. In other words, anyone from any industry can use it.
-->
Strongholdは、ハッカーへの暴露や偶発的な漏洩からデジタル機密を隔離することを唯一の目的とした安全なソフトウェアの実装です。バージョン管理され、二重に暗号化されたファイルベースのスナップショットを使用しており、デバイス間でかんたんにバックアップし、安全に共有できます。Rustで書かれており、メモリ安全性とプロセスの完全性が強力に保証されています。高レベルの開発者向けライブラリは、IOTAプロトコルを統合し、インスピレーションやクラス最高のツールを探している人のためのリファレンス実装として機能します。低レベルのライブラリには暗号通貨の概念が組み込まれておらず、高レベルのライブラリを使用せずにそのまま使用することができます。言い換えれば、どのような業界の人でも使うことができます。

<!--
At IOTA, we will begin rolling out the IOTA Stronghold to secure the new wallet. In the next phase, we will have tight integration with IOTA Identity. We look forward to working with exchanges to discover new patterns of usage for Stronghold and are also excited about the many possibilities it brings to our work with smart contracts.
-->
IOTAでは、新しいウォレットのセキュリティを確保するために、IOTA Strongholdの展開を開始します。次の段階では、IOTA Identityとの緊密な統合が予定されています。私達は、取引所と協力してStrongholdの新しい利用パターンを発見することを楽しみにしています。また、スマートコントラクトとの連携がもたらす多くの可能性にも期待しています。

## For the Technical Professionals
<!--
The primary task of Stronghold is to isolate the activity of “privileged” functions from other programs. For example, a primary goal is to create a software enclave where private keys are used to sign messages without revealing those keys to other functions. In the near future, we expect to move the Stronghold stack to Trusted Execution Environments (TEE) and integrate it into custom hardware.
-->
Strongholdの主なタスクは、「特権的な」機能の活動を他のプログラムから隔離することです。例えば、秘密鍵を使用してメッセージに署名する際、他の関数に鍵を公開しないようなソフトウェアの飛び地を作ることが主な目標です。近い将来、StrongholdスタックをTrusted Execution Environments(TEE)に移行し、カスタムハードウェアに統合することを期待しています。

<!--
It is based on a suite of low-level libraries known as Stronghold Engine that provide tooling and algorithms to build secure systems in Rust in a way that can be embedded and deployed to devices regardless of architecture and operating system. This collection of libraries deals with the obfuscation, encryption, usage, and sharing of secrets between devices. It has been in research and development for the past 8 months — beginning at https://ionary.dev — and it culminated in a successfully completed grant from the IOTA Ecosystem Development Fund. Its code can be reviewed here at GitHub and its principal author, Tensor, has prepared both a retrospective about its development as well as an introductory video.
-->
Stronghold Engineとして知られる低レベルのライブラリ群をベースにしており、アーキテクチャやオペレーティングシステムに関係なくデバイスへの組み込みやデプロイが可能な方法で、Rustでセキュアなシステムを構築するためのツールやアルゴリズムを提供しています。このライブラリのコレクションは、デバイス間の秘密の難読化、暗号化、利用、共有を扱います。https://ionary.dev から始まり、過去８ヶ月間研究開発が続けられてきましたが、IOTAエコシステム開発基金からの助成金を受けて最高潮に達しました。コードはGitHubでレビューでき、主要な作者であるTensorは開発の回顧と紹介ビデオを用意しました。

<!--
Stronghold is written in stable Rust and has four primary components:
-->
Strongholdは安定したRustで書かれており、４つの主要なコンポーネントを持っています。

<!--
- low-level, modular libraries for building a secure blackbox of versioned data with a file-backed snapshot-oriented persistence layer that enables users to securely share their data between devices (beta quality)
-->
- ユーザーがデバイス間でデータを安全に共有できるように、ファイルをバックアップしたスナップショット指向の永続化レイアを備えた、バージョン管理されたデータの安全なブラックボックスを構築するための低レベルのモジュール式ライブラリ。(ベータ品質)

<!--
- high-level libraries that integrate IOTA with the low-level libraries and expose them in an intuitive way (pre-alpha, currently in active development)
-->
- IOTAと低レベルライブラリを統合し、直感的な方法で公開する高レベルライブラリ（プレアルファ、現在開発中）

<!--
- an actor-model interface for security-focused applications that use Rust (pre-alpha, currently in active development)
-->
Rustを使用するセキュリティに特化したアプリケーションのためのアクターモデルインタフェース（プレアルファ、現在開発中）

<!--
- FFI bindings to other programming languages like C, Java and Node.js (available soon)
-->
C、Java、Node.jsなどの他のプログラミング言語へのFFIバインディング（まもなく利用可能）

## What will you do with Stronghold?
<!--
Because of its composability, there are many exciting applications that can be built using Stronghold — not just cryptocurrency wallets. Its low-level engine is totally use-case agnostic and so flexible that the encryption algorithms can be swapped out at your leisure, composed in new ways, and extended with other parts of virtually any stack. The high-level libraries will be so solid that you can entrust them with doing things the right way.
-->
その構成性の高さから、暗号通貨のウォレットだけでなく、Strongholdを使って構築できるエキサイティングなアプリケーションはたくさんあります。低レベルのエンジンは使用ケースにとらわれず、暗号化アルゴリズムを自由に交換したり、新しい方法で構成したり、事実上あらゆるスタックの他の部分を使って拡張したりできるほど柔軟です。高レベルのライブラリは、あなたが正しい方法で物事を行うことを彼らに任せることができるように、非常に堅固なものになるでしょう。

<!--
Here are just a few ideas of the possibilities to help you get your juices flowing:
-->
ここでは、あなたのジュースが流れるのを助ける可能性のいくつかのアイデアをご紹介します。

### Wallet
Image for post
Image for post

<!--
Alice’s IOTA wallet is protected by Stronghold, which she can configure (as seen in the image above) to watch over the activity in her wallet and prevent dangerous events from taking place.
-->
アリスのIOTAウォレットはStrongholdによって保護されており、（上の画像のように）設定することで、ウォレットの中の活動を見守り、危険なイベントが起こるのを防ぐことができます。

### Exchanges
<!--
Alice the daytrader and her exchanges can collaboratively use Stronghold distributed key generation and BLS threshold signatures for enhancing the auditability of high-volume IOTA token transfers.
-->
デイトレーダーのアリスとその取引所は、大量のIOTAトークン転送の監査可能性を高めるために、Strongholdの分散鍵生成とBLSのしきい値署名を共同で使用できます。

### Password Management Tools
<!--
Securely scrubbing memory after using a password is a common vulnerability in password managers. Stronghold will help Alice to be safer.
-->
パスワードを使用した後にメモリを安全にスクラブすることは、パスワードマネージャの一般的な脆弱性です。Strongholdはアリスをより安全にしてくれます。

### Multimedia Center
<!--
Alice rents a movie using her Phone to playback on her Smart TV. The movie is sent to the TV as an encrypted stream and a decryption key is synced to her device’s Stronghold. After 48 hours the key is deleted from her Stronghold by the service and the video can no longer be played.
-->
アリスはスマートテレビで再生するために電話を使って映画をレンタルしています。映画は暗号化されたストリームとしてテレビに送信され、復号化キーは彼女のデバイスのStrongholdに同期されます。４８時間後に鍵はサービスによってStrongholdから削除され、ビデオは再生できなくなります。

### GDPR Data Processors and Controllers
<!--
Instead of storing personally identifiable information in a centralized database that can get stolen in one fell swoop, Alice can choose to share and revoke access to her data directly from her Stronghold-powered application.
-->
個人を特定できる情報を一気に盗まれる可能性のある中央集権データベースに保存する代わりに、アリスはStrongholdを搭載したアプリケーションから直接自分のデータを共有したり、アクセスを取り消したりできます。

### Travel Agency
Image for post
Image for post

<!--
Alice securely shares her passport information with her travel agent, and because of the way that Strongholds sync with each other, when the travel agent no longer needs the passport data, she can remove his access to it.
-->
アリスは旅行代理店とパスポート情報を安全に共通しており、Strongholdがお互いに同期しているため、旅行代理店がパスポートデータを必要としなくなったときには、旅行代理店からのアクセスを削除できます。

### Software Developers
<!--
Using the Stronghold command-line interface or system daemon as a local secret and retrieval system enhances Alice the programmer’s operational security and helps prevent accidental disclosure.
-->
Strongholdのコマンドラインインタフェースやシステムデーモンをローカル秘密検索システムとして使用することで、プログラマの運用セキュリティを強化し、偶発的な漏洩を防げれます。

## The Future
<!--
Stronghold has not yet been formally audited for security vulnerabilities and is moving toward the next phase of public community engagement. We are now making this work public, in the hopes that the open-source and security communities find the opportunity to review the design and implementation. At any rate, in late Autumn 2020, Stronghold will undergo a full external security audit. After the audit’s conclusion and respective revisions, we will declare the project mature enough to be used in your projects.
-->
Strongholdは、まだ正式なセキュリティ脆弱性の監査を受けておらず、パブリックコミュニティの関与の次の段階に向かっています。オープンソースコミュニティとセキュリティコミュニティが設計と実装を見直す機会を見つけてくれることを期待して、今、この作業を公開しています。何はともあれ、２０２０年の晩秋には、Strongholdは完全な外部セキュリティ監査を受ける予定です。監査の結論とそれぞれの修正の後、私達はこのプロジェクトがあなたのプロジェクトで使用できるほど成熟していると宣言します。

<!--
The very first internal test of Stronghold will be in its integration with the forthcoming official wallet built for Chrysalis (which will be externally audited before release). It will be the storage mechanism for securing seeds and personally identifiable information. Stronghold will also enable users to enhance their wallet security with Ledger secure storage and Yubikey access.
-->
Strongholdの最初の内部テストでは、Chrysails用に構築された公式ウォレットとの統合が近々行われます（リリース前に外部監査が行われます）。Strongholdは、種や個人を特定できる情報を保護するためのストレージメカニズムとなります。Strongholdはまた、ユーザがLedgerの安全なストレージとYubikeyへのアクセスによってウォレットのセキュリティを強化することも可能にします。

Official Repository: https://github.com/iotaledger/stronghold.rs

Low-Level Video Introduction: https://youtu.be/pd-XWaGLIck

As always, you can join our Discord to give feedback, comments, and join the discussion.

    Iota
    Techupdates
    Research And Development
    Stronghold
    Announcements

Daniel Thompson-Yvetot

Written by
Daniel Thompson-Yvetot
Follow
Open-source, hi-tech, big fun!
IOTA
IOTA
Follow
Official IOTA Foundation blog