https://blog.iota.org/a-guide-to-upcoming-iota-2-0-coordicide-terminology-856872d7bbfc

A Guide to Upcoming IOTA 2.0 (Coordicide) Terminology

William Sanders
Follow
May 29 · 7 min read

With the Coordicide specifications nearing completion, the research department has been communicating the specifics of the new protocol to the engineering department, external researchers, and the community. This communication requires simple and standard terminology for the new components. However, until recently, researchers, including myself, have mainly used potentially confusing “in house” and ad hoc names.

So, several researchers and engineers began devising proper terminology. Recently, we have completed this task and wish to share these names with you in this blog post.

The new IOTA Protocol is divided into three layers: the **network**, **communication**, and **application** layers. There are parallels between our layers and the top layers of the OSI model, although we caution the reader from deep comparisons. The network layer manages the connections and packet transmissions between nodes. The communication layer creates a standardized platform for storing and communicating information. Developers are then free to design decentralized applications on the application layer while abstracting away the lower layers.

# The network layer

This layer manages the lower layers of internet communication like TCP. It is the most technical, and in some ways the least interesting. In this layer, the connections between nodes are managed by the autopeering and peer discovery modules and the gossip protocol.

# The communication layer
This layer stores and communicates information. This layer contains the “distributed ledger” or the tangle. The rate control and timestamps are in this layer too.

In the communication layer, we see many new features of the protocol. First, our signature “tangle” will be renamed the **message tangle**, and objects called **messages** will replace transactions and bundles. Messages have a flexible format of variable size which are more efficient than bundles of fixed-sized transactions. Also, we will retire the names “trunk and branch”: each message references two other messages which we now call the **parents**.

Messages are issued by a node and then gossiped on the network layer. Besides the parents’ hashes, a message contains certain issuing information (issuing node ID, timestamp, etc), a payload that contains the data (more on this later), and the signature of the issuing node.

The term message was chosen to replace the term “transaction” because the IOTA Protocol is not just a value transfer application, but a platform for securely storing and transmitting data.

# The application layer

The IOTA Protocol allows for a host of applications to run on the message tangle. Anybody can design an application, and users can decide which applications to run on their nodes. These applications will all use the communication layer to broadcast and store data.

However, every node will be required to run certain **core applications** that are necessary for the protocol to operate. These include for example

- The value transfer application
- The distributed random number generator (dRNG for short)
- The Fast Probabilistic Consensus (FPC) protocol

These applications maintain the ledger state, and other applications can also operate on top of these applications.

Applications read and create messages payloads stored on the communication layer. We are developing a flexible framework to mediate this interaction.

# Objects

The basic unit of data in the IOTA Protocol is called an **object**. Every object has a **type** and a size. Rigorously defined in a schema, the type specifies the fields the object contains and how they are arranged. The type also determines how a node parses the object.

Message is an object type. Another example is the **generic data object** which, as the name suggests, is just data. Each node maintains a list of the object types it recognizes and knows how to parse.

As with messages, objects can contain a **payload** field. A payload must always be filled with another object. While parsing an object, a node parses its payload according to its type. If the node does not recognize the type, it treats the payload as a generic data object. An object type can require a payload to have a certain type. Through payloads, objects can nest inside each other, creating a very flexible platform.

In order to be gossiped and stored in the message tangle, each object must be encapsulated inside a message, either directly as a payload, or indirectly as payload of some other object. Informally, a message with payload type X can be referred to as an X message.

For example, a supply chain application can define an object type called “delivery”. The payload of a delivery object could support two different object types: parcel and receipt. When sending a package, a user can issue a delivery message (a message with a delivery object) containing a parcel object describing the package. Each time someone receives the package, they can issue a delivery message with a receipt object which lists the hash of the parcel object.

Anyone not using the delivery application could simply treat all delivery objects as generic data.

However, everyone must recognize certain core object types used by the core applications. Core object types include

- Value objects
- FPC Opinion objects
- dRNG objects
- Salt declaration objects
- Generic data objects

As previously mentioned, messages containing these objects can be called respectively value messages, FPC messages, etc.

All object types include a **version number** so that each application can be updated. The version number of a message indicates which version of the IOTA Protocol the message uses. Indeed, we think that the IOTA Protocol will be around a while and will probably change from time to time. Version numbers let the nodes manage interoperability between these different versions.

# The value transfer application

The most important core application is the **value transfer application** which moves funds and updates the ledger state. This application uses **value objects**. Each value object references two other value objects, and so value objects form an additional Tangle on top of the Message Tangle, called the **value tangle**.

In the value tangle, references represent “approval” and record the outcomes of FPC votes. Roughly speaking, any value objects rejected by FPC will be orphaned in the value tangle. We separate the value and message tangles to reduce the innocent data lost in this process.

Each value object has a payload which only supports an object type called a **transaction**. A transaction contains the input transactions, the output addresses and balances, the mana recipient, a payload, and a signature. Since we are adopting a UTXO scheme, the term transaction makes sense: UTXO stands for Unspent (TX) transaction Output.

The payload of a transaction can support a plethora of object types such as smart contracts. Since the payload is signed, it is fundamentally part of the transaction. Per the UTXO scheme, different transactions which consume the same inputs conflict. Therefore two otherwise identical transactions will conflict if they have different payloads. Thus the payload is intrinsically bound to the spend. This functionality enables a wide variety of applications to be built upon the value transfer application.

Consider the delivery application example. When the receiver must pay for the delivered package, the receipt object could be contained in the payload of the payment transaction. Then the proof of payment would contain the proof of delivery, and either both are included into the tangle or neither are.

# Glossary of terms

We now include a glossary of the new definitions in this document.

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

