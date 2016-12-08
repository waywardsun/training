# Video 09 Notes

## The World of Switching
- **Hub, Bridges, Switches**
  - Hubs
    - Layer 1 Device. No intelligence at all.
    - Repeats an incoming packet to all other ports on the hub.
    - No matter how many ports it has, they are all on one collision domain.
    - Not used today because collision rate is very high. Very insecure.
  - Bridges
    - Layer 2 Device. Limited number of ports.
    - Learns MAC addresses and sends packet out the correct port on the device. 
    - Transition device between hubs and switches.
    - Software based. Very slow device.
    - Breaks the network into multiple collision domains.
  - Switches
    - Layer 2 or 3 Device. High number of ports. Managed and intelligent.
    - Full-Duplex, Varying port speeds
    - ASIC-based (Application Specific Integrate Circuitry)
      - Moved software based processing into hardware
    - Every port is it's own collision domain

- **Collision Domains and Broadcast Domains**
  - Collision Domain
    - How many ports can collide.
    - Collision occurs when two hosts send data at the exact same time.
  - Broadcast Domain
    - How far a broadcast packet will go before it is stopped.
    - A broadcast will make a switch like a hub and repeat to all ports.
  - Half-Duplex - Send OR receive data
    - All network speeds rated in half-duplex (10Gbps, 100Mbps, etc)
  - Full-Duplex - Send AND receive data

- **A Day in the Life of a Switch**
  - Switch Ports
    - Ethernet limited to 100 meters.
    - Fiber can travel up to miles depending on fiber used
      - Fiber port added using SFP Module (Small Form-Factor Pluggable)
      - Multi-Mode fiber cheaper, but doesn't travel as far. Plastic
      - Single-Mode fiber more expensive, travels further. Glass
  - CAM table
    - Content Accessible Memory
    - Empty when the device boots
    - Stores MAC addresses for the switch
      - All ARP requests/responses populate a switches CAM table
      - Can takes as quick as 5 to 10 seconds to fully populate from boot
      - Entries in the CAM table expire after 5 minutes by default.

---
 
[Back to main](https://github.com/rot0xd/CBTNuggets/blob/master/CCNA/ICND-1/README.md)

