https://iota.cafe/t/parallel-reality-based-ledger-state-using-utxo/261

“Parallel reality” based ledger state (using UTXO) 

Coordicide


hans.moog

18 Oct '19

In this thread I want to introduce a new concept for keeping track of the ledger state in the tangle, that tries to avoid “walking the tangle” as much as possible. Especially with high amounts of TPS, every “walk in the tangle” becomes expensive relatively fast and the algorithms degrade in performance.

**Note: You can click on the headlines to expand the section!**

# Motivation

**The Status Quo**

The tangle is a datastructure, where every single transaction has a very unique perception of the ledger state (defined by its past cone). Accordingly, to accurately calculate a transactions “perception”, we have to sum up all the balance changes of all its directly or indirectly approved transactions since genesis.

Obviously it would be very inefficient, to do the same calculations over and over again. It makes much more sense to “cache” the result of these calculations (as all transactions at some point share the same history). This is why IRI accumulates all the changes between milestones and stores them in a differential ledger state that contains the aggregated balance changes since the last milestone. Since transactions that have been referenced by a milestone are considered to be confirmed, we can also create an additional confirmed ledger state that is essentially a sum of all the differential ledger states, which enables fast look ups of balances in the following way:

> Whenever we walk through the past cone of a transaction, we only have to collect the balance changes until we reach a transaction that has been referenced by a milestone. We can then add these collected balance changes to the confirmed ledger state to get the final balances.

Note: This is a very straight forward way of optimization and it works sufficiently good in the case of our coordinator issued milestones.

**The Problem**

This approach is however only viable because we

1 have to do these kind of ledger state calculations relatively seldom (only when a new milestone arrives or if we want to select tips to approve / issue a tx ourselves) and
1 because we can have this cut-off point for the walk in form of the confirmed ledger state.

For our voting based consensus, we instead

1 need to check the validity and the ledger state of every single transaction as soon as it arrives (to be able to vote) and
1 can not rely on having consensus on these kind of checkpoints that are required for this kind of optimization.

We could most probably devise an algorithm that would select sufficiently good checkpoints for this kind of caching even without a coordinator, but it would either require some form of rollback-mechanism for the ledger state that allows us to react to changing opinions or to only “aggregate” confirmed transactions which means that depending on the TPS and the time to finality, we might have to do relatively long “walks”.

Especially with high amounts of TPS, every “walk in the tangle” becomes expensive relatively fast and the algorithms degrade in performance. One famous example is the gtta-API-call which is currently considered to be one of the biggest bottlenecks for IOTA and the reason why we consider changing to a different URTS-based tip selection algorithm.

The fact, that we need to use this already “not-so-lightweight” approach for every single transaction, would make this a huge bottleneck for high throughput scenarios.

**The Solution - a different form of optimization**

Obviously, the described algorithms and mechanisms are the most exact representation of what happens in the tangle and pretty straight forward. Sadly however, the ways to optimize it are very limited as they are all essentially space-time trade-offs (we save walking time by creating caches).

I now want to propose a fundamentally different way of calculating the ledger state that will not only allow us to have very fast balance look ups but that will also include a way to detect and “manage” the states of conflicting subtangles.

**Fundamental questions - "Do we really need to walk?"**

**Let’s ask ourselves a very fundamental question**: Why do we need to walk through the past cone of a transaction, to tell if it is valid or not? We realize quite fast, that the answer to this question is pretty simple:

> We walk through the past cone to check if the funds that are supposed to be spend exist and have not been spend by another transaction in the same past cone already.

What we are essentially doing is a “binary search” in the tangle for the funds that are supposed to be spent. Considering, that most transaction only spend funds from a few input addresses but reference a very large amount of other transactions, this doesn’t seem to be a very good approach.

**So the next question is**: Can we not somehow get rid of this need to “search the tangle”? And the answer is, yes we can (see specification)!

# Specification

**1. Using a UTXO scheme**

Instead of using an account based ledger where we only keep track of the addresses and their balances, we instead keep track of “sub balances” on an address associated to the transaction hash that was responsible for creating these balances (UTXO).

When specifying the inputs of a transaction, we reference the address and the transaction hash which uniquely identifies the funds we want to spend (see picture):



UTXO%20Scheme%20(5)
472×761 33.1 KB


**2. Additional references as part of the past cone**

These additional “input references” (next to branch and trunk) will be considered to be part of the past cone of a transaction and a transaction is only solid, if

- all of the referenced inputs are solid and
- branch and trunk are solid.

This way, a solid transaction by definition contains the funds it wants to spend in its past cone no matter where in the tangle a transaction attaches (see picture):



UTXO%20Scheme%20(8)
442×761 27.8 KB


Since transactions directly reference funds that they want to spend, it is impossible to have transactions that try to spend funds out of thin air (because they would never become solid).

**3. Aggregated Ledger State (for non-conflicting transactions)**

Since most of the transactions in a “healthy” tangle are non-conflicting (or just data transaction), they will anyway converge into a globally shared state that nodes will agree on and we don’t even have to think about maintaining “separate” ledger states or perceptions for each of these honest transactions.

All solid transaction will therefore initially be “booked” into an aggregated ledger state, which will simply be a list of transaction outputs - the “master reality”.

**4. Detecting double spends**

Whenever a transaction consumes an output, we take note of the transaction hash that consumed the output by storing it in a list of consumers together with the output in the database (we mark it as spent). Whenever a transaction consumes an already spent output that was consumed by another transaction, then we have identified a double spend and need to handle it differently.

**5. Handling conflicts using parallel “realities” (versions of the ledger state)**

Every double spends introduces a unique perception of the ledger that will not automatically converge like the honest transactions discussed before. All transactions in the future cone of such a double spend are sharing this unique perception.

To be able to correctly reflect this, we create a copy of the ledger state for each of the double spends. Then we walk through the future cone of the double spends and “book” all the balance changes that approve this perception into this new version of the ledger. If the balance changes have previously been booked in another reality (i.e. the master-reality while the transaction was not conflicting), then we move the booked balances over to the corresponding reality that we just created.

Note: Instead of making an “actual” copy of the ledger state, we organize these realities in a hierarchical way where every reality has a parent reality from which it recursively inherits all of the balances. This is an optimization that allows us to create realities without having to copy all of the existing transfer outputs. A “reality” becomes extremely lightweight and is just an identifier, which is used to logically “group” the transaction outputs. Since transaction outputs are only stored once and then just get “booked” to this logical group, realities “cost” next to nothing.

**Let’s look at a short example**:

We have a conflict free tangle (with only the master-reality) and a double spend (TX2) arrives that is using the same inputs as an existing transaction (TX1).
1 We create two additional realities - one for TX1 and one for TX2.
1 We walk through the future cone of TX1 and move the balances from the master-reality to the reality of TX1.
1 We walk through the future cone of TX2 (most probably very small since it just arrived) and book its balance changes to the reality of TX2.

We now have 3 versions of the ledger that correctly reflect the different “opinions” that exist in the tangle:

- master-reality (which reflects the opinion that both double spends will be rejected)
- TX1-reality (which reflects the opinion that TX1 gets accepted and merged back with the main-reality)
- TX2-reality (which reflects the opinion that TX2 get accepted and merged back with the main-reality)

**6. Conflict sets**

If transactions are spending the same input, then their corresponding realities will form a conflict set (identified by the used input). If a transaction is spending multiple inputs, then its reality can be part of multiple conflict sets at the same time.

Note: We can either like exactly one or none of the realities of a conflict set.

**7. Recursive sub-realities**

If a reality contains additional double spends, then it will recursively form sub-realities in the same way as realities get formed from the master-reality by creating a new reality that is having his parent reality pointing towards the reality that contained the funds before the second spend arrived.

**8. Aggregated realities**

It is also possible for transactions to combine multiple realities (if they are not part of the same conflict sets) by attaching to transactions of these realities (branch / trunk / used inputs). This will create an “aggregated reality” that has multiple parent realities (namely the ones that got combined). This allows us to associate every transaction with exactly one reality.

To not have to walk through the future cone of the double spends whenever we receive a new transaction (to correctly associate newly received transactions to their corresponding reality), we store the reality that a transaction is associated to in the transaction metadata.

Newly attached transaction can now simply “inherit” the reality of their parents in the following way:

> We iterate over the referenced realities and remove all realities that “descend” from one another keeping only the “deepest” realities (that have the longest path to the main-reality).
> - If there is only one reality left, then we associate this reality with the new transaction.
> - If there is more than one reality left, then we combine them into an aggregated reality and assign the aggregated reality to the new transaction.
> The identifier of the aggregated reality is calculated by hashing a concatenation of the sorted list of reality ids it “contains”.

**Example**: A transaction referencing the main-reality and the TX1-reality will inherit the latter because the TX1-reality has the main-reality as its parent.

**9. Conflict resolution and cleaning up**

Once a conflict has been decided (i.e. by finalizing a decision after a voting process), we can remove the conflict set and all of its associated realities (prune the transactions from the database - they will be orphaned). The winning reality gets “promoted”, which means that we will copy all of its content into its parent reality and reconnect its sub-realities to now point at the underlying parent reality instead.

Additional decisions about the pending sub realities will be resolved in the same way by merging them back with their parent reality whenever a decision was made.

**Conclusion**:

This way of keeping track of the leder allows us to instantly decide if a transaction is valid without having to walk the tangle. We simply need to retrieve the referenced transaction outputs and check if they have a consumer already.

The more complicated conflict handling only kicks in if it is really necessary and instead of having to walk the tangle over and over again to determine the balances, we just have to do it once (when we create the realities). First simulations of this approach show that we can handle around half a million ledger operations per second.

At the same time, due to the use of UTXO, we no longer need to make sure that we correctly reference the funding transaction in the past cone of a spend, which will make the tip selection also independent of walks in the tangle.

Note: The worst case - where every single tip is always conflicting with all other tips - essentially “degrades” to the way we calculate the ledger state today (with every single transaction having its own reality which can then only be resolved by “walking” through the parent realities of this transaction).




Does coordicide increase TPS / Scaling?
3

Simplicial complexes and realities
1

created
Oct '19
last reply
Oct '19
2
replies
456
views
2
users
2
links

andreas.penzkofer
Oct '19

This looks interesting. How do you reference funds that are below the max depth? Maybe if you clip at milestones the UTXOs could merge into a new unique identifier? If so, this can overcome the million UTXO references in a tx problem - you just have to wait long enough.





hans.moog
Oct '19

Unspent funds are never “below” max depth - they just stay in the ledger state until they get spent. They are essentially the equivalent of the balances that we store today.

You can throw away the actual transaction when you have stored the transfer output. When checking the solidity you only check if the transfer output is known in your ledger state but you don’t need the actual transaction anymore.

You can of course have the issue that somebody “spams” the database with unspent transfer outputs by making a lot of small transactions to an address, but the same thing can be done today by sending a lot of small funds to separate addresses.

In the case of creating a lot of “sub-balances” you can think of ways to clean up these kind of sub-balances using additional mechanisms. One could for example allow people to “sweep” multiple funds from an address to the same address without having to sign it and therefore allow others to proactively “clean up” addresses that got spammed (maybe claiming the mana in the process of doing so).

This would incentivize everybody to sweep the funds themselves as soon as you receive them.



