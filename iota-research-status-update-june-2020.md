https://blog.iota.org/iota-research-status-update-june-2020-f0fbf9df0a4b

IOTA Research Status Update June 2020

Serguei Popov
Follow
Jun 18 · 5 min read


We have a few exciting status updates to share with everyone this month: First, the new GoShimmer release v0.2.0 is planned for the end of June. We consider this release to be a significant milestone, as it will support value transactions and conflict resolution via FPC for the first time. It will also include updates such as a different transaction layout, UTXO, support for “parallel-reality” ledger states, binary (encoding, cryptographic signatures and hash functions), new APIs and more. GoShimmer is designed with modularity at its core, which has greatly simplified the process of enriching it with these additional features and modules.

Next, we’re happy to report that we have published a paper on integrating FPC and mana, to be presented at FTC2020. We’ve also submitted two networking papers, and our dRNG paper is being polished for submission.

Finally, we are pleased to report that the positive feedback loop between Research and Engineering has been strengthened, with input from each team helping in an iterative refinement process of the specifications. Most of the specifications have been improved as a result of this interaction, and we are excited to see the progress of the specifications across the board to a very good stage. Specific updates from each of our groups follow below.

・・・

**GoShimmer Implementation**. The team has finished implementing and testing the parallel-reality based ledger state that will be part of the next GoShimmer release in its branch-based form. We believe that this new concept for managing the ledger state will be a very good fit for our decentralized network and will be one of the main subjects to assess after the new release. The analysis server has been enriched with a brand new section showing the overall network consensus, specifically a real-time update on the FPC outcome on each conflict. These results will also be stored on a database so that, together with our community, we will gather enough experimental data to compare with our previous results obtained by means of simulations. Moreover, the autopeering section has been improved on both the frontend and backend side.

This month we have also been working on the new APIs for issuing value transactions and retrieving the balance of a given address. These APIs will be the core of a very simple wallet we are currently working on.

As everything is now based on binary, we have developed a new configurable Proof of Work (PoW) library that will, in future and iterative releases, shift towards our adaptive PoW.

Finally, a large amount of our time has been spent on developing and improving both unit and integration tests. Although this task can be (and it has been!) tedious, it has helped us tremendously to be sure not only that the code works as we expect, but also to improve some bits and pieces and to learn more about the code written by other team members.

**FPC**. We have just published a conference paper on how mana is implemented in FPC; the paper will be presented at FTC2020. Moreover, we finished a short research note that investigates effects that may arise from weighted voting such as loss of anonymity, centralization, and scalability while discussing their relevance to protocol design and implementation.

**Networking**. Two manuscripts have been submitted and are currently under review for a top-level international conference: (i) “On Congestion Control for Distributed Ledgers in Adversarial IoT Networks” presents our current proposal to deal with network congestion, and shows the results of our simulations; (ii) “Preventing Denial of Service Attacks in IoT Networks through Verifiable Delay Functions” describes how verifiable delay functions can be used to replace PoW as a rate-limiting mechanism, and shows an actual implementation on Raspberry Pi and standard laptops.

Additionally, we are working on the theoretical validation of our congestion control algorithm by analyzing the buffer dynamics through queueing theory models, and we are generalizing our proposal for transactions of different sizes and types. As for verifiable delay functions, we are actively studying multi-exponentiation techniques to speed up computation and verification time, especially in low-power devices.

**dRNG**. With the specification of dRNG module ready, we are currently focused on writing articles for peer-reviewed academic journals. We hope that publishing our results will help us improve our ideas and promote them. We decided that we are going to prepare two articles. The first one focuses on the committee selection and random number publication in the Tangle. The second one is devoted to improvements to security and liveness.

**Mana and Autopeering**. We now have good drafts of the mana and autopeering specifications, which is an exciting step. After the engineering department reviews them, we will make some final revisions and then the specifications will be finished. The engineering team will then be able to implement these solutions.

We also refined some ideas about mana, and we decided to add a feature that will enable nodes to “refresh” their mana, even if it was connected to funds held in cold storage. This will increase the utility of mana, and also help secure the system.

As the specifications near completion, the first phase of this group’s project is really winding down. We hope to start to shift our focus to writing up our results and also researching the best parameters. This work, although important, is not as pressing as the specifications since it is not blocking engineering’s ability to begin coding.

**Protocol**. This month the team finalized the research on orphanage and finality. We also revisited the recent research on solidity to see how it would interact with voting and other checks that depend on the past, hence we decided that solidification on the Value Tangle should not be enforced, but required to be eligible for tip selection and voting.

With the research on the protocol nearly concluded, the specs are being written and advancing smoothly. They will be concluded in the coming days and will be passed off to the engineering team for their feedback.

We look forward to the coming GoShimmer release, and we hope that you are able to participate in the early community testing. Until our next monthly update, you can stay up to date with the IOTA Research team in the #tanglemath channel on our Discord. You are also welcome to follow and participate in our technical discussions on our public forum: IOTA.cafe.


Research And Development
Iota
Coordicide
Goshimmer
Techupdates

1.7K claps






Written by
Serguei Popov
Follow
mathematician


IOTA
Follow
Official IOTA Foundation blog