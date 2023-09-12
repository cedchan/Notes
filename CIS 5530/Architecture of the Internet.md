## Protocols

>[!definition]
>**Protocols** are agreements between parties on how to communicate. They define the **syntax** of communication—like where pauses go, grammar, etc.—as well as the **semantics** of communication—like starting with a greeting.

In networking, protocols exist on both hardware and software levels for purposes from data transfer to routing control. Typically, they're defined by standard bodies like the IETF.

## Networks

>[!definition]
>**Broadcast networks** hare a common channel where everyone can hear one another.
>
>**Switched networks** transmit information through a small subset of the nodes (typically one).

### Circuit Switching

There are three phases:
1. Circuit establishment (from source to destination)
2. Data transfer
3. Circuit termination

Most circuit switch networks have a "busy signal"

### Packet Switching

Packets are sent individually. No resources are pre-allocated.

Advantages:
- No connection state required
- Easy to recover from errors
- Minimal network assumptions

Disadvantages:
- No guarantees
- Slower when transmitting a lot of data

## Founding of the Internet

Goal was to have an **inter-network**—that is, a network of existing networks. There were two main goals:
- **Multiplexing** (sharing): Shared use of a single communications channel
- **Existing networks** (interconnection)

Packet switching was chosen because it's more general and worked on top of existing networks, as well as provided slightly better multiplexin.