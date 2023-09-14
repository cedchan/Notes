## Layering

>[!definition]
>**Layering** is the ability to mix and match protocols. The set of protocols in use is called a **protocol stack**. 

Protocols are horizontal—they don't really need to know about what else is going on—whereas layers are vertical and are somewhat interdependent. We call the relationship between layers **services** provided.

### OSI vs. Internet

The OSI (open systems interconnection) conceptually defines services, interfaces, and protocols. The internet, meanwhile provides a successful implementation. 

![](Pasted%20image%2020230913154621.png)

Above, we see that the presentation and session layers have been absorbed into surrounding layers. Further, the datalink and physical layers are so interconnected that they've been merged into one. Lastly, there's only one network—namely, the internet.

- Physical: Given a series of bits, how do I convert that into analog?
- Datalink: Given this way to translate bits, how do I do things like manage transfer rates?

### Encapsulation

>[!definition]
>**Encapsulation** is the mechanism for effecting protocol layering. The opposite, which is done when messages are received, is called **decapsulation**.

With each layer, existing content is simply "wrapped" with the new layer without looking at the content itself. Eventually, the message looks like an onion, with the lowest layers on the outside. 

This also makes sure that protocols only talk to each other (i.e., they look at the header to get only the relevant content.)

![](Pasted%20image%2020230913155322.png)

Sometimes, encapsulation/decapsulation also happens at intermediary devices, like a router. For example, some outer layers might be peeled off, then modified before being sent off to the final destination.

#### Modifying Inner Contents

Although we've established previously that a header is simply tacked on for a new layer, sometimes we must actually modify the inner content slightly. For example, if contents need to be encrypted or compressed, or if long messages must be segmented into smaller sections.

### Multiplexing

Problem: How do we know which protocol a packet is intended for?

This is achieved with **demultiplexing keys**. As a message is sent down a stack, the choice of what to do next is typically decided by the application. For example, your web browser probably chose to use TCP, and TCP probably chose to use IP as the third layer.

At the ethernet level, there's an **ethertype value**, which is a 16-bit value that says what the other layers are.

## Choosing Layers

Layering opens up the design question of which layer to implement different functionalities on. For example, on which layer should error-checking be implemented?

**Solution 1:** Hopy-by-hop reliaility

Use checksums, sequence number checks, internal retry mechanisms, etc. at every layer.

**Solution 2:** End-to-end reliability

Use a checksum, etc. for the whole file. Specifically, store the file with a checksum, transfer the file, read the transferred file back, compute the checksum, and send the checksum back to the originator for comparison. If there's a failure, then the entire process should be restarted. 

### The End-to-End Principle

The idea of the end-to-end principle is to implement reliability at the lowest layer possible. The justification is twofold: (1) hop-by-hop reliability is still susceptible to failure, so end-to-end checks are still required, and (2) we don't want to over-engineer the solution.

#### Exceptions to the End-to-End Principle

- Wifi: It's so flaky that not using it would fail
- Cost vs. reliability tradeoff
- Security considerations

## Performance Metrics

### Link-Level Metrics

>[!definition]
>**Link bandwidth (capacity):** Maximum rate (in bps) at which the sender can send data along the link.
>
>**Propagation delay:** Time it takes the signal to travel from source to destination.
>
>**Packet transmission time:** Time it takes the sender to transmit all bits of the packet.

### Node-Level Metrics

>[!definition]
>
>**Queuing delay:** Time the packet needs to wait before being transmitted because the queue was not empty when it arrived.
>
>**Processing time:** Time it takes a router/switch to process the packet header, manage memory, etc.

#### Queuing

The queue has $Q$ bits when a packet arrives. The packet must wait for the queue to drain before being transmitted. For example, if a Google server on one end is blasting data to your WiFi network, it must slow down when it arrives to be processed.

### Throughput

>[!definition]
>The **throughput** of a connection or link is the total number of bits successfully transmitted during some period $[t, t+T)$ divided by $T$.
>
>**Link utilization** is the (throughput) / (link capacity)

### Latency

>[!definition]
>
>The **latency** is computed using other performance metrics like bandwidth, propagation delay, and transmission time. 

### Calculating Metrics

To summarize:
- Latency = propagation + transmit + queuing delay
- Propagation = distance / speed of light
- Transmit = packet size / bandwidth
- Queuing delay = queue length / bandwidth
### Other Metrics

- **Round-trip time (RTT):** Time from sender to receiver and back
- **Jitter:** Variability in delay
- **Bandwidth-delay product:** Product of bandwidth and delay. It is the "storage" capacity of the network.

### Jitter

>[!definition]
>Informally, **jitter** is the change in latency from packet to packet.

Measuring jitter is important for delay-sensitive traffic like voice/video data in calls. Excessive jitter can cause dropouts in audio or choppy video.

Causes:
- Router: queuing delays, congestion
- Links: failures leading to alternate paths taken

#### Measuring Jitter

Jitter $=|(RxA-TxA)-(RxB-TxB)|$, where $RxC, TxC$ denote the receive and transmit time of packet $C$. That is, it's the difference in the latencies of packets $A, B$. 

>**Example.** Packet $A$ takes $15$ ms to travel the network, and Packet $B$ takes $18$ ms.
>
>Jitter $=| 15 - 8 | = 3$ ms

Jitter can also be expressed as the sum of the differences in receive and transmit times:
$$|(RxA-TxA)-(RxB-TxB)|=|(RxA-RxB)+(TxB-TxA)|$$
