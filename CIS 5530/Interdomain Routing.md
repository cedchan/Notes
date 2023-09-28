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

Distance vector (chosen)
- Per-destination updates provide mode control
- Wasn't designed to implement policies
- Vulnerable to loops

Distance vector was expanded into the final algorithm: **Border Gateway Protocol (BGP)**.

### Path Vector Protocol

The basic idea of BGP is that it uses the distance vector algorithm, plus some extra information. Specifically, it stores the complete path, which uses more storage, but doesn't use more computation.