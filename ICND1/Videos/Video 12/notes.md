# Video 12 Notes

## Base Configuration - Part 2
  - Configuration Checklist (cont)
    - Encrypt passwords in config
    - Management (VLAN) IP Address
    - Default Gateway
    - Shutdown
    - Logon Banner
    - Saving Configurations


## Encrypt passwords in config
  - Purpose: Encrypt the passwords stored in the device configuration
  - Steps
    - Enter general configuration mode
      - ```enable``` -> ```conf t```
    - Enable encryption for configuration passwords
      - ```service password-encryption```


## Management (VLAN) IP Address
  - Purpose: Assign an IP address to the switch so it can be managed remotely
  - Steps
    - Enter general configuration mode
      - ```enable``` -> ```conf t```
    - Enter vlan 1 configuration mode
      - ```interface vlan 1```
    - Assign an IP address to a virtual port on the vlan
      - ```ip address 192.168.1.2 255.255.255.0```
    - Enable the vlan interface
      - ```no shutdown```
  - To see info on the vlan: ```show vlan```


## Default Gateway
  - Purpose: Assign the default gateway the switch will route traffic through
  - Steps
    - Enter general configuration mode
      - ```enable``` -> ```conf t```
    - Set the default gateway to the general configuration
      - ```ip default-gateway 192.168.1.1```
  - To see info on the default gateway: ```show ip route```


## Shutdown
  - Purpose: Disable a port
  - Steps
    - Enter general configuration mode
      - ```enable``` -> ```conf t```
    - Enter configuration for the interface being disabled
      - ```interface fastEthernet 0/1```
    - Disable the port
      - ```shutdown```


## Logon Banner
  - Purpose: Provide a message to all users logging into the server
  - Steps
    - Enter general configuration mode
      - ```enable``` -> ```conf t```
    - Configure the banner
      - ```banner motd %Unauthorized access. Prohibited!%```


## Saving Configurations
  - Purpose: Persist your running configuration across reboots
  - Steps
    - Enter general configuration mode
      - ```enable``` -> ```conf t```
    - Copy the running configuration to the startup configuration
      - ```copy running-config startup-config```


---
 
[Back to main](https://github.com/rot0xd/CBTNuggets/blob/master/CCNA/ICND-1/README.md)

