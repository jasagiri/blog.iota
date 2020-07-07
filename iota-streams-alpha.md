https://blog.iota.org/iota-streams-alpha-7e91ee326ac0

IOTA Streams alpha

Jakub Cech
Follow
Apr 3 · 3 min read


We have been working on a new and vastly improved version of MAM (Masked Authenticated Messaging) for a couple of months now. Today, **we are releasing an alpha implementation**. Together with the release, and as described in this post, we are also **renaming MAM to IOTA Streams**. The implementation, written in Rust, allows you to test how IOTA Streams can be used and how it differs from previous versions of MAM. Please bear in mind that this is an early implementation, and it was mainly created to get feedback as we progress towards the final implementation. Find the repository here.

To summarize some of the changes, as compared to MAM v0 (thanks to Michele Nati):

- **Cryptographic framework** — IOTA Streams is not just about channels.
 IOTA Streams is a framework for cryptographic applications. The Channels functionality, significantly extended from MAM v0, is now just one example of an application that can be implemented on top of IOTA Streams. For purposes where the Channel application isn’t the ideal solution, a different application can be built using the IOTA Streams framework.

- **Channel application** — The IOTA Streams channels application has some novel features. For example, as before one Author can sign messages and multiple Subscribers can receive messages. Subscribers can now however also publish unsigned messages. In contrast, in MAM v0 only channel owners could publish messages.

- **Message types** — In IOTA Streams, messages have a structure based on the header. In MAM v0, the message format was fixed, and if your use case required different message structures, you needed multiple channels for each structure. For example, you may have different message types for monitoring messages and alert messages. In IOTA Streams, you can publish both in the same channel, and applications that read the messages will distinguish them based on their specific headers.

- **Improved access control** — In MAM v0, you needed multiple channels to share various information with different parties. In IOTA Streams, you can apply a different cryptographic mechanism to each message based on its message type. All in one channel. This means that different messages have different access control rules based on their type. And different parties only access the information they have access to.

- **Linking messages** — In MAM v0, all messages were independent, in IOTA Streams, messages can link to one another. This means that a message can link to another message containing supplementary information about the current message.

- **Message sequencing** — In MAM v0, if you wanted to invalidate a message with a newer one, you needed to create a new channel, this increased the application level complexity. In IOTA Streams, you can amend previous messages in an existing channel, and while the older message remains in the Tangle to guarantee integrity, applications can directly retrieve only the newest, valid message. This makes replacing and changing information like credentials much simpler than before. You can update credentials linked to a digital identity, for example, without having to create a new channel and identity like you did with the previous MAM.


To test some of the functionality yourself, see the **Streams [repository](https://github.com/iotaledger/streams)** on our Github. As we progress with the implementation and finalize the functionality, we will be working on more comprehensive examples and scenarios in our documentation.

We’d like to take this opportunity to gather feedback, and then adjust the specification and implementation as necessary to then follow up with a full Rust and C implementations, as defined in our [roadmap](https://roadmap.iota.org/).

**We welcome you to have a look feedback and suggestions on our #streams-discussion channel on the IOTA Discord.**

Thanks to Vlad Semenov for his amazing work on IOTA Streams!


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
