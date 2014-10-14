Raft
====

Raft is a simple consensus algorithm, an alternative to Paxos. This project provides an embeddable library to store consistent replicated log. Also the clients can run this as a service. 

Consensus algorithm is usually a way to build replicated state machines.

It provides the clients with a simple function

updateState(byte[])

The library just replicates the byte[] array across all servers. Also the library provides the hook for the clients to plugin what to do when a log can be committed to a state machine. The library abstracts leader election, replicating logs across the cluster of machines, adding/removing a member from the cluster. 

Architecture
====

1) Logs and other relevant information are stored on LevelDB. LevelDB uses log structured merge tree, which provides higher write throughput. 
2) When a log is replicated across majority of the servers, the log can be applied to state machine. As this library just takes care of replicating the logs, the client has to maintain the actual state machine. 

Performance
====


Unit testing
====

This library provides a simpler unit testing code base, using which you can easily launch virtual set of servers, and you can inject failures (like shutdown server, restart a server, make a partition between set of servers), but does not provide a way to test network failures.

