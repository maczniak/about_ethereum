
Hyperledger Fabric is a platform for distributed ledger solutions, written in
 Golang and with a modular architecture that allows multiple implementations for
 its components. It is one of multiple blockchain frameworks hosted with the
 Hyperledger Project and aims at high degrees of confidentiality, resilience,
 flexibility, and scalability.

Iroha is another open-source blockchain platform developed under the Hyperledger
 Project. Its architecture is inspired by the original (v0.6) design of Fabric.
 All validating nodes collaboratively execute a Byzantine consensus protocol. In
 that sense it is also similar to Tendermint and Symbiont Assembly.

Tendermint Core is a BFT protocol that can be best described as a variant of
 PBFT, as its common-case messaging pattern is a variant of Bracha's Byzantine
 reliable broadcast. In contrast to PBFT, where the client sends a new
 transaction directly to all nodes, the clients in Tendermint disseminate their
 transactions to the validating nodes (or, simply validators) using a gossip
 protocol. Tendermint's most significant departure from PBFT is the continuous
 rotation of the leader.

Symbiont Assembly is a proprietary distributed ledger platform.

Corda does not order all transactions as one single virtual execution that forms
 the blockchain. Instead, it defines states and transactions, where every
 transaction consumes (multiple) states and produces a new state. Only nodes
 affected by a transaction store it. Since a node stores only a part of the
 Hash-DAG, it only knows about transactions and states that concern the node.

Juno from kadena is a platform for running smart contracts that has been
 developed until about November 2016 according to its website. Later Juno has
 been deprecated in favor of a "proprietary BFT-consensus protocol" called
 ScalableBFT, which is "inspired by the Tangaroa protocol" and optimizes
 performance compared to Juno and Tangaroa.

The Chain Core platform is a generic infrastructure for an institutional
 consortium to issue and transfer financial assets on permissioned blockchain
 networks.

Quorum, mainly from developers at JPMorgan Chase, is an enterprise-focused
 version of Ethereum, executing smart contracts with the Ethereum virtual
 machine, but using an alternative to the default proof-of-work consensus
 protocol of the public Ethereum blockchain. The platform currently contains
 two consensus protocols, called QuorumChain and Raft-based consensus.
 (Raft-based consensus) Quorum uses the implementation in etcd and co-locates
 every Quorum-node with an etcd-node (itself running Raft).

The MultiChain platform is intended for permissioned blockchains in the
 financial industry and for multi-currency exchange in a consortium, aiming at
 compatibility with the Bitcoin ecosystem as much as possible. MultiChain uses a
 dynamic permissioned model.

Another extension of the Ethereum platform is HydraChain, which adds support for
 creating a permissioned distributed ledger using the Ethereum infrastructure.
 The repository describes a proprietary consensus protocol "initially inspired
 by Tendermint."

The Swirlds hashgraph algorithm is built into a proprietary "distributed
 consensus platform"; a white paper is available and the protocol is also
 implemented in an open-source consensus platform for distributed applications,
 called Babble.

The Hyperledger Sawtooth platform provide means for running general-purpose
 smart contracts on a distributed ledger. It can use a permissioned and a
 public, permissionless mode. The platform also introduces a novel consensus
 protocol called Proof of Elasped Time (PoET).

Ripple and Stellar are two globally operating exchange networks with built-in
 cryptocurrencies; unlike Bitcoin, they do not involve mining and operate in a
 somewhat permissioned fashion.

IOTA is heralded as a "cryptocurrency without a blockchain" and creates a
 Hash-DAG instead, which is called the tangle. All of its tokens are created at
 the outset.

"Bitcoin Cash is what I started working on in 2010,"
 [tweeted Gavin Andresen](https://twitter.com/gavinandresen/status/929377620000681984)
 on Saturday. The endorsement is significant because Andresen was chosen by
 founder Satoshi Nakamoto to lead the Bitcoin project after Nakamoto faded from
 the scene in 2011. Andresen was
 [frozen out of the Bitcoin Core development team](https://www.theguardian.com/technology/2016/may/06/bitcoin-project-blocks-out-gavin-andresen-over-satoshi-nakamoto-claims)
 last year in the midst of a bitter debate over the network's future.<br>
But others saw decentralization as the essential attribute of the Bitcoin
 network. They worried that enabling a flood of transactions would make it too
 difficult for ordinary people to participate in Bitcoin's transaction-clearing
 process. They have promoted a hack called segregated witness that helps to
 squeeze more transactions into each one-megabyte block. But beyond that, they
 have
 [argued](https://medium.com/@jgarzik/bitcoin-is-being-hot-wired-for-settlement-a5beb1df223a)
 that it's actually healthy for Bitcoin fees to rise over time to prevent the
 network from getting cluttered with low-value transactions. Later that month,
 the main Bitcoin network activated the
 [segregated witness](https://en.wikipedia.org/wiki/SegWit) hack, which moves
 cryptographic signatures outside the one-megabyte block limit. This change has
 roughly doubled the capacity of the network and brought some temporary relief
 to congestion that had plagued the network for months.<br>
Small-block fans have pinned their hopes on
 [Lightning](https://en.wikipedia.org/wiki/Lightning_Network), a new type of
 payment network that allows people to make fast, small Bitcoin payments without
 having to post every transaction to the Bitcoin blockchain. In theory,
 Lightning could allow millions of bitcoin-denominated payments to happen every
 day without changing Bitcoin's one-megabyte block size limit. But Lightning is
 still in development, and it's far from clear if it will work as well as
 advocates hope.<br>
Hong Kong-based LightningAsic CEO Jack Liao,
 [to-do list](https://trello.com/b/P1rLw1G9/bitcoin-gold-todos),
 [GitHub](https://github.com/BTCGPU/BTCGPU),
 [Slack group](https://bitcoin-gold.slack.com/)<br>
Critics have objected to the unusual way that Bitcoin Gold launched the
 currency. After forking the main Bitcoin blockchain a few weeks ago, the
 Bitcoin Gold team operated the new network privately, allowing them to mine a
 bunch of "gold" bitcoins without competition from the rest of the Bitcoin
 world.<br>
PoW charts:
 [Johoe's Mempool Size Statistics](https://jochen-hoenicke.de/queue/#2w),
 [fork.lol](https://fork.lol/pow/hashrate)

