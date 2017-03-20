# Physical Layer

## Time Domain Reflectrometry
Insert a pulse into the network, and when the network should have been balanced
(in terms of impedance) no signal should come back. When an intruder is
connected, some signal will come back because the impedances are not balanced.

## Parallel cables
There can be crosstalk between cables, which can be exploited. Current flowing
in a certain direction creates a magnetic field, which creates a current in 
another cable.

#### Shielding
Methods to prevent this from happening, is to use shielding. This shielding
is a metal mesh around the cable, which should be connected to ground.

There is a notation when it comes to cabling: OO/LLTT

 - The TT part says something about the wire pairs.
 - LL says something about the shielding of each individual pair
 - The OO is the outer kind of shielding that is put in.

Talking about UTP = U/UTP -> Two pairs of wires, no shielding around the wire,
no shielding around the cable.
Talking about S/STP -> Shielding around the entire cable, and also shielding 
around each individual cable.

Read into twisting cables! Twisting cables reduces interference effects.

#### Encryption
Another method is encryption of data at the physical layer. A thourough 
investigation of *trust boundaries* should be done, to find out where data 
should be encrypted.

#### Prevent physical access
An intrudor cannot wiretap 50 buildings away, so physical access control can
reduce the chance of wiretapping and prevent an intrudor from just disconnecting
a wire. Part of physical access control are camera's, switches, etc.

## Optical Fiber 
The backbone for all global and governmental communication because it is cheap
and works very well.
If you have a normal window glass of ~1cm, only 50% of the light can go through.
Obviously, this works exponentially but the light degrades so fast that it 
cannot be used for communication. Normal window glass has a degradation of
100.000 dB/km.
Two important inventions:
 - microscopic impurities fuck up windows
 - stronger light sources.

Currently, optical fiber cables have a degradation of 0.2 dB/km.

The refractive index of a material, is `speed of light in vacuum / speed of 
light in medium`. Using the correct material combination, light can be trapped
inside a cable by Snell's law `n1 sin theta1 = n2 sin theta2`.

Optical cables consist of three parts:
 - core: glass
 - cladding: glass with something mixed in to get the correct ratio of 
 reflective indices.
 - coating: 

Bending an optical fiber usually means that some portion of the light is lost,
because some rays may have an impact angle that is larger than the maximum 
allowed one.

Because there is always some leakage, there is a method 
(patent Deutsche Telekom) that uses a mirror and photovoltaic resistor around
the cable to catch the signals going through. This method cannot be detected.


### Physical layer defense

Security:
Security threats do not just have to be wire tappers. Accidents and
natural disasters can be security threats, too.
- resilience: accidents, damage.
    - do resilience planning
    - prevent single points of failure
- wire tappers
    - physical access control (hardened carrier)
        - for a wire between two buildings, put the wire in a pressurized pipe.
        As soon as the pressure drops, stop using that wire.
        - put the cable in concrete, which is much harder to drill in than
        soft ground
    - some sort of social control (continuously monitored carrier)
        - illuminate the area and remove obstacles, so make it harder to 
        get to the cables unnoticed.
        - use video cameras
    - add an alarm (alarm carrier)
        - if something happens to the cable, take action

Depending on the kind of threat, different kinds of redundancy are needed.
Against a landslide, you can have two routes of fiber optic cables. However,
against an attacker you want a redundancy connection that is completely different
from the original connection to make it harder to target both connections.

Encryption works against wire tappers, but because of *defense in depth*:
 - Don't rely on one counter measure, but combine as many as possible. Don't 
 make an eggshell security system, but rather make a honeycomb where the 
 intrudor has to go from compartment to compartment. This slows the attacker
 down and makes intrusion significantly harder.

Even with leased lines you run over the same infrastructure as everybody else,
you just get a guaranteed bandwith, and a private frequency in the optical
cables. This means that you do not suffer from congestion users outside your
company, but you are still not running over private cables.


## Wireless communication
The higher the frequency, the more a wave behaves like light. Lower frequencies
need gigantic antennas but can carry through almost anything. Light on the other
hand is blocked by pretty much any physical object.
Therefore FM radio with a lower frequency can carry ~100km, where WiFi does
not carry further than a few meters in a building.

### Security through range limitation
Make a signal small enough so not everyone can hear.

- UHF RFID: Documented biggest range to read out information from UHF RFID is 66m in a 
university, where usually these chips are used for physical access control
at centimeters distance (open doors, etc).
- Bluetooth: should be carrying about 15 meters, that is what it is used for
normally. However currently bluetooth can be read out from more than a 
kilometer.
- WiFi 802.11b. The normal range for WiFi is about 100m as advertised, but 
has been read out at a distance of 200km.
- GSM can be read out from at least 500km (beyond the ISS).

#### Modern cars, wireless keys
Usually a car cannot hear a key from more than ~15cm. By amplifying a small
key signal from the key inside a building, the car can think the key is 
in range -> the car opens.

A method to solve this is to continuously keep asking for a signal from the 
key. When the driver is too far from the signal to be able to catch the
original signal and amplify it for the car, the car should turn off.


### Information modulation
- AM: modulate the amplitude
- FM: modulate the frequency (slow = 0, fast = 1, e.g.)
- PSK: shift the phase by 180 degrees between a zero and one.

Look at:
- Frequency hop spread spectrum
- chirping
- discrete sequence spread spectrum




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

## Switches
RAM is way too slow, that's why we have CAM, which can do lookups in constant
time. However, CAM is very expensive, so switches usually do not have space
for more than 128.000 ARPs.

ARP is ~40 bytes, at a slow connection of 10Mbit/s, you can do about 25.000 ARPs
per second, so you can fill the ARP table within six seconds.

Then when the switch gets a new packet, that address is not in the ARP table
anymore (because you filled it). Then, what to do?
- Discard the package: no data leaks, but data loss instead
- Broadcast the package: no data loss, but data leaks instead.

In case of an empty switch configuration, you cannot discard because then you
would never be able to fill the ARP table. Therefore broadcasting is the way
to go.

What to do against this attack, when it only takes a few seconds?
- Block ARP requests after a certain threshold
- Check ARP bursts

When something is not used for 5 minutes in FIB, it is deleted automatically.

### Port security
Limit the number of devices behind each port.
- Rate limits
- Mac filtering, it is very bad for access control (MAC spoofing) but works
excellently against ARP attacks.
However, doing port filtering between two switches can cause chaos because then
it is normal for there to be tens of thousands of ARP messages.
- Do classification by ports: differentiate between trunk port and access ports.
Depending on the kind of port, do different filtering.

## VLAN 802.1Q
Separates the physical infrastructure into virtually separate LANs.
A device can also be part of multiple memberships, and also when a device is not
a part of a certain membership, you can configure it such that it will also not
receive information for that membership.

Issues:
- Switch spoofing.
    - STP
    - (D)DOS (The CPU has to handle all control messages, so taking down a
    switch with control messages is fairly easy)
    - Countermeasures: limit what can come in.
- Double tagging attack: look into this at home!
    - Root problem: VLAN1 is used when there is no tag, and is also used for
    VLAN1 (if I understand it correctly..).
    - Countermeasures:
        - disallow double tagging
            - problem: When sending something over a VLAN within your network
            going from Rotterdam to Amsterdam, the ISP will add a second VLAN
            tag to separate your traffic from that of your competitor.
        - disallow non-tagged packets: configure the switches to add a tag
        'VLAN $n' when a pc on VLAN $n sends a packet without a tag.
        - disable the unused ports and move to a non-default VLAN id.
- Multiple logical VLANs are still on the same hardware. When one VLAN
misbehaves (e.g. claims all bandwidth) all VLANs notice this. There is still
physical entanglement.

## WIFI 802.11
- __Independent Basic Service Set (IBSS):__  everyone talks to everyone without a
central access point
- __Infrastructure BSS:__ every one talks to everyone through a common central
access point (Service Set IDentification)
- __Extended Service Set:__ multiple access points, such as eduroam at the TU.
These all share the same SSID

The first WIFI standard had a system callend Open System Authentication (OSA),
which is a euphemism, because there is no authentication in an open system.
They already knew that this could not compete with ethernet, because ethernet
has access control by needing a physical cable. Very soon verification was added
with the protocol Wired Equivalent Privacy (WEP).

### Problems
#### Autoconnect
__Problem:__ Example for wifi-in-de-trein: when you autoconnect to a certain SSID, an
attacker can broadcast with that SSID. The only thing he has to do to make
you connect to him instead of the real wifi-in-de-trein is to broadcast a
stronger signal. Which obviously is trivial.

__Solutions:__ Rogue access point detection by checking if there are multiple
access points with the same SSID. But what to do when you find one?
- Find out where they are before taking out the torches and the pitch forks.
- Increase own signal power, and try to win this somehow
- Third one is apparently most important, did not understand, see book. Is about
reacting and making sure no further compromises are taking place. See
the MARRIOT TO PAY 600.000 TO RESOLVE WIFI-BLOCKING INVESTIGATION, because
apparently this is the technique.

#### Authentication
As an attacker, you can go through all IP-addresses and try to connect
to the access point. At some point, all IP-addresses have been taken and nothing
can connect anymore.
In case of a C-class network, this is around ~250 'devices'.

In the association phase, the client is given an "association ID", which is
an integer number between 0 and 2007. That means that no access point that
implements the 802.11 standard can handle more than 2007 devices.

This memory can be freed either after a certain timeout, or in case of a 
de-authentication.

Clearly, a Denial Of Service attack is for consumer hardware very easily doable.

#### Hiding the access point
Preventing the access point from beaconing may make the network "invisible".
However, as soon as someone connects to it, data is flowing and this data is 
very easily discovered. Therefore, the only way to hide a wireless network is 
by not using it, and hiding the access point is a pretty poor way to hide the
network.

In order to connect to one of these, the client has to go through all networks
in his memory, which means that now there is a privacy leakage: the clients
will broadcast about each of the networks it knows about.

### WEP
More than 40 bits of encryption was deemed 'too strong' according to the laws at
the time the protocol was created.
Solution: use a 64 bits key, of which 24 are public, leaving 40 private bits. 

On page 33: the same handshake can be replayed.

number of IV: 2^24 > 16 million possibilites, so after at most 16M packets, the
same IV has to be reused.
__Go through them one by one:__ Problem: extra effort, have to remember state,
and when going down, the AP will start at 0 again. An attack can purposely
get the AP down to force it to go to 0, and use that without even having to
wait for the IV the attacker knows about.

Randomised also doesn't help. This maps directly to the birthday problem: the
more IV's the attacker knows about, the higher the probability that one of
the IVs the AP uses is one he knows about.

### CRC
As an attacker, you know the cypher C, but not the message M or the key K.
If the attacker wants to change one of your packets:
`M' = T XOR M`

`C' = (M' || CRC(M')) XOR RC4(IV||K) = (T XOR M) || crc(M XOR T)`

`(T || CRC(T)) XOR (M || CRC(M))` 

` = C XOR (T || CRC(T))`

Here, the message could be changed without knowing the encryption key, 
and without breaking the CRC.

### WPA
Wifi Protected Access (802.11i) was meant as an intermediate fix, but was 
still WEP at the core. The final standard came out in 2004 with WPA2, defined
in 802.11w, where the w says something about the number of fixes that were 
needed.

Conceptual problems in WEP:
- small keystream
- very weak encryption
- the challenge response can be replayed to gain access
- integrity control (crc) is linear

and WPA did try to cover these problems.
WPA uses nonces, which are numbers that are not (or rarely) repeated.

WPA does not use a shared key for everyone, but a private key that is taken
from the different nonces, and is thus unique for everyone. Also part of this
secret is put in the integrity control, so no-one without the secret can
change the information.

Read into TKIP!

After the WEP handshake, the WPA handshake takes place. Everything before
the WPA handshake cannot be protected by using the WPA key as verification and
protection against a rogue access point.
A PKI, with certificates, could have protected against this. The drawback is that
you have to pre-configure the network which is not nice from a user perspective.

## Mobile telephony networks

Mobile telephony network evolution:
- 0 G: MTS1946, it seems. There were 12 channels, so e.g. in NYC, 12 people could
make a phone call simultaneously. The tower antenna range was ~100km, so 
frequency bands could barely be re-used
- 1 G: AMPS, in 1983. Nothing much done about security. For example, your 
credentials would be sent out in the open, unencrypted. Solution at the time:
each hardware chip was a little bit different ('puffs' or so?), so the signal 
would show the originating device.

In Germany:
- A-net, 1958
- B-net, 1972
- C-net, 1985

In the UK:
- sys-1, 1959
- ..
- sys-4, 1983

This was pretty useless, because countries now could not communicate.
They wanted to have something that was interoperable between Europe 
Therefore, 2G was created (Global System for Mobile Communication, GSM). 

- 2G: GSM. The telecom operators were all government owned so the operators 
trusted each other. Several standards: A5/0, A5/1, A5/2, LFSR. Of these, A5/2 
was deliberately weakened, and given to parties that were not trusted so it 
could easily be broken. It was designed such that the access point decides 
the handshake and the phone has to comply (assumption: phones should be dumb,
and this is easier to implement in hardware)

### GSM

The system consisted of two subsystems: Base Station Subsystem (BSS) and
Network Subsystem. The two are connected by a Mobile Switching Center.
A mobile phone would connect to a Base Transceiver Station, which sends data 
to a Base Station Controller, which sends data to a Mobile Switching Center,
which sends the data to the Network Subsystem.

The Home Location Register stores the contract details, your location, 
your phone number, etc. This information is used to route data to the correct
user, and keep track of how much the user should pay.

GSM handshake variables:
- IMSI: identity number that is tied to the SIM card. Should have been private
because it can be used for tracking (not impersonating because you also need
the key). However, it is broadcasted in broad daylight, but 'to make it not too
bad' it is only sent once.
- RAND: random number
- SRES: encrypted version of the random number if you would have had the key
- Kc: Session key

Using these variables, the actual key does not have to be out of the
SIM card/ Authentication center, ever. However, there is privacy leakage by
leaking the the IMSI. Also, the phone has to prove its identity to the network,
but the network does not have to authenticate to the phone. The reason is that
phones were supposed to be dumb and simple. To make it worse, phone autoconnect
to the strongest signal.

# Network Layer

## Network design
The simplest way of making a network is simply having one switch, and 
connecting everyone to that one switch. However, the drawback is that there
is a single-point-of-failure. To prevent this, one also could make a 
complete graph of connections. The drawback here is that it is extremely 
expensive and it is not scalable at all.
A third method is a ring, where you can survive one failure but a second
failure will disconnect hosts from each other. Also, messages would need to 
travel an extremely long way, especially when one failure has occurred (if there
is one circle with a break between Utrecht and Den Haag, any traffic from Utrect
to Den Haag has to the other way over the ring, over the whole world).

Usually, networks are divided into three parts:
- Core: you're going to optimize everything for extremely fast traffic 
forwarding. The core is about getting packets from any point to any point as 
fast as possible. This part is often close to a full graph.
- Distribution: In the distribution network you care about providing access to
whatever is beneath you. This is also where you look into security solutions.
- Access: is usually not placed out redundantly. Devices that should be redundant
are often connected directly to the distribution layer.

### Security-driven network design
'Entities' that will connect to the network:
- employees
    - System operations (admins), fairly large priviliges
    - management
    - engineers
    - auditors / legal
    - human resources
    - sales
- guests
- uplinks
- remote locations / VPN
- servers    
    - internal services
        - mail
        - databases
    - authentication
    - websites / external services
Part should be segmented: when a flat hierarchy (everybody has access to 
everything) is hacked, the attacker has access to _everything_.

A first part is to determine who is trusted. Being trusted means that it 
is business critical, and should be covered in layers and layers of security.
- sysops have a lot of priviliges and thus should be protected.
- management: should often not have access to most things, but 'CEO fraud' 
is a real thing.
- engineers. have access to the core, so need to be secured well
- uplinks. Should have no priviliges whatsoever
- remote locations. Even though we trust the other part of the company in city X,
depending on how the data travels we might not trust this at all.
- employees (bring your own device?). Use these devices to interface with the
mail server?

Page 8: 
Prevent CEO fraud for example by letting the Antivirus know that any internal
mail address can never come from the outside.

### Reconnaissance
1. Search for some web presence. Do they have a website, what's on the website?
    - job openings: tell you what kind of systems they're running
    - employees, and sometimes entire organigrams.
2. Search for business relationships, look at the websites of vendor (proud 
customers are..)
3. Call them, get public IP, Google Maps/Streetview.
4. Look at social media (Facebook, LinkedIn)
5. Look for mailings lists, forum posts, bug reports (posted from 
bob@company.com, I have a setup of [...] and my problem is [...])
6. Googling: `password filetype:log`, `id_rsa`

## IP

The ethernet layer does not accept more than 1500 bytes a packet, so IP packets
may have to be split up (slide 32 lecture 6).
Border cases:
- buffer memory echaustion
- fragment overlap
- packets can be reordered
- incomplete assembly
- two streams can interfere (packets from one stream being put on the other 
stream, comes down to a combo of fragment overlap and incomplete assembly)
- about IP header offset: 2^16 = 65536. With 13 bits offset: 
`8192*1480/8 = 65536`. And after that number you can add data. This can allow
buffer overflows, allowing you to write to parts of memory with Operating 
System authority. This is precisely the idea behind the Ping of Death.
- teardrop attack

## DNS
DNS maps logical names to IP addresses, and reverse DNS does the reverse.
There is a separate TTL in the DNS packet, which tells the DNS server for how
long it can cache this data.

What can go wrong in terms of Confidentiality, Integrity and Availability?

**Confidentiality**: 
- Sniff questions and answers
- traffic analysis

**Integrity**: 
- answers may not be legitimate: intercept queries and give a false response.
(pharming)
- NXDomain (Non-eXisting Domain) hijacking, where if you make a typo in a 
domain name, you end up on a website that said 'did you mean [..] and here
are ten advertisements'


**Availability**: 
- flooding the cache pool by sending a lot of DNS packets to the server.
- amplification attacks
- worker exhaustion
