## Introduction

[Spanning trees](Components%20of%20a%20Network.md#Flooding) provide basic connectivity. But they waste capacity and lack optimality.

The theoretical underpinning of routing is that the network is modeled as a graph, where routers are nodes and links are edges. The goal, then, is to determine the "best" path through the network from source to destination.

"Best," of course, isn't as simple as Dijkstra. There are many considerations:
- Latency
- Bandwidth
- Money
- Security
- Hops

We'll use a simpler approximation in this class:
1. Assign each link a cost 
2. Define the "best" path as that with the lowest cost
3. Pick randomly to break ties

### Sink Trees

By our definition of shortest path, every subpath of a shortest path is a shortest path. Then, each node only needs to send to the next hop. The forwarding table only know the next hop (although the routing table may know more).

### Forwarding vs. Routing

- Forwarding is layer 2 vs. routing is layer 3 
- Forwarding is through learning routing is through routing protocol

### Routing Protocols

There are 2 main routing protocols for intradomain routing: [distance vector](Intradomain%20Routing.md#Distance%20Vector) and [link state](Intradomain%20Routing.md#Link%20State).

## Distance Vector

>[!idea]
>- All neighbors start with a weight of infinity
>- Maintain vector of cost associated with destinations
>- Tell neighbors about learned distances

%% $$\begin{align}
1 Initialization:
2 for all neighbor's V do 3 if V adjacent to A 4 D(A,V) = c(A,V); 5 else 6 D(A,V) = ∞; 7 loop: 8 wait (until A sees a link cost change to neighbor V 9 or until A receives update from neighbor V) 10 if (D(A,V) changes by d) 11 for all destinations Y through V do 12 D(A,Y) = D(A,Y) + d /* May result in changing next hop to Y */ 13 else if (update D(V, Y) received from V) /* shortest path from V to some Y has changed */ 14 D(A,Y) = min(D(A,Y), D(A,V) + D(V,Y); /* May result in changing next hop to Y */ 15 if (there is a new minimum for destination Y) 16 send D(A, Y) to all neighbors 17 forever
\end{align}$$ %%

$D()$ distance, $c()$ cost

>[!error]
>check slide

### Link Cost Changes

Things start to get interesting when link costs change. The endpoint nodes of the link will detect this change, then update their routing info, recalculating their distance vectors. Then, if there is a change in the DV, they'll notify their neighbors. 

>[!hint]
>In slides, D is destination, C is cost, N is next hop.

Problem: Good news travels fast, but bad news travels slowly. This is known as the **count to infinity problem**.

>[!error]
>lol look up

#### Poisoned Reverse

One approach to handling the count to infinity problem is **poisoned reverse**. Here, we use the same protocol, but if B is advertising to a node whose next hop is B, it'll say its distance is infinity, so that that route won't be taken.

>[!error]
>look up

This won't work, however, with loops of size >3

#### Routing Information Protocol

**Routing Information Protocol (RIP)** was an early IP routing protocol. To address the count to infinity problem, it simply enforced a maximum cost of 16 for each link. Then, even if the problem occurred, it would be capped at 16.
## Link State

>[!idea]
>- Distribute a map of the network to all the nodes
>- Specifically, each node gets distances with its neighbors, then floods that information out
>- Then, Dijkstra is run on the network

### Flooding

The difference between flooding and broadcasting is that flooding keeps track of what messages each node has seen, so that they won't be repeatedly cycled through the network. 

Challenges:
- Loops
- Packet loss
- Out-of-order arrival

Solutions:
- Sequence numbers: Every advertisement is tagged with a monotonically increasing, unique sequence number that allows for duplicate detection. Each node has its own set of sequence numbers.
- Acknowledgements and retransmissions
- Time-to-live for each packet

## Link State vs. Distance Vector

|Issue|LS | DV|
|-|-|-|
|Storage|Store all links (entire network)|Entry for each possible destination/hop|
|Convergence|Reacts more quickly, in bounded time, to connectivity changes|Count-to-infinity problem. Slower convergence. Bounded path length (16)|
|Global policies|Able to impose global policies in a globally consistent way|Harder, since don't have complete network topology.|

Link state is by far more popular than distance vector.