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




