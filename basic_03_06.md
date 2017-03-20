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



