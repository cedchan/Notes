## Layers of the Internet


### Layer 1: Physical Layer

- Connects: Transmitters and receivers
- Lower interface: Analog signals
- Upper interface: Stream of digital bits
- Name of network: Physical links
- Name of message: Bits

>**Example.** WiFi networks → receivers

### Layer 2: Data Link Layer

- Connects: Physical interfaces
	- Usually the same physical layer protocol
- Lower interface: Stream of bits
- Upper interface: Messages with payloads
- Name of network: Local Area Network (LAN)
- Unit of data: Frame (of data)

### Layer 3: Network Layer

- Connects: LANs
	- Possibly different technologies (.g, WiFi and Ethernet)
- Lower interface: A packet of data
- Upper interface: A segment of data
	- Same thing, but with an extra header
- Name of a network: Internet

>[!hint]
>Data goes analog → bits → frames → packets → segments. Frame → segment are all just arrays of data.

## Links
### Links: Ethernet

The **Ether** can be imagined as a giant wire where all the data flows. A bunch of computers, then, tap into the either with transistors. 

Originally, wires were connected using **vampire taps**.
![](Pasted%20image%2020230918155600.png)

### Links: Wires

- **Twisted**: A bunch of different wires are twisted together
![](Pasted%20image%2020230918155731.png)
- **Co-axial**: Layers of different wires
![](Pasted%20image%2020230918155741.png)
- **Optical networks**: Strands of fiber-optic glass, where lasers are sent through
![](Pasted%20image%2020230918155759.png)

### Links: Wireless

The sender radiates signal over a region. It goes in many directions, to potentially many receivers. It's a bit more difficult because it can have interference.
## Framing

### Converting Bits to Frames

An example message on the ethernet:
![](Pasted%20image%2020230918160419.png)
(CRC = checksum)

>[!definition]
>A **medium access control (MAC) address** is a numerical address used within a link. They are globally unique, and hard-coded in the adapter when it is built, with a flat name space of 48 bits.

Global uniqueness is preserved by **hierarchical allocation**. A **block** of addresses is assigned to each vendor (e.g., Dell), which then assigns a specific address from its block to each **adapter**.

FF:FF:FF:FF:FF:FF is a special **broadcast address** that is sent to all adapters.

### Adapters

Normal adapters receive frames that are sent to the local MAC address or the broadcast address.

Meanwhile, **promiscuous mode** allows an adapter to receive everything, independent of destination MAC address. It can be useful for things like packet sniffing. 

### EtherType (Demux Key)

The **demux key** is a preconfigured special value that tells us what protocal we're using.

>[!error]
>look up

### Framing Problem

How does the link layer decide where each frame begins and ends?

We'll look at two methods: byte count and byte stuffing. In practice, though, the physical layer often provides hints (e.g., if the signal on the wire goes flat, that's probably the end of a frame).

### Byte Count

The simple approach is to start off each frame with a length field that says how long that frame is going to be.

![](Pasted%20image%2020230918161305.png)

The issue with the byte count is that if even one of the lengths gets lost (e.g., through corruption or data loss), every subsequent frame gets messed up—we have a **desynchronization** error.

### Byte Stuffing

A better idea is to have a special FLAG byte that marks the start/end of a a frame.

![](Pasted%20image%2020230918161457.png)
If a FLAG byte gets lost, then two adjacent frames will be merged, which is fine because we can resynchronize on the next FLAG byte.

One complication is if the FLAG byte appears in the payload before the actual FLAG byte. To do this, we use an escape code for FLAG in the content, just like how if we want to put `"` in a string, we have to write `"\""`. 

Then, we have the following:
- Replace all FLAG with ESC FLAG
- Replace all ESC with ESC ESC

On the receiver's end, we can just delete the next thing.

### Bit Stuffing

We can also stuff at the bit level too. For example, we can let a flag be six consecutive 1's.

On transmit, after five 1s in the data, we insert a 0. On the receive side, a 0 after five 1s is deleted.

In terms of performance, bit stuffing is much more efficient. That said, having byte-level alignment is helpful given the way computers are designed, so it doesn't happen too much in practice.

## Devices

### Physical Layer: Repeaters

Signals become weaker as they travel, which creates a limit on the length of each segment of a LAN. 

**Repeaters** join two segments together. They are analog electronic devices that simply monitor electrical signals and spit out an amplified copy.

### Physical Layer: Hubs

A **hub** is like a multi-port repeater. It joins multiple segments and broadcasts traffic that arrives on every other port, but doesn't necessarily amplify the signal. 

Like repeaters, they operate on the physical layer.

### Limitations of Repeaters and Hubs

Repeaters and hubs increase the size of a network, but it remains one large shared LAN. This means that each bit is sent everywhere, limiting throughput and posing a scalability issue.

They also can't support multiple technologies because they don't support buffer or interpret frames, and can't interconnect different rates/formats. 

Lastly, maximum nodes and distances are limited.

### Link Layer: Bridge

The solution is to make connections on layer 2. A **link layer bridge** connects two or more segments at the link layer. Bridges can support simultaneous communication.

Link layer bridges are based on a forwarding table:
- Exact destination address from the frame
- Looks up destination
- Forwards frame to appropriate segment

### Link Layer: Switches

**Link layer switches** typically connect individual computers. It's essentially the same as a bridge, but connects hosts, not segments. Switches, like bridges, allow for concurrent communication.

Functionally, bridges and switches are identical.

### Bridges, Switches vs. Repeaters, Hubs

#### Advantages

Bridges and switches break networks, which help filter packets only to the necessary segments. Segments from different technologies can also be merged.

#### Disadvantages

There's a delay for processing with bridges and switches, while repeaters and hubs can almost instantly repeat a message. One way to solve this is to use **cut-through switching**, which just looks up the destination address, chooses the port, and forwards the frame (here, there isn't error detection).

#### Self-Learning Switches

>[!idea]
>- If we just act like a hub, packets will get to their destinations
>- Whenever we see a packet, we can learn something from it

Self-learning switches start off knowing nothing. When they get a frame, it gets broadcasted to all other ports, except for the source.

When a frame arrives, we inspect the source MAC address, and associate the address with the incoming interface (port). We store this mapping in the switch table. We can also use a time-to-live field to eventually forget the mapping (e.g., for if the host moves to another network).

>[!error] look it up!

Soft-state: Just an optimization