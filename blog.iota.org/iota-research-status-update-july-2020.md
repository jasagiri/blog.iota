https://blog.iota.org/iota-research-status-update-july-2020-5a863a1dfae6

IOTA Research Status Update July 2020
Serguei Popov
Serguei Popov
Follow
Jul 10 · 4 min read



This month, we were honored to release Pollen, the first testnet version of IOTA 2.0 to include Fast Probabilistic Consensus, the consensus mechanism for the post-Coordicide IOTA. Work continues on the finalization and further integration of our research specifications into future updates, with a major milestone this month being the finalized version of two types of mana implementations.

Below are the updates from several of our research groups.

*GoShimmer Implementation*. Last week, we released [Pollen](https://blog.iota.org/introducing-pollen-the-first-decentralized-testnet-for-iota-2-0-349f63f509a1), our first fully decentralized testnet based on GoShimmer v0.2.0. Pollen represents a major upgrade with respect to the previous Alphanet v0.1.3 release. We count roughly 60,000 additions and 25,000 deletions to the [codebase](https://github.com/iotaledger/goshimmer). Some of the newly added features include:

- Fast Probabilistic Consensus (FPC) — IOTA’s new consensus algorithm for a fully decentralized network. You can read the [research paper here](https://arxiv.org/abs/1905.10895).

- Value Transactions — network participants can now use an automated faucet to receive tokens, send value transactions (via a wallet) and test conflict resolution on the network.

- Tokenized Assets — individuals can now ‘color’ IOTA tokens with different attributes that represent real-world assets such as property, IoT devices, or even company equity.

- Prometheus and Grafana integration — node operators can now monitor several metrics by enabling a Grafana dashboard.

- Feeless dApps — this release includes a future capability for the IOTA ecosystem: the development of feeless decentralized applications.

Our amazing community has responded with a lot of engagement and enthusiasm. Testers are helping us find bugs and providing valuable feedback. We have already fixed some of them with the minor release [v0.2.1](https://github.com/iotaledger/goshimmer/releases/tag/v0.2.1) and we are currently working on some other improvements that we will shortly release.

*Mana and Autopeering*. This group’s primary research goals have been accomplished. The mana specification has been revised and will be finalized by the next monthly update. We actually have two variants on how to do mana, and because of the modular nature of the protocol, either one would work. Thus we can leave the final decision about the final mana till later.

The autopeering specifications are also almost complete, and they should also be done by the next update. The only thing left to do is to type and publish the results of our simulations. However, we will start this task once the specifications are complete.

*Networking*. This month, the main focus of the team was on the specifications for rate and congestion control. A preliminary version of these documents is ready, including implementation details. From an algorithmic perspective, our scheduler now also allows fairness in terms of delay, where propagation time for messages is independent of the mana of the issuing nodes (mana only determines nodes throughput).

Additionally, we have started investigating the possibility of having an adaptive global throughput which depends on the health of the nodes (the health of the nodes can refer to their capacity of process messages successfully without being overloaded or falling out of sync).

*dRNG*. In the last few weeks, dRNG group focused on writing peer-reviewed academic papers summarizing our results. We proudly inform you that the first paper about committee selection in DAG distributed ledgers is ready for submission. The second one in which we describe a robust random number beacon should shortly follow.

*Protocol*. This month we concluded all research for the protocol specifications and went over it to check if all questions were properly answered. The specification draft is close to completion too!

We also went to give a theoretical review of the specifications of Chrysalis regarding the modules that were developed by the Protocol Group. The discussions on Chrysalis will still go on for the next few weeks and after that, we should shift our work to review the Coordicide specifications.

*Specifications*. Besides GoShimmer, our department has also recently been making great progress on the technical specifications for all the components of the protocol. These specifications are the blueprints from which the engineering department will build the node software. Thus upon completing these specifications, research will transfer the Coordicide project to engineering for production.

Each author is close to completing a good draft of each specification, representing the end of the first phase of specification. Here are the next steps which will be completed over the next few months:

- Everyone will read each specification and look for errors, both technical and linguistic. We need to make sure that the documents coherently overlap and cover all aspects of the protocol.

- Next, we need to synchronize the language and the format across all the specifications. Parameters and variables often span several modules of the protocol. We need to make sure these names are all consistent.

Now that travel restrictions are easing across Europe, our researchers will be able to meet in person and discuss these next steps, expediting the process.


- Until our next monthly update, you can stay up to date with the IOTA Research team in the #tanglemath channel on our Discord. You are also welcome to follow and participate in our technical discussions on our public forum: IOTA.cafe.


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
