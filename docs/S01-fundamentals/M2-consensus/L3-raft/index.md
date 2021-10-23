  Raft Consensus Tutorial
=======================

  Please go to the [Secret Lives of Data](http://thesecretlivesofdata.com/raft/){target=_blank} website to learn about the basic mechanics of the [Raft consensus protocol.](https://en.wikipedia.org/wiki/Raft_(algorithm){target=_blank}) While Raft is a production-ready consensus protocol, we are mainly using it here to show you a concrete example of a distributed system maintaining state across different nodes in a network.

 Please note, Raft is **not** a Byzantine fault tolerant consensus protocol. Instead, Raft is a **leader-led** consensus protocol, meaning all the nodes blindly trust whatever state the leader sends to them. However, in Raft, if the leader fails in some way and stops sending state, the other nodes in the network are able to identify the failure and re-elect another leader in a distributed way. In this way, the Raft consensus mechanism shows how a distributed system can replicate state in a resilient way.

 Even if you never see it or use it again, we hope learning about Raft will give you a better sense of how a distributed system can use a consensus protocol to adapt to node failures. 

 Additional Resources
--------------------

 * [Wikipedia: Raft](https://en.wikipedia.org/wiki/Raft_(algorithm){target=_blank})
* [Article: In Search of an Understandable Consensus Algorithm](https://raft.github.io/raft.pdf){target=_blank}
* The Raft consensus protocol was developed as a simpler alternative to the [Paxos consensus algorithm](https://en.wikipedia.org/wiki/Paxos_(computer_science){target=_blank}) developed by Leslie Lamport.

 