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



