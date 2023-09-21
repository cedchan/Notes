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

Those 16 bits could actually be a different length:
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

