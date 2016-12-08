# Video 14 Notes

## Managing Port Security
- **Port Security - What Is It?**
  - How to manage what devices are attached to the network.
  - Allow you to restrict connections to the LAN in 2 ways:
    - Number of MAC Addresses per port
    - What MAC Address is on a port
  - Can react in shutdown, protect, restrict modes
    - ```shutdown``` - Disables port by putting in ERR-DISABLE state
    - ```protect``` - Ignore offending devices and you never know about it
    - ```restrict``` - Ignore offending devices and notify syslog
  - View port-security violations
    - ```Switch# show port-security```


- **Limiting the Number of Devices on a Port and allowed MAC Addresses**
  - Set port to be an access port
    - ```Switch(config-if)# switchport mode access```
  - Allow a maximumum of 1 MAC address on a port at a time
    - ```Switch(config-if)# switchport port-security maximum 1```
  - Set the violation mode to shutdown mode
    - ```Switch(config-if)# switchport port-security violation shutdown```
  - Configure the allowed MAC addresses
    - Manually set the MAC Address to be allowed to access the port
      - ```Switch(config-if)# switchport port-security mac-address 0000.0000.0000```
    - Set whatever MAC address currently connected to be the only one allowed
      - ```Switch(config-if)# switchport port-security mac-address sticky```
  - Turn on port security
    - ```Switch(config-if)# switchport port-security```


---
 
[Back to main](https://github.com/rot0xd/CBTNuggets/blob/master/CCNA/ICND-1/README.md)

