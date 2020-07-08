https://blog.iota.org/a-guide-to-upcoming-iota-2-0-coordicide-terminology-856872d7bbfc

A Guide to Upcoming IOTA 2.0 (Coordicide) Terminology

William Sanders
Follow
May 29 · 7 min read

<!--
With the Coordicide specifications nearing completion, the research department has been communicating the specifics of the new protocol to the engineering department, external researchers, and the community. This communication requires simple and standard terminology for the new components. However, until recently, researchers, including myself, have mainly used potentially confusing “in house” and ad hoc names.
-->
Coodicideの仕様が完成間近に迫る中、研究部門では新しいプロトコルの詳細を工学部門、外部の研究者、コミュニティに伝えてきました。このやりとりには新しいコンポーネントのためのシンプルで標準的な用語が必要です。しかし、最近まで私を含む研究者は、主に混乱を招く可能性のある「インハウス」とアドホックという名称を使用してきました。
<!--
So, several researchers and engineers began devising proper terminology. Recently, we have completed this task and wish to share these names with you in this blog post.
-->
そこで、何人かの研究者や技術者がこの適切な用語を考案し始めました。最近、私たちはこの作業を完了したので、このブログ記事でこれらの名前を共有したいと思います。
<!--
The new IOTA Protocol is divided into three layers: the **network**, **communication**, and **application** layers. There are parallels between our layers and the top layers of the OSI model, although we caution the reader from deep comparisons. The network layer manages the connections and packet transmissions between nodes. The communication layer creates a standardized platform for storing and communicating information. Developers are then free to design decentralized applications on the application layer while abstracting away the lower layers.
-->
新しいIOTAプロトコルは、**network**、**communication**、**application**の3つの層に分かれています。我々のレイヤーとOSIモデルの最上位レイヤーの間には類似性がありますが、深い比較はしないように注意してください。network層は、ノード間の接続とパケット伝送を管理します。communication層は、情報の保存と通信のための標準化されたプラットフォームを作成します。開発者は、下位レイヤーを抽象化しながら、application層で分散型アプリケーションを自由に設計することができます。

# The network layer
<!--
This layer manages the lower layers of internet communication like TCP. It is the most technical, and in some ways the least interesting. In this layer, the connections between nodes are managed by the autopeering and peer discovery modules and the gossip protocol.
-->
このレイヤーは、TCPのようなインターネット通信の下位レイヤーを管理します。もっとも技術的で、ある意味では最も面白くないレイヤーです。このレイヤーでは、ノード間の接続は、オートピアリングとピア発見モジュールとゴシッププロトコルによって管理されます。

# The communication layer
<!--
This layer stores and communicates information. This layer contains the “distributed ledger” or the tangle. The rate control and timestamps are in this layer too.
-->
このレイヤーは、情報の保存と通信です。このレイヤーには「分散型台帳」、つまりTangleが含まれています。レート制御やタイムスタンプもこのレイヤーにあります。
<!--
In the communication layer, we see many new features of the protocol. First, our signature “tangle” will be renamed the **message tangle**, and objects called **messages** will replace transactions and bundles. Messages have a flexible format of variable size which are more efficient than bundles of fixed-sized transactions. Also, we will retire the names “trunk and branch”: each message references two other messages which we now call the **parents**.
-->
communicationレイヤーでは、このプロトコルの多くの新機能を見ることができます。まず、我々の署名である「tangle」は**message tangle**に改名され、**messages**と呼ばれるオブジェクトがトランザクションやバンドルに取って代わることになります。Messagesは可変サイズの柔軟なフォーマットを持ち、固定サイズのトランザクションのバンドルよりも効率的です。また、「trankとbranch」という名称を廃止します。それぞれのメッセージは**parent**と呼ばれる他の２つのメッセージを参照します。
<!--
Messages are issued by a node and then gossiped on the network layer. Besides the parents’ hashes, a message contains certain issuing information (issuing node ID, timestamp, etc), a payload that contains the data (more on this later), and the signature of the issuing node.
-->
Messagesはノードによって発行され、ネットワーク層で噂されます。メッセージには親のハッシュの他に、特定の発行情報（発行ノードID、タイムスタンプ等）、データを含むペイロード（これについては後で詳しく説明します）、発行ノードの署名が含まれています。
<!--
The term message was chosen to replace the term “transaction” because the IOTA Protocol is not just a value transfer application, but a platform for securely storing and transmitting data.
-->
メッセージという単語は、「トランザクション」という用語を置き換えるために選択されました。IOTAプロトコルは、単なる値の転送アプリケーションではなく、データを安全に格納及び送信するためのプラットフォームだからです。

# The application layer
<!--
The IOTA Protocol allows for a host of applications to run on the message tangle. Anybody can design an application, and users can decide which applications to run on their nodes. These applications will all use the communication layer to broadcast and store data.
-->
IOTAプロトコルでは、メッセージtangle上で多数のアプリケーションを実行できます。誰でもアプリケーションを設計でき、ユーザーは自分のノードで実行するアプリケーションを決めることができます。これらのアプリケーションはすべてcommunication層を使用してデータをブロードキャストし、保存します。
<!--
However, every node will be required to run certain **core applications** that are necessary for the protocol to operate. These include for example
-->
ただし、すべてのノードは、プロトコルの動作に必要な特定の**コアアプリケーション**を実行する必要があります。これらには以下のものが含まれます。
<!--
- The value transfer application
- The distributed random number generator (dRNG for short)
- The Fast Probabilistic Consensus (FPC) protocol
-->
- 価値移転アプリケーション
- 分散型乱数発生器 (略してdRNG)
- 高速確率的コンセンサス(FPC)プロトコル
<!--
These applications maintain the ledger state, and other applications can also operate on top of these applications.
-->
これらのアプリケーションが台帳の状態を維持しており、他のアプリケーションがこれらのアプリケーション上で動作することも可能です。
<!--
Applications read and create messages payloads stored on the communication layer. We are developing a flexible framework to mediate this interaction.
-->
アプリケーションはcommunication層に格納されたメッセージのペイロードを読み込んで作成されます。この相互作用を仲介する柔軟なフレームワークを開発しています。

# Objects
<!--
The basic unit of data in the IOTA Protocol is called an **object**. Every object has a **type** and a size. Rigorously defined in a schema, the type specifies the fields the object contains and how they are arranged. The type also determines how a node parses the object.
-->
IOTAプロトコルにおけるデータの基本単位は、*object*と呼ばれています。すべてのobjectには*type*とサイズがあります。typeはスキーマで厳密に定義され、objectに含まれるフィールドとその配置方法を指定します。typeはまた、ノードがどのようにobjectを解析するか決定します。

<!--
Message is an object type. Another example is the **generic data object** which, as the name suggests, is just data. Each node maintains a list of the object types it recognizes and knows how to parse.
-->
Messageはobjectのtypeです。もう一つの例は、**generic data object**で、これは名前が示すようにただのデータです。各ノードは認識し、解析する方法を知っているojbectのtypeのリストを維持します。

<!--
As with messages, objects can contain a **payload** field. A payload must always be filled with another object. While parsing an object, a node parses its payload according to its type. If the node does not recognize the type, it treats the payload as a generic data object. An object type can require a payload to have a certain type. Through payloads, objects can nest inside each other, creating a very flexible platform.
-->
messageと同様に、objectには**payload**フィールドを含めるられます。payloadは常に別のobjectで満たされている必要があります。objectの解析中に、ノードはそのtypeに従ってpayloadを解析します。ノードがtypeを認識しない場合、payloadは一般的なデータオブジェクトとして扱われます。オブジェクト型では、payloadが特定のtypeを持つことを要求できます。payloadを介して、objectは相互に入れ子にでき、非常に柔軟なプラットフォームを作成できます。

<!--
In order to be gossiped and stored in the message tangle, each object must be encapsulated inside a message, either directly as a payload, or indirectly as payload of some other object. Informally, a message with payload type X can be referred to as an X message.
-->
噂され、message tangleに格納されるには、各objectをmessage内に直接payloadとして、または間接的に他のobjectのpayloadとしてカプセル化する必要があります。非公式には、payloadのtype X のmessageは X messageと呼ばれます。

<!--
For example, a supply chain application can define an object type called “delivery”. The payload of a delivery object could support two different object types: parcel and receipt. When sending a package, a user can issue a delivery message (a message with a delivery object) containing a parcel object describing the package. Each time someone receives the package, they can issue a delivery message with a receipt object which lists the hash of the parcel object.
-->
例えば、流通アプリケーションは、「delivery」と呼ばれるオブジェクト型を定義できます。delivery objectのpayloadは、小包と領収書という２つの異なるオブジェクトタイプをサポートすることができます。パッケージを送信するとき、ユーザーはパッケージを記述する小包オブジェクトを含むdelivery message（delivery objectを持つmessage）を発行することができます。誰かがパッケージを受け取るたびに、小包オブジェクトのハッシュをリストにした領収書オブジェクトを含むdelivery messageを発行することができます。

<!--
Anyone not using the delivery application could simply treat all delivery objects as generic data.
-->
deliveryアプリケーションを使用していない人は、すべてのdelivery objectを単純に汎用データとして扱えます。

<!--
However, everyone must recognize certain core object types used by the core applications. Core object types include
-->
しかし、誰もがコアアプリケーションで使用される特定のコアオブジェクト型を認識しなければなりません。コアオブジェクト型には以下のものがあります。

<!--
- Value objects
- FPC Opinion objects
- dRNG objects
- Salt declaration objects
- Generic data objects
-->
- 値オブジェクト
- FPCオピニオンオブジェクト
- dRNGオブジェクト
- Salt 宣言オブジェクト
- 汎用データオブジェクト

<!--
As previously mentioned, messages containing these objects can be called respectively value messages, FPC messages, etc.
-->
前述したように、これらのオブジェクトを含むメッセージは、それぞれ、値メッセージ、FPCメッセージ等と呼ぶことができます。

<!--
All object types include a **version number** so that each application can be updated. The version number of a message indicates which version of the IOTA Protocol the message uses. Indeed, we think that the IOTA Protocol will be around a while and will probably change from time to time. Version numbers let the nodes manage interoperability between these different versions.
-->
すべてのオブジェクト型には、アプリケーション毎に更新できるように、**version number**が含まれています。メッセージのversion numberは、メッセージが使用するIOTAプロトコルのバージョンを示します。実際、IOTAプロトコルはしばらくの間存在し、刻一刻と変化しているもの思われます。バージョン番号は、ノードがこれらの異なるバージョン間の相互運用性を管理することを可能にします。

# The value transfer application
<!--
The most important core application is the **value transfer application** which moves funds and updates the ledger state. This application uses **value objects**. Each value object references two other value objects, and so value objects form an additional Tangle on top of the Message Tangle, called the **value tangle**.
-->
もっとも重要なコアアプリケーションは、資金を移動して台帳の状態を更新する**value transfer application**です。このアプリケーションは*value objects*を使用します。各value objectsはmessage tangle上に追加のtangleを形成し、**value tangle**と呼ばれます。

<!--
In the value tangle, references represent “approval” and record the outcomes of FPC votes. Roughly speaking, any value objects rejected by FPC will be orphaned in the value tangle. We separate the value and message tangles to reduce the innocent data lost in this process.
-->
value tangle 内では、参照は「承認」を表し、FPCの投票結果を記録します。大まかにいえば、FPCによって拒否されたvalue ojbectsはvalue tangleの中で孤立してしまいます。このプロセスで失われる無実のデータを減らすために、value tangleとmessage tangleを分離しています。

<!--
Each value object has a payload which only supports an object type called a **transaction**. A transaction contains the input transactions, the output addresses and balances, the mana recipient, a payload, and a signature. Since we are adopting a UTXO scheme, the term transaction makes sense: UTXO stands for Unspent (TX) transaction Output.
-->
各value objectは **transaction**と呼ばれるオブジェクト型のみをサポートするpayloadをもっています。transactionは、入力トランザクション、出力アドレスと残高、mana受信者、payload、および署名を含みます。UTXOスキームを採用しているので、transactionという用語は意味があります。UTXOは、Unspent (TX) tranzaction Output の略です。

<!--
The payload of a transaction can support a plethora of object types such as smart contracts. Since the payload is signed, it is fundamentally part of the transaction. Per the UTXO scheme, different transactions which consume the same inputs conflict. Therefore two otherwise identical transactions will conflict if they have different payloads. Thus the payload is intrinsically bound to the spend. This functionality enables a wide variety of applications to be built upon the value transfer application.
-->
tranzactionのpayloadは、スマートコントラクトのような多数のオブジェクト型をサポートできます。payloadは署名されるので、基本的にtranzactionの一部です。UTXOスキームでは、同じ入力を消費する異なるトランザクションは競合します。したがって、異なるpayloadを持つ２つの同一tranzactionは競合します。このように、payloadは支払いに本質的に結びついています。この機能により、価値移転アプリケーションをベースにした様々なアプリケーションを構築することができます。

<!--
Consider the delivery application example. When the receiver must pay for the delivered package, the receipt object could be contained in the payload of the payment transaction. Then the proof of payment would contain the proof of delivery, and either both are included into the tangle or neither are.
-->
delivery アプリケーションの例を考えてみましょう。受信者が配送された荷物の代金を支払わなければならない場合、領収書オブジェクトは、支払いトランザクションのpayloadに含まれている可能性があります。そうすると、支払証明には配達証明が含まれ、両方がtangleに含まれているか、どちらも含まれていないかのどちらかになります。

# Glossary of terms
<!--
We now include a glossary of the new definitions in this document.
-->
この度、本文書に新しい定義の用語集を掲載しました。

<!--
- **Application Layer**: The top layer hosting all of the applications.
- **Core Application**: An application that must be run by all users.
- **Communication Layer**: The layer dealing with messages and the message tangle.
- **Core Object type**: An object type which must be parsed by all users
- **Generic Data Object**: The most basic object type. All unrecognized data objects are treated as this.
- **Network Layer**: The most basic layer which manages the connections and gossiping between neighbors.
- **Message**: The object type which is gossiped between neighbors. All gossiped information is included in a message.
- **Message Tangle**: The collection of all messages.
- **Object**: The most basic unit of information of the IOTA Protocol. Each object has a type and size and contains data.
- **Payload**: A field in an object which can only be filled by another object.
- **Tangle**: An append only data structure where each item references two other items.
- **Transaction**: The payload of a value object. It contains the particulars of a transfer of funds.
- **Value Object**: The basic object of the value transfer application
- **Value Tangle**: The collection of all value objects.
- **Value Transfer Application**: The application which maintains the ledger state.
- **Version number**: Indicates the correct format of each type.
-->

- **Application Layer**: すべてのアプリケーションをホストする最上位層。
- **Core Application**: すべてのユーザーが実行しなければならないアプリケーション。
- **Communication Layer**: メッセージとメッセージtangleを扱う層。.
- **Core Object type**: すべてのユーザーが解析しなければならないオブジェクト型
- **Generic Data Object**: 最も基本的なオブジェクト型認識されていないデータオブジェクトはすべてこれとして扱われます。
- **Network Layer**: 最も基本的なレイヤーで、隣人の間の接続と噂を管理します。
- **Message**: 隣人の間で噂されるオブジェクト型。噂された情報はすべてメッセージに含まれます。
- **Message Tangle**: すべてのメッセージのコレクション。
- **Object**: IOTAプロトコルの最も基本的な情報単位。各オブジェクトはtypeとサイズを持ち、データを含みます。
- **Payload**: object内のフィールドで、他のオブジェクトでしか埋められないもの。
- **Tangle**: 各項目は他の2つの項目を参照します。
- **Transaction**: 値オブジェクトのpayload。これには資金移動の詳細が含まれます。
- **Value Object**: 値オブジェクトのpayload。値転送アプリケーションの基本的なオブジェクト。
- **Value Tangle**: すべての値オブジェクトのコレクション。
- **Value Transfer Application**: 台帳の状態を維持するアプリケーション。
- **Version number**: 各型の正しいフォーマットを示す。


Iota
Techupdates
Coordicide
Specifications
Research And Development

1.4K claps






Written by
William Sanders
Follow
I am mathematician doing research for IOTA foundation. I specialize in commutative algebra and category theory.


IOTA
Follow
Official IOTA Foundation blog

