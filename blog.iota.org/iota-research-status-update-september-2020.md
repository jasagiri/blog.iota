https://blog.iota.org/iota-research-status-update-september-2020-72720fa1c032

# IOTA Research Status Update — September 2020
Serguei Popov
Serguei Popov
Follow
Sep 11 · 5 min read
Image for post
Image for post

With the easing of travel restrictions in Europe, our department was able to have its first summit since February. The primary purpose of this meeting was to review all the specifications which each group had been working on over the last few weeks. With our theoretical Coordicide research nearing its end, our research is moving into a new phase, where we are focused on the following tasks:

- Tying up the last few loose ends in the specifications and completing specifications documents
- Implementing the specifications into the next version of our testnet, Nectar
- Sharding research

With our research moving into this phase, we decided to reorganize our group structure to better service our current priorities. Here are our new groups:

1. *Nectar Testnet Implementation*: This group is focusing on implementing the specifications into code.
2. *Nectar Testnet Study Group*: The point of building a prototype is to evaluate the performance of the protocol on a testnet. This group is doing that evaluation. In particular, they are:

  - Collecting and analyzing data collected on Pollen Testnet
  - Verifying previous theoretical claims about the protocol
  - Finding optimal values for each parameter

3. *Protocol*: This group will study issues arising in the protocol as they are implemented in Pollen. They will also finish the specifications.

4. *Networking*: This group will carry on studying and optimizing aspects of the protocol related to rate and congestion control and gossiping.

5. *Sharding*: This group will focus on research around sharding.

*Pollen Testnet Implementation*. This month the GoShimmer team released the Pollen Testnet v0.2.4 that fixes a synchronization issue occurring when missing messages were not requested more than once. This release also fixes the node’s dashboard explorer crashing or not properly visualizing the payload of a given message, and improves the Grafana local dashboard by adding support for the sync-beacon payload type as well as displaying uptime and nodeID. We have also worked on improving the overall code quality by fixing all the linter related issues.

The team is currently working with the GoShimmer X-Team, a group of selected community members, to start testing the distributed random number generator (dRNG). This feature will be part of the upcoming v0.3.0 release.

*Mana in Pollen*. The next Coordicide module that will be progressively integrated into Pollen is mana. This month we have worked on turning the mana research specification into a more detailed document that we are currently using to implement mana in Pollen. The document outlines our proposal for mana implementation, including mana calculation and inclusion in the transaction layout. We also cover the mana module functionality and propose related tools, including APIs, visualizations, and analytics.

*Specifications*. As discussed in the introduction, the department recently met to review the specifications. This was an excellent chance to take a holistic view of the protocol. We found no problems, tied up the remaining few core theoretical research questions, and we are proud to report that we are very happy with our work so far. That said, we did identify a few gaps in the specifications which still need to be filled in. In particular, these last few loose ends include:

- Synchronization: When a new node comes online, it downloads the recent messages and transactions from its neighbors. However, it cannot verify the outcomes of FPC voting on these transactions. To deduce the outcome of votes, a node can track the mana held by nodes issuing messages in the future cone. We are now working on the specification to do exactly this.
- Parallel reality-based ledger state: Pollen uses parallel reality-based ledger state, which we are formalizing the specifications for now.
- Message creation: Although this is implied by several other specifications, we are working to document this thoroughly.

Some of the specifications documents still require more details and others some editing, so work continues to finish all specifications documents in a prudent manner. As the specifications are implemented into Pollen, we may discover that certain adjustments are required. Thus, the specifications will continue to evolve alongside Pollen.

*Nectar Testnet Study Group*. As one of the new groups, most of the meetings have been devoted to planning our future work. There are many aspects of the prototype to study, which the group is working to prioritize. We began by listing metrics that each Nectar Testnet module needs to measure and what data it needs to store. We will forward this to the Nectar Testnet Implementation team, so it can be incorporated into future releases. We also spent some time learning how to use Pollen nodes, and how the current data collection works.

*Protocol*. Following the research summit, the protocol group made an extensive plan, covering what still needs to be done for IOTA 2.0 as well as how to go from the current specification drafts to a final version.

The specification drafts went through review, to check what is still missing and assess the current state of everything and assign owners for each file. We are happy to report this work is nearly done. The teams will return to work on the specs, and have the drafts become a proper version in a few weeks.

Recent communication with the GoShimmer group led to our group’s prioritization of research on confirmation confidence, finalization and how these impact mana calculation. We came to a theoretical agreement over those issues by utilizing an approach aligned with our current approach in the Pollen Testnet. We are also currently working on node bootstrapping, or the method by which nodes join the network, specifically dealing with methods to obtain the necessary information in a secure way. Everything is progressing well and we hope to have all IOTA 2.0 research “loose ends” completed in a few weeks.

*Networking*. The current main goal of the networking group is to analyze the consistency criterion under the presence of malicious actors. The task is non-trivial, as it should include: (i) a way to detect malicious behavior; (ii) the action of blacklisting the related issuing nodes; (iii) an effective packet drop strategy which optimizes latency; and (iv) a lightweight procedure for unsolid transactions. We are currently simulating the first proposal to address these points.

We are glad to communicate that the paper “Preventing Denial of Service Attacks in IoT Networks through Verifiable Delay Functions” has been accepted for publication at IEEE GLOBECOM 2020, a top tier networking conference.

Until the next update, if you have any questions or would just like to say hi, you can find our Research team members in the #tanglemath channel on our Discord. You are also welcome to follow and participate in our technical discussions on our public forum: IOTA.cafe.
