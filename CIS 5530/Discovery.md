## Our View of the Internet (So Far)

$$\text{Devices}\rightarrow\text{Switch}\rightarrow\text{Routers ... }\rightarrow\text{Border Router}$$
1 AS
1 L3 network
Each connection between things is an L1 network (transmitting bits)

L2: Network with endpoints, connected by switches

Any device above layer 2 will have to decapsulate layer 2 (e.g., decapsulate WiFi and ethernet so they can work together in a router)

Any time you see a router, everything on either side will be a different layer 2 network.
## Why Discovery

We have **host names** (e.g., URL) that are understood by humans, **IP addresses** understood by routers, and **MAC addresses** understood by adapters.

## DNS

The **Domain Name System (DNS)** at a basic level translates between host-addresses and human-readable names.

### History

The precursor to DNS was the `hosts.txt` file, located in `/etc/hosts` that map hosts to addresses. Originally, it was maintained by the Stanford Research Institute (SRI), where people had to submit changes by email. 

Eventually, the volume of changes were too much to handle (both in terms of receiving requests and having many people download). Additional issues arose with conflicts between names.

DNS was invented to fix this.

### Key Idea: Hierarchy

#### Hierarchical Namespace

There are "namespaces" in URLs. **Top-level domains (TLDs)** include things like .edu, .com, .gov, .org, etc. From these namespaces, you could create subdomains. These are represented as trees, where the "name" is the leaf to root path. Because they're trees, we can avoid collisions. 

#### Hierarchical Administration

At each level, there's a **zone** that's managed by a central administrative authority.

#### Hierarchical Servers

The top of the hierarchy has **root servers**, whose locations are hardwired in. There are 13 root servers for all TLDs, labeled A-N. 

Root servers are replicated via **anycast** throughout the world. This works because even though there are 13 addresses that are being replicated in thousands of places, we'll just take the closest one. 

In short, routing finds the shortest path to destination, using the closest location for each address. The drawback is that anycast is fragile. For example, if a link goes down, you might, without knowing it, go to a completely different server with the same address.

### Name Resolution

There are two ways to get names from the root servers.
#### Iterative
There are local DNS servers that are hosted typically by ISPs or organizations (e.g., Penn has its own). These local DNS servers then communicate with the root server, and follow the path all the way until it gets the IP address you want.

![](Pasted%20image%2020231009162248.png)

The benefit of having a local DNS server instead of communicating directly, this makes things faster for both users and the server. The server can tell that it's getting many requests for something like .com, so we can **cache** this information and use it later.

#### Recursive
The other solution is to implement this recursively. In this solution, instead of each server passing the "next hop" information back to the asker, the servers will ask on behalf of the asker.
![](Pasted%20image%2020231009163203.png)
In practice, this isn't used much in practice because of excess overhead that has to be spent on the root servers.

It also allows **reflection attack**. This is when you make a request with a huge payload and fake an target IP address, causing all the root servers to send this payload to the target.

### Resource Records

DNS servers have distributed database storing of **resource records (RR)**. 

RR format: (name, value, type, ttf)
- Type A
	- Name is hostname, value is IP address
- Type NS
	- Name is domain (e.g., foo.com), value is hostname of authoritative name server for this domain
- Type CNAME
	- Can see the canonical name
- Type MX
	- Value is the name of mailserver associated with name

### Caching

There are different tradeoffs for caching with different TTLs. Small TTL results in high responsivity to change, while large TTL results in higher cache hit rate. 

This means that at the top of the hierarchy, the TTLs are usually days to weeks, while at the bottom they may be seconds to hours.

#### Negative Caching

It can take a long time for a request to fail, so **negative caching** will note that particular misspellings will result in a failure.
## ARP



## DHCP