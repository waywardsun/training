# Video 35 Notes

## IPv6 Configuration
- **Assigning IPv6 Addresses To Your Router**
  - Assign addresses
    - IPv6 turned off by default. To turn it on:
      - ```R1(config)# ipv6 unicast-routing```
    - Assign address
      - ```R1(config)# interface fastEthernet 0/0```
      - ```R1(config-if)# ipv6 address 2001:55::1/64```
      - ```R1(config-if)# no shutdown```
  - To view IPv6 configuration
    - ```R1# show ipv6 interface brief```


- **Routing IPv6 - Static and OSPFv3**
  - Static Routing
    - ```R1(config)# ipv6 route 2001:56::/64 2001:210:10:1::2```
  - OSFPv Routing
    - ```R1(config)# ipv6 router ospf 1```
    - ```R1(config)# router-id 1.1.1.1```
    - ```R1(config)# interface fastEthernet 0/0```
    - ```R1(config-if)# ipv6 ospf 1 0```
    - ```R1(config-if)# ```
  - To view IPv6 routes
    - ```R1# show ipv6 route```
  - To view running IPv6 routing protocols
    - ```R1# show ipv6 protocols```
  - To view OSPF neighbors:
    - ```R1# show ipv6 ospf neighbor```

- **IPv4 to IPv6 Migration Strategies**
  - Multiple methods exist to provide a smooth, non-pressured transistion
    - Dual-Stack routers
      - Cisco Recommended Method
      - Simply assign an IPv4 address and IPv6 address to same interface 
    - Tunneling (6to4 and 4to6)
      - Route IPv6 traffic through IPv4-only networks
      - Route IPv4 traffic through IPv6-only networks
    - NAT Protocol Translation (NAT-PT)
      - Take IPv6 addresses and NAT them to IPv4 addresses


---
 
[Back to main](https://github.com/rot0xd/CBTNuggets/blob/master/CCNA/ICND-1/README.md)

