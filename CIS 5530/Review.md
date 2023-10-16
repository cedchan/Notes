Types of question
- Regurgitation
- Application
- Scenarios

subnet mask?

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
- **Packet transmission time:** Time it takes for sender to transmit all bits
- **Throughput:** Total number of bits transmitted over length of time
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
- Wireless
- Repeaters
- Hubs: Multi-port receivers
- Issues: Doesn't support multiple technologies, data sent everywhere

Layer 2
- Medium Access Control (MAC) address: Globally unique address
	- Blocks assigned to vendors, adapters assigned by vendors to devices
	- Broadcast Address FF:FF:FF:FF:FF:FF
	- Promiscuous mode reads all, not just intended messages
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
- Spanning tree to avoid
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

NATs
- Convert private IP to public (from outside, looks like all going to different ports of same device)
- Use L4 demux key to distinguish on both sides
- Advantages: Control over many hosts, rapid deployment path
- Disads: Breaks connectivity, relies on specific L4 protocol, breaks e2e principle

## Intradomain Routing
- Doing better than spanning tree: Shortest path from each
- Shortest paths form a sink tree
- Forwarding = L2, through learning, maps MAC to port; routing = L3, through routing protocol, maps IP to next hop IP

DV
- Routing Information Protocol (RIP) based on Bellman-Ford
- Maintain distance vector to all destinations, periodically broadcast
- Good news fast, bad news slow
- Poisoned reverse (on loops <4)
- Limited Infinity (e.g., 16 hops)
- Minimal overhead, but slow convergence

LS
- Open Shortest Path First (OSPF) based on Dijkstra
- Each node maintains graph topology by flooding info about neighbors through graph
- Challenges: loops, packet loss, out-of-order arrival
- Solutions: Sequence numbers, acknowledgments, TTL
- High overhead, fast convergence

## Look at Review Qs
- Lec 5
- Lec 6 slide 10 (DBD?)
- Lec 7 (192.168.1.128?)

## Questions
- For NATs why do we need L4 demux key for priv addresses? Aren't they alr unique in LAN?