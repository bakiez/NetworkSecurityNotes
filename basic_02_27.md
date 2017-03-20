### Microwave antennas
These are useful because they make a very narrow beam; they have an opening
angle of about 1 degree.
However, even on a 50km distance, this makes the cone about 900 meters wide.

### Satellite communication
Often satellite communication is unencrypted, because of the immense decrease
in performance when encryption would be turned on.


# Link layer

The link layer provides:
- frames
- solving transmission errors
- does addressing using ethernet addresses
- does collision handling
- provides access control

## Addressing

Ethernet addresses look like aa:bb:cc:dd:ee:ff, where the first three
parts identify the manufacturer, and the last three are decided by the 
manufacturer.

The most important part of ethernet adresses is that it is unique.

### ARP
ARP makes sure that devices can talk to each other using a software IP address
instead of the hardware Ethernet address. ARP does this mapping.
The ARP protocal has two states:
- Arp who-has *ip address*
- Arp reply

Doing this for every packet is madness, so ARP does a number of optimizations.
- Caching the ARP entries.
- Include the MAC address in the requests, so the receiver of the question
does not also have to ask the question, because he knows the ip-ethernet 
combination of the one asking the question initially.
- Every host records this, when two neighbours communicate their information.
- Send ARPs on joining the network, so not everyone has to ask.

There is also something called *gratious ARP*. This means that a device tells
everyone 'I have ip address x and MAC address y'.

Usually this is done when:
- The interface is reconfigured.
- In failover scenarios

Imagine two devices A and B, with the same IP and different MAC addresses. When
A falls away, B will tell everyone about its IP and the (now new) MAC address
to take over the tasks of A.

