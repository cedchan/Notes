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

>[!error]
>check slide

### Link Cost Changes

Things start to get interesting when link costs change. The endpoint nodes of the link will detect this change, then update their routing info, recalculating their distance vectors. Then, if there is a change in the DV, they'll notify their neighbors. 

## Link State