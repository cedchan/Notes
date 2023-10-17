Types of question
- Regurgitation
- Application
- Scenarios

subnet mask? (range of ips)

layer 2 → forwarding table (destination → port)
Router: Routign table, ARP, forwarding table
NAT: like router, but with NAT table
Switch: Forwardng table
Hosts: superset of all tables (because it's layer 1-7)

## Vocab

**Link:** Physical medium (e.g., optic fiber, coaxial cable)
**Node:** Computers that links connect
**Router:** Node that connects two networks (also called gateway)
**Multiplexing:** Resource shared by multiple users
**Statistical multiplexing:** Allocates resources in a cost-effective way for multiple nodes to share resources
**Packet:** Granularity at which links are allocated to different flows
**LAN:** Local area network (<10km)
**WAN:** Wide area network (can be worldwide)
**MAN**: Metropolitan area network (10s of kms)
**SAN:** Storage area networks (connect components of a computing system)
**Trailer:** Control information (like header info) but at the end of payload
**Demultiplexing (demux) key:** Identifier in header that says what application a message belongs to (no uniform agreement on what constitutes a demux key)
**Soft-state:** It's not immediately critical, and it can be regenerated (by sending to all addresses), so MAC address learning isn't a problem to the concept of availability in the internet.

## Internet History

- Telephone network = largest network in 50s
	- Used circuit switching (plugging in different ports)
- Need network for defense, computers, etc.
	- Circuit switching unreliable, inefficient

Phase 1: Early Connection
- 1961: Baran, Kleinrock advocate packet switching
- 1962: Licklider's vision of Galactic Network (global set of computers, everyone can access data)
- 1965: Roberts connects two computers via phone
- 1967: Roberts publishes vision of ARPANET
- 1969: BBN installs first IMP (= Interface Message Processor) at UCLA 
![](Pasted%20image%2020231012172542.png)

Phase 2: Internetworking

- 1971 Network Control Program (protocol)
- 1972 Public demo of ARPANET
- 1972 Email invented
- 1972 Telnet introduced
- 1973 FTP introduced
- 1973 Ethernet invented (Xerox PARC)
- 1973 Cerf and Kahn paper on TCP/IP
- 1980 TCP/IP adopted as defense standard
- 1983 Global NCP to TCP/IP flag day

Phase 3: Rapid rowth
- 198x XNS DECbit, and other protocols
- 1984 Janet (British research net)
- 198x Internet meltdowns due to congestion
- 1986 Van Jacobson saves the internet (BSD TCP)
- 1988 Dave Clark steps down from IAB
- 1989 Birth of the web: Tim Berners-Lee (CERN) invents HTTP

Phase 4: The Web
- 1993 Search engines 
- 1994 Internet commericializes
- 199x ATM rises and falls
- 199x Qos rises and fallse
- 1998 IPv6 specification
- 1998 Google reinvents search
- 2000 Dot-com bubble burst

Phase 5: The Cloud
- 1997 The term “Cloud Computing” is coined 
- 1998 Rackspace founded 
- 1999 Salesforce founded 
- 2006 Amazon EC2 and AWS are launched Went from a bookseller to a cloud computing company 
- 2006 YouTube purchased by Google
- 2007 Rise of the iPhone, netflix starts streaming 
- 2010 Instagram founded

Phase 6: Decentralization?
- 2016 Netflix rolls out CDN (content delivery network)
- 2020 Zoom stock's price rises

Single distributed routing protocol → igp (interior gateway protocol) and egp (exterior gateway protocol), regions of networks and connections btwn them

## Design Goals

**Protocols** define syntax and semantics of communication

![](Pasted%20image%2020231012215153.png)

Communication networks could be broadcast or switched
Broadcast:
- Nodes share a common channel
- Everyone hears everyone else
Switched
- Information transmitted through small subset (usually one) node (e.g., router)

Subdivide switch into circuit and packet switched

circuit switching
- 3 phases
	1. Circuit establishment
	2. Data transfer
	3. Circuit termination
- Guaranteed capacity until circuit termination
- If circuit not available, "busy signal"
![](Pasted%20image%2020231012215619.png)



Datagram packet switching
- Each packet independently switched
- Packet header contains destination
- Compute next hop
- Resources not pre-allocated
![](Pasted%20image%2020231012215735.png)

Packet switching vs. broadcast
Advantages:
- No connection state needed
- Easy to recover from error
- Minimal network assumptions
Disads
- No guarantees
- Slow with a lot of data

### Design Goals

Fundamental Goal: Technique for multiplexed utilization of existing interconnected networks (multiplexed = shared)
- Originally: connect ARPANET with ARPA radio network

Second-level goals
- Resilience
- Heterogeneity
- Distributed management
- Cost
- Easy host attachment
- Resource accountability

Goal 2: Survivability
- Be able to keep communicating if device in middle fails
- Key issue: state (e.g., information on location, authentication, message type, etc.)
	- Replication: Network keeps state for you, replicates throughout network for tolerance
		- Difficult to engineer, still fallible
	- Fate sharing (chosen): End hosts responsible for own state, loses information iff host goes down
		- Easy to engineer, but tradeoff in performance

Goal 3: Heterogeneity
- Abstraction through layering → can swap out individual layers (e.g., WiFi vs. ethnernet)
- Best effort

![](Pasted%20image%2020231012220901.png)

Goal 4: Distributed management
- Decentralized (thousands of ISPs)
- ASs manage internal system

Less cared about goals
Goal 5: Cost effectiveness
- Many inefficiencies, retransmission
- But... speeds have increased rapidly as a result

Goal 6: Ease of attachment
- Anything can connect through IP (waist), but bit difficult for implementation

Goal 7: Resource accountability
- Not prioritized at all, billing much less precise than phone
- Convoluted business relationships, hot-potato routing

Missing
- Security
- Availability
- Loss tolerance

Types of errors
1. Bit errors (bit flips, happen in physical link)
2. Packet errors (whole packets lost)
3. Node/link level (loses connection, cuts)

Protocols
- Service interface: Operations local (same computer) objects can perform on protocol
- Peer interface: How other computers interact with protocol
- Protocols are horizontal, layers are vertical

OSI vs internet
![](Pasted%20image%2020231015000019.png)

![](Pasted%20image%2020231015000544.png)

Hop-by-hop vs. end-to-end reliability
- Hop-by-hop is checks at each node, end-to-end is just at hosts
- E2e won because
	- High level errors can still occur with hop-by-hop, so e2e is needed anyway
	- Still lots of trradeoffs, have to restart from beginning

## Performance Metrics

Link level
- **Bandwidth:** Maximum rate (bps) sender can send data
- **Propagation delay:** Time for signal to travel from source to destination (T = distance / speed)
![](Pasted%20image%2020231015001537.png)
- **Packet transmission time:** Time it takes for sender to transmit all bits (size / bandwidth)
- **Throughput:** Total number of bits transmitted over length of time (transfer size / time)
- **Link utilization:** (throughput) / (link capacity)

Node level
- **Queuing delay:** Time to wait before transmission because other haven't been sent yet (Queue Length / Bandwidth)
- **Processing time:** Time it takes for router to process header, etc.

Other
- **Latency** = Propagation + Transmit + Queuing Delay
- **Bandwidth-delay product:** Product of bandwidth and delay. It is the "storage" capacity of the network.
- Informally, **jitter** is the change in latency from packet to packet.
	- Router: queuing delays, congestion
	- Links: failures leading to alternate paths taken
	- Jitter $=|(RxA-TxA)-(RxB-TxB)|$, where $RxC, TxC$ denote the receive and transmit time of packet $C$. That is, it's the difference in the latencies of packets $A, B$. 
	- **Example.** Packet $A$ takes $15$ ms to travel the network, and Packet $B$ takes $18$ ms. Jitter $=| 15 - 8 | = 3$ ms

## Components of a Network

**Make this a table** 
Layer 1: Physical Layer
- Connects: Transmitters and receivers
- Lower interface: Analog signals
- Upper interface: Stream of digital bits
- Name of network: Physical links
- Name of message: Bits
>**Example.** WiFi networks → receivers

Layer 2: Data Link Layer
- Connects: Physical interfaces
	- Usually the same physical layer protocol
- Lower interface: Stream of bits
- Upper interface: Messages with payloads
- Name of network: Local Area Network (LAN)
- Unit of data: Frame (of data)

Layer 3: Network Layer
- Connects: LANs
	- Possibly different technologies (e.g, WiFi and Ethernet, which are different L2 protocols)
- Lower interface: A packet of data
- Upper interface: A segment of data
	- Same thing, but with an extra header
- Name of a network: Internet

>[!hint]
>Data goes analog → bits → frames → packets → segments. Frame → segment are all just arrays of data.

Layer 1
- **Ether** is like a giant cable that everyone taps in and out of
- Originally connected with vampire taps
- Wires: Twisted, coaxial, optical networks
- Network adapters connect nodes and links, convert to/from bits
- Wireless
- Repeaters
- Hubs: Multi-port receivers
- Issues: Doesn't support multiple technologies, data sent everywhere

Layer 2
- Medium Access Control (MAC) address: Globally unique address
	- Blocks assigned to vendors, adapters assigned by vendors to devices
	- Broadcast Address FF:FF:FF:FF:FF:FF
	- Promiscuous mode reads all, not just intended messages
	- CSMA/CD (Carrier Sense, Multiple Access with Collision Detect): try using port with exponential wait (min 46 bytes, max 1500)
- Demux key: Preconfigured code that says what protocol something is
- Framing problem: How do we know when a frame ends?
	- Byte count: Start each frame with length field. Problem: if has one error, hard to resynchronize
	- Byte stuffing: FLAG byte that marks start/end, with ESC byte
	- Bit stuffing: Same, but use 6 consecutive 1s as a flag, insert/remove a 0 after 5 consecutive 1s in the data.
- Bridge: Connects 2 or more segments
- Switch: Like bridge, but connects to hosts, not segments
	- Self-learning with incoming messages and TTL
- VLANs: Partition 1 physical LAN into many sections using software for organization
	- Bridges/switches need config tables

Bridges/Switches vs. Hubs/Repeaters
- Can filter segments
- But cause delay + must create forwarding table
	- Solution: cut-through switching (just look up destination and forward without error detection)

Flooding
- Spanning tree to avoid (L2 protocol)
	1. Everyone advertises self as root w dist 0 (A, A, 0), (B, B, 0)
	2. If receive advertisement with lower root identifier, that becomes new root, take new dist
	3. If nodes on ends of ports are closer to root than you, stop broadcasting there
	4. Stable when only the root is broadcasting
	- Soft state for failure tolerance
	- Open ports are in **forward state**, otherwise **blocked state**

Layer 3
![](Pasted%20image%2020231015164435.png)
![](Pasted%20image%2020231015164515.png)

- IP → 32 bits
- Private IP addresses: 10.0.0.0-10.255.255.255, 192.168.0.0-192.168.255.255
- Public IP addresses: Hierarchical under IANA → regional bodies (RIRs) → companies (later, DHCP)
- TCP (transport control protocol): Reliable byte stream delivery
- UDP (user datagram protocol): unreliable datagram delivery

Classless Interdomain Routing (CIDR)
- XXX.XXX.XXXX.XXXX/y, y is prefix length
	- E.g., 128.23.9.0/26 means first 26 bits are prefix 128.23.9, with $2^6=64$ remaining addresses → range 128.23.9.0-128.23.9.63
- More specific = longer prefix = fewer addresses
- Less specific = shorter prefix = more addresses
- Can aggregate into **supernets**, but rare for security
- Routing lookup: Find the longest matching prefix (aka the most specific route) among all prefixes that match the destination address.

Ipv6
- 128 bits (8 groups of 4 hex digits)
- No checksum
- To solve Ipv6/4 compatibility: **tunneling**, make Ipv6 datagram payload of ipv4 packet between ipv4 routers, then unwrap

NATs (L3-L4)
- Convert private IP to public (from outside, looks like all going to different ports of same device), key and val are both tuples with IP and L4 demux key
- From host perspective, just use priv. IP
- Use L4 demux key to distinguish on both sides (uniquely IDs)
- Advantages: Control over many hosts, rapid deployment path
- Disads: Breaks connectivity, relies on specific L4 protocol, breaks e2e principle
- Subnet is breaking net into smaller parts
	- Hosts given subnet mask and ip address
	- All hosts in subnet have same mask
	- Subnet mask bitwise AND ip address = subnet number

## Intradomain Routing
- Domain: region under single enterprise, ISP, etc
- Doing better than spanning tree: Shortest path from each
- Shortest paths form a sink tree
- Forwarding = L2, through learning, maps MAC to port (L1); routing = L3, through routing protocol, maps IP to next hop IP

DV
- Routing Information Protocol (RIP) based on Bellman-Ford
- Maintain distance vector to all destinations, periodically broadcast
- Good news fast, bad news slow
- Poisoned reverse (on loops <4): Set to infinity
- Split horizon: Don't send information in direction it comes from
- Limited Infinity (e.g., 16 hops)
- Minimal overhead, but slow convergence

LS
- Open Shortest Path First (OSPF) based on Dijkstra
- Each node maintains graph topology by flooding info about neighbors through graph
- Challenges: loops, packet loss, out-of-order arrival
- Solutions: Sequence numbers, acknowledgments, TTL
- High overhead, fast convergence

|Issue|LS | DV|
|-|-|-|
|Storage|Store all links (entire network)|Entry for each possible destination/hop|
|Convergence|Reacts more quickly, in bounded time, to connectivity changes|Count-to-infinity problem. Slower convergence. Bounded path length (16)|
|Global policies|Able to impose global policies in a globally consistent way|Harder, since don't have complete network topology.|

Link state used typically
## Interdomain Routing

>[!definition]
>- **End hosts**, **clients**, or **users**: Run layers 1-7
>- **Autonomous systems (AS)** or **domains**: Region of a network under a single administrative entity (e.g., Penn)
>	- Every AS is assigned a unique number
>- **Border routers**: Routers that are on the edges of ASs to talk to other border routers.
>- **Interior routers**: Regular routers that connect layer 3 devices
>- **Route** or **path**: Path of routers and devices

Internet hierarchy over time
- Pre-1995: All go through ARPANET (gov)
- Circa-1995: Strict hierarchy with gov-funded backbones on top
	- Tier 1: AT&T, Lumen, etc
	- Tier 2: Peers with some, but still purchases transit sometimes
	- Tier 3: Only purchases
- Today: More complex, lines blurred, hierarchy "flattened"

BGP (application layer)
- Want (1) freedom in picking routes, (2) autonomy in policy, and (3) privacy
- Choose DV, but extended into Border Gateway Protocol (BGP) for more policy control
- Same as DV, but stores entire path (i.e., extra storage, but same computation)
	- Format: IP prefix : route attributes
- Can make policy choices based on routers in path, can avoid loops
- Routers can be in multiple BGP sessions
- Start with all routes (50-200k), then only advertise changes
- Message types
	- Open: Establish session with TCP
	- Update: Inform neighbor of newly open (announcement) / closed (withdrawal) routes
	- Keepalive: Inform neighbor route is still fine
- Types of BGP
	- **eBGP**: Between border routers in different ASes
	- **iBGP**: Sessions between border routers and other routers within the same AS (also used by backbones).
	- **IGP (Interior Gateway Protocol):** Traditional intra-domain routing protocol.
- Route attributes
	- **ASPATH**: Vector that lists ASes in a route advertisement has traversed (in reverse order)
	- **LOCAL PREF**: local preference in choosing between AS paths (typically only in iBGP). Higher value = more preferred
	- **Multi-exit Discriminator (MED)**: Used when ASs connected via 2 or more links. Specifies how close a prefix is to the link it's announced on. Lower is better.
	- **iGP Cost**: Used for hot-potato routing. Number of "hops"
![](Pasted%20image%2020231015210601.png)

- Issues: Policy > performance, doesn't guarantee reachability, 20% of internet inflated by $\geq$ 5 hops, security, convergence

Policy
- Dictates selection (which path to use) and export (which paths to advertise)
![](Pasted%20image%2020231015205137.png)
- Customers pay providers, peers don't pay each other
- Internet exchange points now allow ISPs to easily peer
- Peers don't provide transit between peers (i.e., only if they get paid by someone)
- Multi-homing: Connect to multiple providers for reliability, less control over how rest of internet reaches us

Gao-Rexford Rules
- AS policy graphs are DAGs and are valley-free
- Selection policy (high → low priority):
	- Make money
	- Performance (shortest path)
	- Minimize use of own bandwidth (hot potato)
- Typical **export policy**:

|Destination prefix advertised by|Export route to|
|-|-|
|Customer|Everyone (providers, peers, customers)|
|Peer|Customers|
|Provider|Customers|

BGP vs DV
1. **Doesn't pick shortest path:** BGP selects based on policy.
2. **Path-vector routing:** Advertise entire path
3. **Selective route advertisement:** May choose not to advertise everything.
>[!note]
>This means that reachability is not guaranteed.
4. **BGP may aggregate routes**: Not common today because of security, but possible for scalability.

## Discovery

### DNS (L7)
- Host name (e.g., cis.upenn.edu): for humans, hierarchical, based on org
- IP address: for routers, hierarchical, based on org and topology
- MAC Address: for adapters, non-hierarchical

DNS goals
- Used to be sored on /etc/hosts file, couldn't handle as internet grew
- Uniqueness: no naming conflicts
- Scalable
- Distributed, autonomous admin
- Perfect consistency is a non-goal
- 3 hierarchies: Namespace, administration, servers

Hierarchical namespace
- Top level domains on top (edu, com, gov, mil, org, net)
- Subtrees

Hierarchical Administration
- Zone is portion of hierarchy an administration controls. (e.g., Penn controls `*.upenn.edu`)

Hierarchical Servers
- 13 root servers (top), labeled A-N
	- Location hardwired into other servers
	- TLDs belong to root
- Each zone as authoritative name server
- Anycast to replicate 13 roots
	- Routing chooses shortest path 
	- If several locations have same address, choose closest

Iterative DNS 
![](Pasted%20image%2020231015212327.png)
- Local DNS server to cache things

Recursive DNS (not used)
![](Pasted%20image%2020231015212343.png)
- Excess overhead in root (has to keep track of all requests)
- Allows reflection attack (target IP with huge payload, all root servers attack)

Resource records
- Distributed database storing with RRs
- RR format: (name, value, type, ttf)
- Type A: Name is hostname, value is IP address
- Type NS: Name is domain (e.g., foo.com), value is hostname of authoritative name server for this domain
- Type CNAME: Name is alias (e.g., ibm.com), value is canonical name (servereast.backup2.ibm.com)
- Type MX: Value is the name of mailserver associated with name

Reliability and speed
- Root and authoritative servers replicated, can ask alternates and reask
- Caching saves time
	- TTL: Small = fast response to change, large = higher cache hit rate
	- Top of hierarchy: days to weeks TTL
	- Bottom: Seconds to hours
- Negative caching: cache lookups that should fail (failure takes long time to find)

### ARP (L2)

How to find interface IP given MAC?
Address resolution protocol
- Each IP node (host, router) has ARP table `<IP; MAC; TTL>`
	- TTL ~20 min
- A wants to send to B, but doesn't have B in ARP table. A broadcasts (to all) ARP query packet with B's IP. B responds with B's MAC (unicast)
- Soft state

### DHCP (L7, but interacts with L2)
- Dynamic host configuration protocol
- Gets: Local IP, DNS IP, gateway IP, prefix length
- Host uses to discover
	- Own IP
	- Local DNS server IP
	- Basic routing info (gateway router IP, LAN prefix length)
- Modes
	- Dynamic: Pool of addresses, handed out by demand, renewed periodically
	- Automatic: DHCP reservation, permanently assigned to client
	- Manual: Address selected by client, who informs DHCP
- DHCP server maintains all info (IP pool, netmask, DNS servers)

Phases
1. Broadcast DHCP discovery message (L2, to FFFF:FF...). DHCP server(s) responds with "offer" (proposed IP, lease time, etc.)
2. Broadcast DHCP request message, accepts one offer. Selected server responds with ACK

Stateless DHCP (IPv6): Use ethernet for lower portion, then learn higher portion of address from router

## Putting it All Together

- Traceroute: Sends packets with increasing TTL to target using ICMP (L3) packet (debugging). Will receive ping timeout response from each packet, telling how far that router is along the path to destination

## Look at Review Qs
- Lec 5
- Lec 6 slide 10 (DBD?)
- Lec 7 (192.168.1.128?)
- Lec 8
- Lec 9
- Lec 10
	
**read 3.3, 4.1**
- look at path vector order prac exam <<<<
## Questions
- For NATs why do we need L4 demux key for priv addresses? Aren't they alr unique in LAN?
- When/why is iBGP used within an AS vs RIP/DV
- Spanning tree vs RIP/DV
- In practice test, why does router have 2 mac addresses