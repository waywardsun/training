# Video 27 Notes

## Routing Protocols and OSPF
- **Routing Protocols: Friends Telling Friends**
  - When you boot a router, it only knows about directly connected networks
  - You can configure routes statically or with a routing protocol
  - Routing Protocols:
    - Routers find routes from neighboring router's routing tables
    - More than one route available:
      - Allows for a level of redundancy. 
      - Allows for routers to choose the fastest 
  - Can use more than one routing protocol at a time
    - This is a CCNP level topic
    - Administrative distance is used to choose metric
      - Tells which routing protocol is the best protocol
      - Each protocol is assigned a number
      - The lower the protocol number = the better the protocol
      - Better protocol has "higher believability"
      - A router with directly connected interfaces has a distance of 0
      - Static route has a distance of 1


- **The Jelly Bean Jar of Protocol Choices**
  - Many different routing protocols:
    - RIP
      - Administrative distance: 120
      - It will work, but not fast or elegant
      - Default advertising-cycle/hello-timer of once every 30 seconds
        - Repeats entire routing table every 30 seconds
        - If router not heard from after 90 seconds, it is removed from table
      - Metric for best route is hop count.
        - Example:
          - First route: 1 hop over 56k connection
          - Second route: 4 hops over Gigabit connections
          - First route is considered faster
    - IGRP
      - Administrative distance: 100
      - Cisco decided to create something better than RIP
        - Actually turned out to be worse than RIP (lol)
      - Default advertising-cycle/hello-timer of once every 90 seconds
        - Repeats entire routing table every 90 seconds
        - If router not heard from after 270 seconds, it is removed from table
      - Metric for best route is bandwidth/speed
        - Example:
          - First route: 1 hop over 56k connection
          - Second route: 4 hops over Gigabit connections
          - Second route is considered faster
      - IGRP is dead, do not worry about it
    - OSPF (Open Shortest Path First)
      - Administrative distance: 110
      - Open standard. No cost to use
      - The most popular routing protocol in the world 
      - Default advertising-cycle/hello-timer of once every 10 seconds
        - Sends keepalive every 10 seconds by default
          - Timer can change. Only advertises changes to routing tables
      - Metric for best route is the 'cost' (bandwidth / 100)
        - Example:
          - First route: 1 hop over 56k connection
          - Second route: 4 hops over Gigabit connections
          - Second route is considered faster
    - IS-IS (Intermediate System to Intermediate System)
      - OSPF Competitor
        - From days of TCP vs OSI
      - Rarely used due to obscurity but very effective 
    - EIGRP
      - Administrative distance: 90
      - Proprietary protocol
        - Made for by Cisco for Cisco equipment
      - Very easy to configure
      - All features of OSPF and more
      - Metric for best route is the bandwidth + delay + reliability + load
        - Great metric
    - BGP (Border Gateway Protocol)
      - Administrative distance: 20
      - Not fast, but very reliable and can accomplish anything
      - Used for the internet
      - Can handle hundreds and hundreds of thousands of routes
      - Has an entire certification exam on this one protocol


---
 
[Back to main](https://github.com/rot0xd/CBTNuggets/blob/master/CCNA/ICND-1/README.md)

