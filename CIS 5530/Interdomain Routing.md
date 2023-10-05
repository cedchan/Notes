## Structure of the Internet

There isn't a central authority that manages the internet, so much of what dictates the internet's system is distributed multilateral decisions.

>[!definition]
>- **End hosts**, **clients**, or **users**: Run layers 1-7
>- **Autonomous systems (AS)** or **domains**: Region of a network under a single administrative entity (e.g., Penn)
>	- Every AS is assigned a unique number
>- **Border routers**: Routers that it on the edges of ASs to talk to other border routers.
>- **Interior routers**: Regular routers that connect layer 3 devices
>- **Route** or **path**: Path of routers and devices

### Timeline of the Internet

|Time|State|
|-|-|
|Pre-1995|The government still controlled the internet, so everybody connected through the government backbone.|
|Circa-1995|The "backbones" were sold off to different private companies (ISPs)|
|Today|Increased consolidation and conncetivity options. ("Flattening" of the hierarchy.)|

Since privatization, there have emerged a couple of tiers of networks.
- **Tier 1**: Global ISPs. Networks that peers with every other network to reach the Internet. (E.g., AT&T, Lumen Tech., Verizon, etc.)
- **Tier 2**: Peers with some networks, but still purchases IP transit to reach at least some portion of the internet.
- **Tier 3**: Solely purchases transit from other networks to reach the internet.

Today, the lines between tiers have blurred a bit more, however.
### Routing Between ASs

Goals of ASs:
- Freedom in picking routes
- Autonomy
- Privacy

Given these goals, and the structure of the internet, there were some considerations for deciding a routing algorithm.

Link state
- Scaling limitations (memory usage was okay for small networks, but not the internet)
- No privacy—broadcasts all information
- Limited autonomy—needs agreement on metric
- Converges faster (bypasses count to infinity, etc.)

Distance vector (chosen)
- Per-destination updates provide more control
- Wasn't designed to implement policies
- Vulnerable to loops

Distance vector was expanded into the final algorithm: **Border Gateway Protocol (BGP)**.

### Path Vector Protocol

The basic idea of BGP is that it uses the distance vector algorithm, plus some extra information. Specifically, it stores the complete path, which uses more storage, but doesn't use more computation.

Advantages:
- Can make policy choices based on ASs in path
- Can easily avoid loops

### Advertising Routes

Nodes advertise all the routes they want neighbors to know (to the order of 50-200k). Then these advertisements are incrementally updated to inform neighbors of changes.

There are a couple of message types in BGP:
- Open: Establishes session with TCP
- Update: Informs of newly active/inactive connections
- Keepalive: Informs that connection is still active

## Policy

**Selection** controls whether/how traffic leaves network by assessing which of the available paths to take. **Export** is how paths are advertised. That is, it controls how traffic enters the network.

How BGP works (i.e., how selection and exporting happens) is highly influenced by the business side of the internet.

### Inter-AS Business Relationships

There are typically two types of business relationships:
- **Customer to provider**
- **Peer to peer**

Customer-to-provider relationships (e.g., a household to Comcast) involve payment from the customer to provider, whereas peers don't pay each other. 

You have to pay both directions on each route. Most of the time, you're not paying per packet. Payment supports connectivity (funds backbone's infrastructure), so it shouldn't be thought of as "postage."

The hierarchical [tiers](Interdomain%20Routing.md#Structure%20of%20the%20Internet#Timeline%20of%20the%20Internet) of providers are based on who has peer-to-peer relationships. 

### Flattening of the Internet

Because peering relationships allow ISPs to cut out the "middleman" (i.e., higher tier providers), there are incentives for companies to do so.

**Internet exchange points** are companies that own real estate where ISPs can connect with border routers and peer with other IPSs. Because this saves ISPs money, and has become relatively easy, many ISPs have chosen to take these routes, flattening the internet by cutting out higher levels.

>[!note]
>Peers do not provide transit between other peers.

![](Pasted%20image%2020231002160409.png)
Here, the red line doesn't work because B won't get money while A and C will.

### Typical Policies

Typical **selection policy**, in decreasing order of priority
- Make/save money (to customer > peer > provider)
- Maximize performance (smallest path length)
- Minimize use of my network bandwidth ("hot potato" between ISPs who don't want to hold the packet)

Typical **export policy**:

|Destination prefix advertised by|Export route to|
|-|-|
|Customer|Everyone (providers, peers, customers)|
|Peer|Customers|
|Provider|Customers|

These are the **Gao-Rexford rules**. They're common practice, although not required. In short, these rules necessitate that the AS policy graph is a [DAG](Directed%20Acyclic%20Graphs%20(DAGs).md). 

### Multi-Homing

As a customer, people sometimes connect to multiple providers for reliability and pricing, among other reasons.

Then, the customer can choose which paths to take based on all advertisements and prices.


## Border Gateway Protocol (BGP)

BGP does the same loop as does distance vectors. 

![](Pasted%20image%2020231002161640.png)

### Differences with Distance Vectors

1. **Doesn't pick shortest path:** BGP selects based on policy.
2. **Path-vector routing:** Advertise entire path (while DV sends distance metric per destination). This allows for loop avoidance, and more policy control (can see which ASs are coming)
3. **Selective route advertisement:** May choose not to advertise everything.
>[!note]
>This means that reachability is not guaranteed.
4. **BGP may aggregate routes**: Not common today because of security, but possible for scalability.

### Types of BGP

- **eBGP**: Between border routers in different ASes
- **iGP**: Sessions between border routers and other routers within the same AS.
- **IGP (Interior Gateway Protocol):** Traditional intra-domain routing protocol.

### Route Attributes

BGP route updates are formatted as (IP prefix, route attributes). They are either **announcements** to indicate a new route or **withdrawals** to indicate that a route has disappeared.

Routes are described using **attributes**. There are some standardized ones:
- **ASPATH**: Vector that lists ASes in a route advertisement has traversed (in reverse order)
- **LOCAL PREF**: local preference in choosing between AS paths (typically only in iBGP). Higher value = more preferred
- **Multi-exit Discriminator (MED)**: Used when ASs connected via 2 or more links. Specifies how close a prefix is to the link it's announced on. Lower is better.
- **iGP Cost**: Used for hot-potato routing. Number of "hops"

Rules for route selection:
![](Pasted%20image%2020231002162803.png)

### Issues with BGP

- **Reachability**: With policy routing, even if a connection exists, there might not be connection.
- **Policy over performance**
	- E.g., hot potato routing—routing to another AS as quickly as possible, routes to the nearest exist point, causes convergence delays
	- 20% of internet paths inflated by at least 5 router hops