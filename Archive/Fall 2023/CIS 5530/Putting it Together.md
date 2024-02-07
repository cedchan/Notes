
## Traceroute

This is a debugging utility that helps find what path a layer 3 packet is taking. There's a protocol called ICMP that encompasses all debugging (e.g., pings are ICMP packets). There's a helpful functionality in the ping packet: if the TTL expires, routers will try to tell you about it. Traceroute sends out packets with increasing TTL values. On this bounce back, you get info about the routers along path to any router.