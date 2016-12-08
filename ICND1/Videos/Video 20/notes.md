# Video 20 Notes

## Practical Routing - Enhancing VLANs
- **Concept - Moving Data Between VLANs**
  - VLANs are a layer 2 feature
  - Hosts on separate VLANs cannot speak directly
    - Must pass through a layer 3 assistant


- **Routing Option 1: Individual Interfaces**
  - Router uses a FastEthernet ports for each VLAN
  - Each port connects to a separate VLAN on the switch
  - All router's FastEthernet ports gets an IP on each VLAN


- **Routing Option 2: Using Sub-Interfaces**
  - Router uses a single Trunk port
  - Router connects trunk port to switch
    - Set the switch's switchport to trunk mode
      - ```CBTSwitch(config)# interface fastEthernet 0/0```
      - ```CBTSwitch(config-if)# switchport trunk encapsulation dot1q```
      - ```CBTSwitch(config-if)# switchport mode trunk```
    - To limit which VLANs can communicate over the trunk port:
      - ```CBTSwitch(config-if)# switchport mode trunk allowed vlan 10```
    - To view information on trunking interfaces:
      - ```CBTSwitch# show interfaces trunk```
  - The router's will use sub-interfaces
    - With sub-interfaces, the real interface doesn't need an IP address
      - ```CBTRouter(config)# interface fastEthernet```
      - ```CBTRouter(config-if)# no ip address```
    - To create and configure a sub-interface for VLAN 10:
      - ```CBTRouter(config)# interface fastEthernet 0/0.10```
      - ```CBTRouter(config-subif)# encapsulation dot1Q 10```
      - ```CBTRouter(config-subif)# ip address 10.1.10.1 255.255.255.0```


- **Routing Option 3: Layer 3 Switching**
  - No external router required if switch supports layer 3
  - Assign a virtual interface to each VLAN and configure it
    - ```CBTSwitch(config)# interface vlan 10```
    - ```CBTSwitch(config-if)# ip address 10.1.10.1 255.255.255.0```


---
 
[Back to main](https://github.com/rot0xd/CBTNuggets/blob/master/CCNA/ICND-1/README.md)

