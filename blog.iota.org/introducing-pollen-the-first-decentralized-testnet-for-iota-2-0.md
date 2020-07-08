https://blog.iota.org/introducing-pollen-the-first-decentralized-testnet-for-iota-2-0-349f63f509a1

Introducing Pollen: the First Decentralized Testnet for IOTA 2.0

IOTA Foundation
Follow
Jun 30 · 6 min read


After years of intensive research, rigorous testing, and tireless efforts by our engineers, we are proud to finally be able to invite everyone to participate in this momentous milestone for the IOTA project. Pollen marks the beginning of the world’s first truly decentralized, scalable, and fee-less Distributed Ledger, which has been IOTA’s promise since day one. Pollen is the first phase in IOTA’s [three-part release strategy](https://blog.iota.org/iota-2-0-introducing-pollen-nectar-and-honey-de7b9c4c8199) that will culminate in our coordinator-less, production-ready network: IOTA 2.0. Pollen is a rapidly developing research testbed where the community, researchers and engineers can test and validate the concepts of [IOTA 2.0](https://blog.iota.org/a-guide-to-upcoming-iota-2-0-coordicide-terminology-856872d7bbfc).

You can download the new release and see the full changelog here.

Pollen represents a major upgrade with respect to the previous Alphanet v0.1.3 release. We roughly count 60000 additions and 25000 deletions to the codebase. We have built the foundation for a functional coordinator-less network. From here, iterative improvements to the code will transform Pollen into the final, feature-complete release candidate for IOTA 2.0.

Today’s release includes the following main feature updates:

- Fast Probabilistic Consensus — IOTA’s new consensus algorithm for a decentralized network. You can read the [research paper here](https://arxiv.org/abs/1905.10895).

- Value Transactions — network participants can now use an automated faucet to receive tokens, send value transactions (via a wallet) and test conflict resolution on the network.

- Tokenized Assets — individuals can now ‘color’ IOTA tokens with different attributes that represent real-world assets such as buildings, IoT devices, or even company equity.

- Prometheus and Grafana integration — node operators can now monitor several metrics by enabling a Grafana dashboard.

- Feeless dApps — this release includes a future capability for the IOTA ecosystem: the development of feeless decentralized applications.

We have also improved previously released features from the last version of the Alphanet. These include improved stability and instrumentation of both the autopeering and the gossip modules. We have built an enriched dashboard with a brand new Tangle explorer and visualizer. The analysis-server has been refactored from the ground up to support not only the visualization and analysis of the autopeering network but also the real-time update of the Fast Probabilistic Consensus protocol in action.

Our interest in this testnet will focus on the overall behavior of the network rather than on its raw performance and user experience. We will gradually work on optimizations and improvements in future iterations. From an implementation point of view, the newly introduced components are still in their infancy (e.g. wallet library, FPC) and several components are not yet optimized (e.g. gossip). Please note that until local snapshots are implemented, we will reset the network from time to time to prevent the database from growing too much and to introduce potential breaking changes.

With this new release, we have introduced a new architecture, made up of three separate layers: the network, communication, and application layers. This new architecture will provide support for future features like Tokenization, Scalable Smart Contracts, Feeless dApps and Sharding.

There are parallels between our layers and the top layers of the OSI model, though we caution the reader from deep comparisons. The network layer manages connections and packet transmission between nodes. The communication layer creates a standardized platform for storing and communicating information. Developers are then free to design decentralized applications on the application layer while abstracting away the lower layers. To learn more about this, you can refer to our [“A Guide to Upcoming IOTA 2.0 Terminology”](https://blog.iota.org/a-guide-to-upcoming-iota-2-0-coordicide-terminology-856872d7bbfc) blogpost.

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

With our next major release, called Nectar, the remaining components (such as mana, rate control, adaptive PoW, just to mention a few) will be released onto our test network for a fully functional, incentivized testnet.

Pollen is a major milestone for IOTA 2.0. It is a substantial step in testing the core ideas of IOTA’s fully decentralized network.

We look forward to taking you with us on this exciting journey with Pollen and we hope you will enjoy the development of this project as much as we do. As always, we welcome your comments and questions either here on Medium or in the #tanglemath channel on our Discord. You can also join in the #goshimmer-discussion on Discord.


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

