https://blog.iota.org/dev-status-update-september-2020-2869dd1e0420

# Dev Status Update — September, 2020
Jakub Cech
Jakub Cech
Follow
Sep 18 · 5 min read
Image for post
Image for post

Published by the IOTA dev team every month, this update will provide you with news and updates about our key projects! Please click here if you want to see the last status update.

The research department is also releasing a monthly update that you might want to see.

## IOTA 1.5

IOTA 1.5 (also known as Chrysalis) is the mainnet’s intermediate stage before Coordicide is complete. You can read more about the strategy for releasing Chrysalis here.

The Chrysalis phase 1 components were deployed to mainnet last month. The engineering team is now working on Chrysalis phase 2.

## Pollen

Further improvements of the Pollen network are well underway. Specifically, *the latest version of the GoShimmer node software, v0.2.4, brings the integration of the dRNG module*, improved tooling and debugging capabilities, and more. You can read up on the update here.

You can read more about Pollen, Nectar, and Honey, concepts we introduced to talk about the milestones on the path to Coordicide in this post.

You can follow the project on its GitHub repository. If you want to get involved, check out our updated contributing guidelines.

## Bee

The Bee team is working on finishing up some of the final pieces of the Bee node software, such as the storage layer and local snapshots. The work on auto peering will soon start. The team is also switching the implementation to the Tokio runtime for better performance and compatibility with the Rust ecosystem. Once the last efforts are finished, we will be releasing an alpha version of the Bee software.

Work is also beginning on implementing Chrysalis phase 2 components.

The team has also been doing regular live stream coding sessions every Friday at 5PM CEST. You can find the full playlist here. One of the future sessions will be devoted to releasing the first alpha version of the node software.

You can find all Bee RFCs in their respective GitHub repository.

## Hornet

The team has released a breaking 0.5.0 version containing Chrysalis phase 1 changes in August. Since then, the team has been working on fixes and improvements for the node software. Lastly, the team released a 0.5.3 version of Hornet this week.

Initial implementations of some of the Chrysalis phase 2 changes are already in progress. The current goal is to achieve a state in the node software where Chrysalis Phase 2 changes can be tested out in a dedicated test network.

## IRI

As noted in this blog post, IRI 1.8.6 was the last release of IRI. The software has been discontinued with the upgrade to Chrysalis phase 1 and you are encouraged to run Hornet nodes instead.

## Smart contracts

The Smart contracts team is now mainly focusing on finishing up the prototype release of Wasp node and PoC hard coded smart contracts demo that is slated for end of September.

Stay tuned for more information in the upcoming weeks!

## Stronghold

The Continuous Integration workflow at the public github repository is being finalized. This means that the rust crates will be automatically published to https://crates.io — and ‘internal products’ (like the CLI) will be built for the major desktop platforms and published as releases. This is expected to be finalized in week 39 of 2020.

The high-level library for integration with the IOTA Protocol has been built and some of the late protocol changes are on deck for enhancement once they are available in iota.rs. A refactoring of the low-level ‘engine’ is being undertaken to further isolate activities within ‘sub-actors’ to prevent secret leakage. Furthermore, an internal review is underway to identify opportunities to not only zero out memory, but also to limit other simultaneous operations.

On the research fronts, initial work is beginning for the p2p communication system between strongholds (using libp2p-noise). Finally, together with some members of the community, initial tests are being done to identify opportunities for using an adapted Stronghold CLI in concert with a browser extension.

## Wallet

The wallet library (wallet.rs) was recently open-sourced. You can now track its progress here. The library is for the most part complete, with some finer details of Stronghold integration, some Chrysalis adjustments, and later testing against a Chrysalis testnet, still to do.

Meanwhile, the wallet front end team has begun implementing the wallet’s user interface. We are currently investigating a new plugin system and an extensible component library. With such a system, developers would be able to build a UI from the component library using json. The plugin system would make third party contributions more straightforward and more easily auditable, as well as generally improving the security of the app (by limiting control over what is allowed and separating contexts).

## IOTA Identity

The Identity team has been set up last month consisting out of community members huhn#8105, Thoralf#3558, and Tensor#2912 collaborating through an EDF fund. They work in close collaboration with a few IOTA Foundation developers. In the short time span, the identity.rs repository has seen a lot of progress, implementing many of the requirements of the DID and Verifiable Credential proposed standards from W3C.

Currently, the team is also exploring the integration and collaboration with Stronghold to deliver IOTA Identity with a default, strong security model, protecting your digital identities. The team is on track for an IOTA Identity 1.0 release before the end of the year. This release will enable decentralized identity applications in production, but might miss some ease of use and tooling for the developers. These will be developed over the next year.

## IOTA Streams

The Streams team has been working on changes to the implementation that allows for functionality like multi-publisher support, as well as changing the existing processes into a binary form to improve performance on existing hardware.

All the changes will be part of a pre-release coming this Friday! Stay tuned on our Discord and Twitter for more information on the release.

## IOTA Experience Team

The community involvement in the IOTA Experience Teams is steadily growing.

Luca#3952, joined the GoShimmer and Permanode Experience Teams and set up a 0.2.1 Chronicle permanode and provided useful examples for the community.

The IOTA Access Experience Team had a session with Bernardo Araujo during which it was possible to preview the source code of IOTA Access SDK.

Two other IOTA community members joined the IOTA GoShimmer Experience Team: MaKla#4289 and Maik Piel#8401, this X-Team is involved in testing the drand software integration with GoShimmer and has set up a seven member dRNG committee to support Angelo Capossele in the research to reach the 0.3.0 milestone for Pollen.

daverl#0001 (a.k.a. Dave [EF] and svenger87#8523 installed the alpha version of Bee and contributed to the Bee X-Team initiative with valuable feedback.

To get started, discover the IOTA Experience Team on GitHub, explore the IOTA Experience Initiatives and then apply through this form.

## Roadmap updates

We have made the following updates to our roadmap:

- The next IOTA Streams release has been moved to September.
- The Permanode release with solidification support has been moved to September.

As always, we welcome everyone to stop by on Discord — every project mentioned here has a channel (or more) for discussion with the devs!

Follow us on Twitter to keep track of all the latest news: https://twitter.com/iotatoken

    Iota
    Dlt
    Research And Development
    Software Development
    Techupdates

Jakub Cech

Written by
Jakub Cech
Follow
Director of Engineering @IOTA Foundation
IOTA
IOTA
Follow
Official IOTA Foundation blog