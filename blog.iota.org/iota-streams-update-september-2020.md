https://blog.iota.org/iota-streams-update-september-2020-c3b8668e231e

# IOTA Streams Update — September, 2020
Jonathan Shaffer
Jonathan Shaffer
Follow
Sep 19 · 4 min read
Image for post
Image for post

Since our *last major update* announcing IOTA Streams as the evolution of Masked Authenticated Messaging (MAM), we’ve made substantial progress on #IOTAStreams and now invite the community to test some of its new functionality, in preparation for the beta release.

IOTA Streams is a framework for sending secure messages and data streams. This provides a universal method for devices to communicate in a secure and private manner on the Tangle. IOTA Streams has been rewritten from the ground up to allow a lot more flexibility, functionality and ease of use.

We are now releasing a major update for IOTA Streams. As a note, the progression of IOTA Streams out of Alpha and into Beta is planned to occur with the transition of the IOTA protocol through Chrysalis Phase 2. The improvements in this update are:

- The Rust based core library is now complete
- C Bindings have been provided for easier compatibility with other languages
- The codebase has been completely converted to binary resulting in an impressive size reduction.
- The Merkle Tree Signature Scheme (MSS) has been replaced with Ed25519 signature scheme and NTRU key encapsulation has been replaced with X25519 key exchange. The MSS was much too wasteful and inefficient in some use cases. With binary, Ed25519 is much more lightweight for embedded applications resulting in a drastic improvement in performance and a considerable memory reduction.
- Single Branch and Multi-Branch Sequencing has been implemented in this release. This functionality should allow for existing MAM implementations to migrate over to Streams much easier due to full compatibility with previous MAM capabilities.
- Core functionality for no-std has been implemented and should be completed after this release candidate is finalized later this month.
- An incompatibility issue with Hornet Nodes has been addressed allowing ease of integration for Streams with Hornet Nodes.

This update brings massive improvements in efficiency to IOTA Streams on it’s road to being enabled as a general embedded application for use in IoT solutions. Current benchmarking estimates put the size reduction of the new Streams library to *a nearly 10X reduction in library size* while having *a near 100X improvement in performance* based on resource constraints and processing time required.

The switch to no-std enables the use of IOTA Streams in low power embedded devices, and also results in significant further size improvements, currently estimated at a 4–5x size reduction. For more information on no-std you can read more in The Embedded Rust Book and to further detail the importance of enabling no-std and it’s relevance to integrating IOTA Streams with embedded devices you can read more in Rust RFC1184.

To note, one of the important improvements notates a feature known as Sequencing. This is a new feature that was not previously enabled on MAM, but helps to cover many of the utilities of MAM while adding more capabilities. Sequencing is a method for mapping and ordering data in a channel. There are two core versions of sequencing:

*Single Branch* — In a single branch channel, all messages will be incrementally sent to a single branch by all publishers within the channel. Each time a publisher posts a message into the chain, all participants increment the sequence state uniformly. This allows for easy transmission of data between directly connected devices (i.e. a subscription to sensor streams) where all data posted is relevant to all parties involved. When looking for the next message, a message identifier can be generated for each public key using the next anticipated sequence state. If the message is found and verified, that sequence state is updated and the next message searched for. For a visual of what this looks like reference the below diagram.

*NOTE*: This is relevant to older MAM designs, as we can now reference previous messages in a message chain.
Image for post
Image for post

*Multi-Branch* — More complex channel configurations use a branch as a point of reference, called the sequencing branch to map individual publishers to the one or more messaging branches found in the channel. This allows for publishers/subscribers to use the sequencing branch as a reference to navigate the messaging branch(es) to easily find the messages from a specific publisher.
Image for post
Image for post

More updated information and tutorials can be found in *[the developer documentation for IOTA Streams](https://docs.iota.org/docs/iota-streams/1.1/overview)*, including reference material for further information on the new Ed25519 signature scheme and X25519 key exchange integrations.

To test some of the functionality yourself, you can check out the develop branch of the *Streams repository* on our Github. As we progress with the implementation and finalize the functionality, we will be working on more comprehensive examples and scenarios in our documentation.

We will also be releasing much more information and material regarding IOTA Streams later this month.

We’d like to take this opportunity to gather feedback, and then adjust the upcoming specification and implementation as necessary, as defined in our *roadmap*. We also welcome others in the community to help develop the necessary Go, JavaScript and Python bindings. Please take the time to fill out the short survey that can be found *here* with input, comments, and feedback on IOTA Streams.

As always, we welcome your comments and questions either here on Medium or in the #streams-discussion or #streams-dev channels on *Discord*. To keep track of future updates, you can also subscribe to the IOTA Newsletter *here*.

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