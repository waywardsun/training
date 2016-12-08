# Video 18 Notes

## Configuring Trunking, VTP, and VLANs
- **Configuring VLANs**
  - To view info about VLAN
    - ```Switch# show vlan``` or ```Switch# show vlan brief```
  - Configuring VLANs: Single Switch
    - Create VLANs
      - ```Switch(config)# vlan 20``` creates VLAN 20.
    - Name VLANs
      - ```Switch(config-vlan)# name NEW_VLAN_NAME```
    - Create/Configure VLAN interface
      - ```Switch(config)# interface vlan 20```
      - ```Switch(config-if)# ip address 10.1.50.10 255.255.255.0```
    - Assign ports to VLANs
      - ```Switch(config)# interface fa0/18```
      - ```Switch(config-if)# switchport access vlan 50```


- **Configuring Trunking**
  - Set all ports to access mode by default. 
    - ```Switch(config)# interface range fastEthernet 0/1-48```
    - ```Switch(config-if-range)# switchport mode access```
  - Configure Trunk Ports
    - ```Switch(config)# interface fastEthernet 0/1```
    - ```Switch(config-if)# switchport mode trunk```


- **Configuring VTP**
    - To view VTP status
      - ```Switch# show vtp status```
    - Enable VTP
      - ```Switch(config)# vtp domain CBTNuggets```
        - NOTE: domain is case-sensitive
    - Set VTP mode
      - ```Switch(config)# vtp mode server```
    - To view connected Cisco devices:
      - ```Switch# show cdp neighbors```


---
 
[Back to main](https://github.com/rot0xd/CBTNuggets/blob/master/CCNA/ICND-1/README.md)

