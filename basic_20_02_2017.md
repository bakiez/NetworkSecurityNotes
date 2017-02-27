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


