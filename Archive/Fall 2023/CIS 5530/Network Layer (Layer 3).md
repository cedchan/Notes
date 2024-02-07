The goal of the network layer—i.e., the **internet**—is end-to-end data delivery between hosts on an internetwork. 

- Name of protocol: IP
- Name of message: Packet
- Name of device: Router

They connect different layer 2 systems, like ethernet and WiFi.
## Structure of Layer 3

Layer 3 also uses a routing table, but it's a bit different from the ones in [layer 2](Components%20of%20a%20Network.md#Devices#Link%20Layer%20Bridge). The "next hop" in the table is the router (or local, if it's the same LAN). 

![](Pasted%20image%2020230920163234.png)

## Internet Protocol (IP)

IP is an addressing scheme to identify all hosts. It has hierarchical, not flat addresses—32 bits for IPv4, and 64 for IPv6.

It's a "best effort" service, so it may have loss, duplication, and other errors. Routers forward packets with pre-computed routes.

### IPv4 Packet, Pre-1994

![](Pasted%20image%2020230920163456.png)

- HLen: Header length (can actually be configured)
- TTL (Time to live): Prevents loops by limiting how many times packet can go through the internet

IPv4 uses **location-dependent addressing**. Rather than have unique addresses designated at creation, addresses are assigned based on location.

**Problem:** $2^{32}$ is a lot of table entries.

**Solution:** Routing based on network and host. The first 16 bits are the network, and the last 16 are the host. For example, all devices at Penn have one of 3 16-bit network addresses. 

![](Pasted%20image%2020230920164126.png)

Those 16 bits could actually be a different length, in a system called **classful addressing**:
![](Pasted%20image%2020230920164319.png)

The first few bits (the red) indicate which class it is. 

#### Private IP Addresses

There are special **private IP addresses** that are reserved to be used freely within a private network (home, small company, etc.)
- 10.0.0.0–10.255.255.255
- 192.168.0.0–192.168.255.255

#### Allocating Public IP Addresses

There's a large nonprofit, IANA that hierarchically assigns IP ranges. IANA delegates to regional bodies (**RIRs)**, which then delegate to companies in their regions, who assign IPs to users.

### Post-1994

### Problems with Old System

The differences between classes, though, were too huge (exponential). There were also problems with fairness. MIT got a class A, Penn got a class B, and yet some whole countries had less than class C IP addresses.

### Classless Interdomain Routing (CIDR)

The solution to the problems of the classful addressing system was to assign arbitrary bit boundaries.

Convention: `/` indicates that we're taking that many bits as the network ID. For example, 128.23.9.0/26 means the first 26 bits are the network ID. This leaves 6 bits, or $2^6=64$ addresses.

That is, more specific prefixes, or longer prefixes, mean fewer addresses. Less specific prefixes, or shorter prefixes, mean more addresses.

![](Pasted%20image%2020230925154404.png)
We can also aggregate different networks into **supernets** (e.g., for all of AT&T's customers), although this isn't done for security.

#### Forwarding: Longest Prefix Match

Entries in forwarding tables can have overlap, just by the `/` convention's syntax. The solution was to create a new system called **longest prefix match**, which finds the longest matching prefix (a.k.a. the most specific route) among all prefixes that match the destination address.

One of the benefits of longest prefix matching is being able to provide default behaviors with less specific prefixes. For example, for a local network we can have this routing table:

|Address|Next Hop|
|-|-|
|192.168.0.0|Local|
|0.0.0.0|Comcast|

0.0.0.0 matches everything, and 192.168.0.0 overlaps with it. 

## IPv6

The biggest change of IPv6 is the larger address space. It uses 128 bits instead of 32 bits. 

Format:
- 8 groups of 4 hex digits (16 bits)
- Omit leading zeros
- Groups of zeros can be replaced with double colons

### Transition from IPv4 to IPv6

Not all routers can be upgraded simultaneously (there's no "flag day"). This creates a problem with networks that must operate with mixed IPv4 and IPv6 routers.

One solution is **tunneling**, where IPv6 datagrams are carried as payloads in IPv4 datagrams among IPv4 routers. That is, 2 endpoints that want to use IPv6 can communicate ahead of time to do so, then every time we get to an IPv4 router, we wrap the message in an IPv4 header. 

### NAT: Network Address Translation

To the outside world, it looks like every packet is coming from a single IP (e.g., with many ports). The L4 demultiplexing ID distinguishes the devices. It translates the private address to a public address.

Advantages:
- Rapid deployment path when there is no other option
- Control over many hosts

Disadvantages:
- Breaks connectivity (can't connect to any machine)
- Breaks layering (tied to a specific L4 protocol)
- Breaks end-to-end principle (leads to loss/delays)

## Questions
1. Subnet mask???
2. Look up NAT
3. Demux key