
A blockchain-based system is a classical distributed system with shared state
 (i.e. the blockchain).

permissionless and permissioned (Hyperledger Fabric, Multichain)<br>
A private blockchain is a special permissioned blockchain operated by one
 entity, i.e., within one single trust domain.<br>
Permissioned blockchains address many of the problems that have been studied in
 the field of distributed computing over decades, most prominently for
 developing Byzantine fault-tolerant (BFT) systems.

The DAG (directed acyclic graph) changes and is totally different for each epoch
 in the Ethereum system. An epoch is identified as a time period taken to
 generate 30000 blocks. The DAG only depends on the block height and the clients
 can pre-generate and cache the DAG. DAG is needed for mining only and not for
 verfication. The Ethereum network adjusts the difficulty level to produce a
 block every 15 seconds.

Hyperledger Fabric provides a flexible architecture with a pluggable consensus
 model. It also support smart contracts on the blockchain, also known as
 chaincode. Hyperledger currently supports two consensus models---the popular
 Practical Byzantine Fault Tolerance algorithm (PBFT) and its variation SIEVE
 that is able to handle non-deterministic chaincode execution. Current proposals
 are considering Crash Fault Tolerance (XFT), which a variation of Paxos with
 Byzantine Fault Tolerance built-in, as an alternative consensus algorithm for
 future versions.

Therefore one needs to apply mathematical reasoning and formal tools to reason
 why the solution would remain secure under any scenario permitted by the stated
 trust assumption. Without such reasoning, security claims remain vague.<br>
Already since the 19th century, Kerckhoffs' principle has been widely accepted,
 which states that "a cryptosystem should be secure even if everything about the
 system, except the key, is public knowledge."<br>
Protocol designers today prefer the *eventual synchrony* assumption for its
 simplicity and practitioners observe that it has broader coverage of actual
 network behavior, especially when compared to so-called partially synchronous
 models that assume probabilistic network behavior over time.<br>
We discuss only protocols for static groups; they require explicit group
 reconfiguration and do not change membership otherwise. This assumption
 contrasts with view-synchronous replication, where the group composition may
 change implicitly by removing nodes perceived as unavailable.

PoS 방식의 합의 방식인 캐스퍼, 블록내 트랜잭션의 병렬 처리를 가능하게 하는 샤딩,
 거래 당사자간의 직거래를 가능하게 하는 라이덴 네트워크

"airdropped" cryptocurrency forked from the main bitcoin chain, which is
 distributed to anyone who owned bitcoin at the time of the split

