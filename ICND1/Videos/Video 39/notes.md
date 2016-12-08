# Video 39 Notes

## Floating Statics, DHCP Services, and CDP
- **Understanding the Purpose and Place of Floating Static Routes**
  - "Floating Static" describes a static route with manually set administrative distance
  - Useful for backup routes, last resort paths
  - Very easy to configure
    - Normal Route: ```ip route NETWORK SUBNET_MASK GATEWAY```
    - Floating Route: ```ip route NETWORK SUBNET_MASK GATEWAY ADMIN_DISTANCE```


- **Configuring a Cisco Device as a DHCP Server or Relay Agent**
  - DHCP - Dynamic Host Configuration Protocol
  - Configuration Steps:
    - Configure IP addresses to be excluded
      - ```CBTRouter(config)# ip dhcp excluded-address 192.168.1.1 192.168.1.49```
      - ```CBTRouter(config)# ip dhcp excluded-address 192.168.1.100 192.168.1.255```
    - Configure pool of IP addresses
      - ```CBTRouter(config)# ip dhcp pool HOME_NETWORK```
      - ```CBTRouter(dhcp-config)# network 192.168.1.100 255.255.255.0```
      - ```CBTRouter(dhcp-config)# default-router 192.168.1.1```
      - ```CBTRouter(dhcp-config)# dns-server 8.8.8.8 8.8.4.4 4.4.2.2```
  - To view DHCP leases:
    - ```CBTRouter# show ip dhcp binding```
  - To view detected machines that statically assigned IP in DHCP pool range:
    - ```CBTRouter# show ip dhcp conflict```
  - IP Helper Address (AKA DHCP Relay Agent)
    - Allows a router to pass DHCP requests to a DHCP server on another network
    - Packages requests in unicast packet and send directly to DHCP server
    - To configure the remote router to forward DHCP traffic:
      - ```CBTRouter(config-if)# ip helper-address 192.168.1.1```


- **The Wonderful Cisco Discovery Protocol (CDP)**
  - Detects what Cisco devices are directly connected to you
  - Enabled by default on all Cisco devices
  - Layer 2 Protocol
    - This allows you to see devices even if no IP configured/misconfigured
  - Useful Commands
    - ```CBTRouter# show cdp neighbors```
      - Shows directly connected devices and their details
    - ```CBTRouter# show cdp entry DEVICE```
      - Show all details about a remote device
      - Identical to ```show cdp neighbors detail```
    - ```CBTRouter# show cdp interface```
      - Show the CDP configuration for each local interface
    - ```CBTRouter(config-if)# no cdp enable```
      - Disables CDP on a specified interface
    - ```CBTRouter(config)# no cdp run```
      - Disables CDP on all interfaces


---
 
[Back to main](https://github.com/rot0xd/CBTNuggets/blob/master/CCNA/ICND-1/README.md)

