# Video 28 Notes

## Routing Protocols and OSPF (Continued)
- **How to get OSPF working**
  - OSPF: Lets our routers talk about what they think is most interesting
  - OSPF uses 'HELLO' packets
    - Contains timers, area, authentication, subnet mask
      - Timers: Tells how often packets will come and dead timer
        - Timers must match between routers or else no relationship formed
      - Area: Allows you to break networks up into groups of networks
        - Areas represent a point of summarization
        - Allow you to summarize multiple small networks in one larger network
          - Example:
            - Networks: 10.1.0.0/24, 10.1.1.0/24,...., 10.1.255.0
            - Can be sent as area: 10.1.0.0/16
            - Areas have to match or else no relationship formed
      - Authentication: 
        - Allows for verification of router's identity
        - Keys must match or else no relationship formed 
      - Subnet Mask: 
        - Subnet mask must match or else no relationship formed 

- **OSPF Configuration**
  - View the current routing table: 
    - ```CBTRouter# show ip route```
  - Turn on OSPF
    - ```CBTRouter(config)# router ospf 1```
      - Creates OSPF process with PID of 1
      - Just use 1 as the PID
  - Configure OSPF interfaces
    - ```CBTRouter(config-router)# network 192.168.2.0 0.0.0.255 0 ```
      - Advertises all networks that start with 192.168.2.X in area 0
      - ```network``` command has two purposes
        - ```network X.X.X.X Y.Y.Y.Y Z```
          - ```X.X.X.X``` - Identifies what interface to send 'HELLO' packets on
          - ```X.X.X.X``` - Identifies what networks to advertise
          - ```Y.Y.Y.Y``` - Wildcard bits. Opposite of subnet mask
            - Example: ```255.255.255.0``` Mask has Wildcard ```0.0.0.255```
          - ```Z``` - Area. Identifies the area the network is in
      - To turn on OSPF on every interface on the router
        - ```CBTRouter(config-router)# network 0.0.0.0 255.255.255.255 0```
    - Cisco best practice:
      - ```CBTRouter(config-router)# network 192.168.1.1 0.0.0.0 0 ```
        - Advertise only the exact network for each interface
  - Enable passive interface mode
    - ```CBTRouter(config-router)# passive-interface default```
      - Set all interfaces to be passive interfaces
      - Passive interface mode causes the interface to not send HELLO packets
    - ```CBTRouter(config-router)# no passive-interface fastEthernet 0/0```
      - Set only fastEthernet 0/0 to not be in passive-interface mode.
  - View the current OSPF neighbors: 
    - ```CBTRouter# show ip ospf neighbor```
  - View the current running routing protocols: 
    - ```CBTRouter# show ip protocols```
  - View the details of the OSPF configuration on an interface
    - ```CBTRouter# show ip ospf interface fastEthernet 0/0```


---
 
[Back to main](https://github.com/rot0xd/CBTNuggets/blob/master/CCNA/ICND-1/README.md)

