
consensus protocol

* Proof-of-World (PoW) based consensus
 * scaled to thousands of completely untrusted participants (node)
 * drawbacks - high latencies, low transaction rate (about 7 txns/sec vs
   MasterCard or VISA's 10,000 txns/sec), significant energy expenditure
 * (permissionless) Bitcoin, NameCoin, LiteCoin, DogeCoin, Monero
 * Ethereum Homestead's EthHash - memory hardness, GHOST (includes the headers
   of the recently orphaned blocks known as uncles)
* Paxos, RAFT, various Byzantine Fault Tolerance algorithms
 * (permissioned)
 * do not scale well beyond about twenty peering nodes and cannot have any
   open-ended participation
 * Tolerating Byzantine faults (needs "3f+1" replicas) increase the complexity
   of the consensus protocol by adding several extra layers of messaging into
   the system.
 * Practical Byzantine Fault Tolerance (PBFT) uses the concept of primary and
   secondary replicas, where the secondary replicas automatically check the
   sanity and liveness of decisions taken by the primary and can collectively
   switch to a new primary if the primary is found to be compromised.
* Proof-of-Stake (PoS)
 * Ethereum Serenity
 * The PoS algorithm pseudo-randomly selects validators for block creation.
   Naïve PoS algorithms suffer from a problem called Noting-at-Stake.
 * PoS was first designed and a naïve version of it used by PeerCoin. Different
   variations of PoS are also used by BitShares, NXT and Tendermint.
 * Casper uses the concept of security deposits and bets to achieve consensus.
   Nodes are allowed to be bonded with the Ethereum system by making significant
   security deposits set by the protocol. These nodes are bonded validators and
   show commitment and interest in advancing the Ethereum blockchain via staking
   their security deposits. The initial list of bonded validators is tracked by
   a special contract known as the Casper contract. From there on, the bonded
   validator list can evolve based on newer nodes joining in and older ones
   leaving the system. Each validator is pseudo-randomly selected to produce a
   block from the active validator set, with the probability of selection
   lineraly weighted by each validator's deposit. If a validator produces a
   block that gets included in the chain, they receive a block reward equal to
   the total ether in the active validator set. If the validator produces a
   block that does not get included in the chain, the protocol works such that
   validator loses the security deposit equal to the block reward.
* Proof-of-elapsed-Time (PoeT)
 * IntelLedger or Intel SawtoothLake, under Linux Foundation's HyperLedger
   project as a proposal for further development
 * intended to run in a Trusted Execution Environment (TEE), such as Intel's
   Software Guard Extensions (SGX)
 * PoET uses a random leader election model or a lottery based election model
   based on SGX, where the protocol randomly selects the next leader to finalize
   the block. The random leader election algorithm uses this model to deal with
   untrusted nodes and open-ended participation of nodes in the consensus
   algorithm. Each validator requests a wait time from the code running inside
   the TEE. The validator with the shortest wait time wins the lottery and can
   become the leader. When a validating node claims to be a leader and mines a
   block, it can also produce proof generated within the TEE that other nodes
   can easily verify. It has to prove that it had the shortest wait time and it
   waited for a protocol designated amount of time before it is allowed to start
   mining the next block.
* Byzantine Fault Tolerance and variants
 * HyperLedger Fabric
 * PBFT - It uses the concept of replicated state machine and voting by replicas
   for state changes. It also provides several important optimizations, such as
   signing and encryption of messages exchanged between replicas and clients,
   reducing the size and number of messages exchanged. This approach imposes
   a low (3%) overhead on the performance of the replicated service. PBFT
   however has only been scaled and studied to 20 replicas. It's messaging
   overhead increases significantly as the number of replicas increase.
 * SIEVE - SIEVE consensus protocol is designed to handle non-determinism in
   chaincode execution. SIEVE handles transactions that are usually
   deterministic, but which may occasionally yield different outputs. It
   initially executes all operations speculatively and then compares the outputs
   across replicas. If the protocol detects a minor divergence among a small
   number of replicas, the diverging values are sieved out. If the divergence
   occurs across several processes, then the offending operation itself is
   sieved out.
 * Cross-Fault Tolerance (XFT) - The XFT protocol is a new protocol that
   simplified the attack model (relaxes the assuption of the BFT's powerful
   adversary) and make BFT tolerance feasible and efficient for practical
   scenarios. XFT assumes that the adversary cannot control majority of the
   nodes and generate network partitions at will at the same time. XFT is
   particularly interesting to blockchain based systems.
* Federated Byzantine Agreement
 * use variations of the BFT consensus models by making them open-ended with
   respect to node participation. End users generate payment transactions using
   client software and must trust some gateways to hold their payments. Gateways
   are like banks that people use in the real world to hold their money.
   Gateways hold user funds issued to the gateway in flat currencies and create
   equivalent issuances in the Ripple/Stellar network, which reflect as an
   account balance in the global blockchain.
 * Ripple - Ripple protocol requires each node to define a Unique Node List
   (UNL). The UNL comprises of other Ripple nodes that are trusted by the given
   node not to collude against it. Each UNL has to have a 40% overlap with other
   nodes in the Ripple network. Consensus happens in multiple rounds where each
   node collects transactions in a data structure called "candidate set" and
   broadcasts its candidate sets to other nodes in its UNL. Nodes validate the
   transactions, vote on them and broadcast the votes. Based on the accumulated
   votes, each node refines its candidate set and transactions receiving the
   largest number of votes in the UNL, the candidate set becomes a valid block
   or in Ripple terms a "ledger". This ledger is finalized and considered the
   "Last Closed Ledger (LCL)" and added to the Ripple blockchain by each node.
   Consensus in the entire network is reached when each individual sub-network
   reaches consensus.
 * Stellar - Stellar Consensus protocol algorithm uses the concept of quorums
   and quorum slices. A quorum slice is a subset of a quorum that can convince
   one particular node about agreement. An individual node can appear on
   multiple quorum slices. Stellar introduces quorum slices to allow each
   individual node to choose a set of nodes within its slice thereby allowing
   open participation. These quorum slices and quorums are based on real life
   business relationships between various entities thereby leveraging trust that
   already exists in business models. Each node first performs initial voting on
   transactions, also generically considered as statements. It can accept a
   different statement if its quorum slice has accepted a different one. Second
   step is the acceptance step. A node accept a statement if it has never
   accepted a statement contradicting the current statement and each node in its
   v-blocking set has accepted that statement. A v-blocking set is a set of
   nodes one each from a quorum slice to which the current node belong to. This
   step is known as ratification when all members of a quorum agree on a
   statement. Confirmation is the final step of the voting process and signifies
   system level agreement.

Sybil attacks on a blockchain network can allow a single user to generate
 several online identities to influence and manipulate the consensus
 process.<br>
selfish mining, where the normally honest miners are incentivized to support the
 attacker and join in carrying otu a 51% attack

rigorous real-world application requirements - low latencies, immediate
 transaction finality, high performance, good scalability

state machine replication

Consensus algorithms have to resilient to failures of nodes, partitioning of
 the network, message delays, messages reaching out-of-order and corrupted
 messages. They also have to deal with selfish and deliberately malicious
 nodes.<br>
Each algorithm makes the required set of assumptions in terms of synchrony,
 message broadcasts, failures, malicious nodes, performance and security of the
 messages exchanged.<br>
A consensus protocol has three key properties: safety (consistency of the shared
 state), liveness, and fault tolerance. (see also the FLP Impossibility
 Result)<br>
fail-stop faults and Byzantine faults<br>
blockchain type, transaction finality, transaction rate, token needed?, cost of
 participation, scalability of peer network, trust model, adversary tolerance

Hyperledger Fabric, Tendermint, Symbiont, R3 Corda, Iroha, Kadena, Chain,
 Quorum, MultiChain, (not directly following the BFT approach) Sawtooth Lake,
 Ripple, Stellar, IOTA Tangle<br>
As an example for the principle of scientific study, some serious flaws in a BFT
 consensus protocol called Tangaroa (also known as BFT-Raft) are shown.

As mentioned earlier, the form of consensus relevant for blockchain is
 technically known as *atomic broadcast*. It is formally obtained as an
 extension of a *reliable broadcast* among the node, which also provides a
 global or *total order* on the messages delivered to all correct nodes.<br>
The most important and most prominent way to implement atomic broadcast (i.e.,
 consensus) in distributed systems prone to t < n/2 node crashes is the family
 of protocols known today as Paxos and Viewstamped Replication (VSR). Discovered
 independently, their core mechanisms exploit the same ideas. The *Zab* protocol
 inside *ZooKeeper* is a prominent member of the protocol family. A more recent
 addition to the family is *Raft*, a specialized variant developed with the aim
 of simplifying the understanding and the implementation of Paxos. All protocols
 in this family progress in a sequence of *views* or "epochs," with a unique
 leader for each view that is responsible for progress. If the leader fails, or
 more precisely, if the other nodes suspect that the leader has failed, they can
 replace the current leader by moving to the next view with a fresh leader. This
 *view change* protocol must ensure agreement, such that message already
 delivered by a node in the abandoned view is retained and delivered by all
 correct nodes in this or another future view.<br>
More recently, consensus protocols for tolerating *Byzantine* nodes have been
 developed, where nodes may be *subverted* by an adversary and act maliciously
 against the common goal of reaching agreement. In the eventual-synchrony model
 considered here, the most prominent protocol is *PBFT*. It can be understood as
 an extension of the Paxos/VSR family and also uses a progression of views and a
 unique leader within every view. Actual systems that implement PBFT or one of
 its variants are much harder to find than systems implementing Paxos/VSR. In
 fact, [*BFT-SMaRt*](https://github.com/bft-smart/library) is the only known
 project that was developed before the interest in permissioned blockchains
 surged around 2015. There is widespread afreement today that BFT-SMaRt is the
 most advanced and most widely tested implementation of a BFT consensus protocol
 available. Experiments have demonstrated that it can reach a throughput of
 about 80'000 txns/sec in a LAN and very low latency overhead in a WAN.<br>
Like Paxos/VSR, Byzantine consensus implemented by PBFT and BFT-SMaRt expects an
 eventually synchronous network to make progress. Without this assumption, only
 *randomized* protocols for Byzantine consensus are possible, such as the
 practical variations relying on distributed cryptography as prototyped by
 SINTRA or, much more recently, HoneyBadger.

This communication primitive is known in the literature as *Byzantine consistent
 broadcast (BCB)*. BCB ensures *consistency* in the sense that *if* some two
 correct nodes deliver any payload, then they deliver the *same* payload. ... It
 is well-known how to prevent this: PBFT uses *Byzantine reliable broadcast
 (BRB)* in the place of the BCB. This primitive entails a second all-to-all
 message exchange, formally ensures the agreement property, and, most
 importantly, makes it possible for a subsequent leader to gather enough
 information so as not to violate the consensus protocol's guarantees.<br>
It would be readily possible to extend such protocols to more complex fault
 assumptions, as formulated by *generic Byzantine quorum systems*.

The Sumeragi consensus library of Iroha is "heavily inspired" by BChain a
 chain-style Byzantine replication protocol that propagates transactions among
 the nodes with a "chain" topology. Chain replication arranges the n nodes
 linearly and each node normally only receives messages from its predecessor and
 sends messages to its successor. Although there is a leader at the head of the
 chain, like in many other protocols, the leader does not become a bottleneck
 since it usually communicates only with the head and the tail of the chain, but
 not with all n nodes. This balances the load among the nodes and lets
 chain-replication protocols achieve the best possible throughput, at the cost
 of higher normal-case latency and slightly increased time for reconfiguration
 after faults. In Sumeragi, the order of the nodes is determined based on a
 reputation system, which takes the "age" of a node and its past performance
 into account. As becomes apparant from
 [the online documentation](https://github.com/hyperledger/iroha/wiki/Sumeragi),
 though, the protocol departs from the "chain" pattern, because the leader
 "broadcasts" to all nodes and so does the node at the tail.

The Federated Consensus protocol of Chain Core is executed by the n nodes that
 make up the network. One of the nodes is statically configured as "block
 generator". It periodically submits the block for approval to "block signers".
 Each singer endorses only one block at each height. Once a node receives q
 such endorsements for a block, the node appends the block to its chain. The
 protocol is resilient to a number of malicious (Byzantine-faulty) signers but
 not to a malicious block generator.

The QuorumChain protocol uses a smart contract to validate blocks. The trust
 model specifies a set of n "voter" nodes and some number of "block-maker"
 nodes, whose identities are known to all nodes. A block-maker waits for a
 randomly chosen time and then creates, signs, and propagates a new block that
 extends its own chain. A voter will validate the block (by executing its
 transactions and checking its consistency), "vote" on it, and propagate this.
 Each node accepts and extends its own chain with the block that obtains more
 votes than a given threshold, and if there are multiple ones, the one with
 most votes. There is one block-maker node by default. It is obvious that
 already one malicious block-maker node can easily create inconsistencies
 (chain forks) unless the network is perfect and already provides consensus.
 With m > 1 block-maker nodes, safety is not guaranteed and forks may occur due
 to network effects, even when all block-makers are correct.

(MultiChain) Instead, any permitted node may generate new blocks after waiting
 for a random timeout. More precisely, if the permitted list has length L, then
 a block proposal from a node is only accepted if the blockchain held by the
 validating node does not already contain a block generated by the same node
 among the ρL most recent blocks. Futhermore, a well-behaved node will not
 generate a new block if its own chain already contains a block of his within
 the last ρL blocks.

In constrast to PBFT and other protocols discussed there, the Swirlds hashgraph
 algorithm operates in a "completely asynchronous" model. The white paper states
 arguments for the safety and liveness of the protocol and explains that
 hashgraph consensus is randomized to circumvent the FLP impossibility. Since
 the algorithm is guaranteed to reach agreement on a binary decision only with
 exponentially small probability in n, it appears similar to Ben-Or-style
 randomized agreement.

Proof of Elasped Time (PoET), originally contributed by Intel, which is based on
 **the insight that proof-of-work essentially imposes a mandatory but random
 waiting time for leader election**. In particular, Nakamoto consensus lets all
 nodes participate in a probabilistic experiment, where each node is delayed for
 a random duration. Once the timer expires, the node can prove to all others in
 a verifiable way that it has executed the "waiting step" correctly for
 extending the blockchain. The SGX platform (available in many modern Intel
 CPUs) creates an attestation that can be used by any node to verify that the
 leader correctly waited for the proper random time. As the protocol's security
 depends on the hardware module potentially running on an adversarial host, the
 impact of attacks will have to be understood as well. In a permissioned
 setting, with known nodes, traditional BFT consensus protocols have several
 advantages compared to PoET: they are more efficient, do not rely on a single
 vendor's hardware, and create final decisions. Moreover, if trusted modules are
 available, then BFT consensus can increase the resilience to f < n/2 subverted
 nodes and achieve more than 70'000 tps throughput in a LAN.

The Ripple protocol consensus algorithm (RPCA) and its offspring Stellar
 consensus protocol (SCP) depart from the traditional security assumption for
 consensus protocols (i.e., some f < n/3 faulty nodes) by making their trust
 assuptions flexible. This means that each node would declare on its own which
 nodes it trusts, instead of accepting a global assumption on which node
 collusions the protocol tolerates. Each node designates a list of other nodes
 sufficient to convince itself (throught the unique node list in Ripple or the
 quorum slice of Stellar).<br>
In Ripple, the process of advancing the common distributed ledger is controlled
 by so-called validating nodes. They periodically start to create a new ledger
 entry and iteratively vote in rounds on its content. Furthermore, it is obvious
 that a minimal overlap among the convincing-sets (i.e., unique node lists) of
 all pairs of validating nodes is required, since otherwise they could exhibit
 split-brain behavior and the ledger would fork. Currently, Ripple "provides a
 default and recommended list of validators operated by Ripple and third
 parties," through a static configuration file; by default there are five
 validators operated by Ripple which trust each other and no other node. It
 appears that this list is adopted by most validating nodes in the system;
 consequently, trust is by far not as decentralized as advertised. A typical
 consensus process creating one new ledger entry completes in less than four
 seconds on average. Ripple has stated a throughput of about 1000 tps on a test
 network.<br>
As Stellar evolved from Ripple, it uses similar ideas and a protocol called
 federated Byzantine agreement within the Stellar consensus protocol (SCP). Only
 validator nodes participate in the protocol for reaching consensus. A node
 accept a "vote" or a transaction for the ledger when a threshold of nodes in
 its convincing-set confirm it. Examples in the documentation and the white
 paper suggest the use of hierarchical structures with different groups
 organized into multiple levels, where a different threshold may exist for each
 group. Similar structures have been known as Byzantine quorum systems (BQS) and
 are well-understood. They can readily be used to build consensus protocols for
 BFT systems. Furthermore, it seems that for constructing one single ledger, the
 convincing-sets for all useful configurations of SCP should intersect at the
 top of the suggested hierarchies. This appears to introduce some amount of
 centralization, similar to BQS.

(IOTA's Hash-DAG, tangle) This creates the DAG, with an edge pointing from each
 confirmed transaction to the new one. A weight is assigned to the transaction
 proportionally to the difficulty of the puzzle that the node has solved for
 producing it. The node is supposed to choose the k transactions to confirm
 randomly, from all transactions it is aware of, and to verify the two
 transactions plus all transitive predecessor transactions of them. The
 construction of the DAG is reminiscent of Lewenberg et al.'s inclusive
 blockchain protocols, but the details differ. The white paper and documentation
 claim that the tangle hash-DAG ensures a similar level of consistency as other
 permissionless blockchain systems.

Bitcoin Gold uses an alternative
 [proof-of-work algorithm called Equihash](https://www.cryptolux.org/images/b/b9/Equihash.pdf)
 that supporters believe is impervious to being sped up with custom hardware.
 Equihash has [also been adopted](https://z.cash/blog/why-equihash.html) by a
 Bitcoin rival called Zcash for the same reason. Equihash is based on a computer
 science and cryptography concept called the Generalized Birthday Problem.
1. Equihash starts with a list of pseudorandom bit strings derived from the
   block the miner wants to add to the blockchain.
1. The miner tries to find a subset of n strings (out of the ones generated in
   step 1) that XOR to zero.
1. The bit strings chosen in step 2 are concatenated together and hashed with
   the goal (as in the original Bitcoin) of finding a value below
   some pre-defined value.

In one example presented in the Equihash paper, solving a version of the problem
 with 700 megabytes took about 15 seconds, while solving the same problem with
 250 megabytes took 1,000 times as long.

## Casper

from Casper the Friendly Finality Gadget

Casper is a partial consensus mechanism combining proof of stake algorithm
 research and Byzantine fault tolerant consensus theory.<br>
There are two major schools of thought in PoS design. The first, *chain-based
 proof of stake*, mimics proof of work mechanics and features a chain of blocks
 and simulates mining by pseudorandomly assigning the right to create new blocks
 to stakeholders (Peercoin, Blackcoin, Iddo Bentov's work). The other school,
 *Byzantine fault tolerant* (BFT) based proof of stake, is based on a
 thirty-year-old body of research into BFT consensus algorithms such as PBFT
 (Tendermint).<br>
Casper the Friendly Finality Gadget is an overlay atop a *proposal
 mechanism*---a mechanism which proposes blocks. Casper provides safety, but
 liveness depends on the chosen proposal mechanism. That is, if attackers wholly
 control the proposal mechanism, Casper protects against finalizing two
 conflicting checkpoints, but the attackers could prevent Casper from finalizing
 any future checkpoints.<br>
new features - Accountability, Dynamic validators, Defenses, Modular overlay<br>
Rather than deal with the full block tree, for efficiency purposes Casper only
 considers the subtree of *checkpoints* forming the *checkpoint tree*.<br>
Each validator has a *deposit*; when a validator joins, its deposit is the
 number of deposited coins. After joining, each validator's deposit rises and
 falls with rewards and penalties. Proof of stake's security derives from the
 size of the deposits, not the number of validators.

*justified*, *finalized*<br>
If a validator violates either slashing condition, the evidence of the violation
 can be included into the blockchain as a transaction, at which point the
 validator's entire deposit is taken away with a small "finder's fee" given to
 the submitter of the evidence transaction. In current Ethereum, stopping the
 enforcement of a slashing condition requires a successful 51% attack on
 Ethereum's proof-ofwork block proposer.<br>
two fundamental properties: *accountable safety* and *plausible liveness*.
 Accountable safety means that two conflicting checkpoints cannot both be
 finalized unless ≥ ⅓ of validators violate a slashing condition (meaning at
 least one third of the total deposit is lost). Plausible liveness means that,
 regardless of any previous events (e.g., slashing events, delayed blocks,
 censorship attacks, etc.), if ≥ ⅔ of validators follow the protocol, then it's
 always possible to finalize a new checkpoint without any validator violating a
 slashing condition.<br>
To avoid this, we introduce a novel, correct by construction, fork choice rule:
 FOLLOW THE CHAIN CONTAINING THE JUSTIFIED CHECKPOINT OF THE GREATEST HEIGHT.
 This fork choice rule is correct by construction because it follows from the
 plausible liveness proof.<br>
The *dynasty of block b* is the number of finalized checkpoints in the chain
 from root to the parent of block *b*. We call *d* + 2 this validator's *start
 dynasty*, DS(v) / *end dynasty*, DE(v). Once validator v leaves the validator
 set, the validator's public key is forever forbidden from rejoining the
 validator set. This removes the need to handle multiple start/end dynasties for
 a single identifier.<br>
At the start of the end dynasty, the validator's deposit is locked for a long
 period of time, called the *withdrawal delay* (think "four months' worth of
 blocks"), before the deposit is withdrawn. If, during the withdrawal delay, the
 validator violates any commandment, the deposit is slashed.

