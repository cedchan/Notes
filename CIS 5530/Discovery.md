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



## ARP

## DHCP