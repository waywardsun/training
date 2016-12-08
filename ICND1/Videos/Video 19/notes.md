# Video 19 Notes

## Understanding Routing Core
- **What is Routing?**
  - The process of moving packets between IP-based networks
  - Facilitated by a Cisco router
  - IOS-powered, CEF-enhanced
    - CEF - Cisco Express Forwarding
      - Hardware that attempts to implement routing functionality

- **Understanding the Look and Feel of Cisco Routers**
  - Typically have 2 ethernet interfaces
  - Can add functionality through modules


- **Basic Router Configuration... Review**
  - Checklist
    - Hostname
    - Negating Commands
    - Console Password
    - Telnet Password
    - Enable Password
    - Encrypt passwords in config
    - Management (VLAN) IP Address
    - Default Gateway
    - Shutdown
    - Logon Banner
    - Saving Configurations


## Hostname
  - Purpose: Set the name of the device on the network
  - Steps
    - Enter general configuration mode
      - ```Router# conf t```
    - Configure the hostname
      - ```Router# hostname CBTRouter```


## Negating Commands
  - Purpose: To remove configuration entered into the device.
  - Steps
    - Enter a command that we want to undo
      - ```CBTRouter# hostname BadHostname```
    - Undo the command by negating it
      - ```CBTRouter# no hostname```


## Console Password
  - Purpose: To require a password to access the device over the console port
  - Steps
    - Enter general configuration mode
      - ```CBTRouter# conf t```
    - Enter console configuration mode
      - ```CBTRouter(config)# line console 0```
    - Create a password
      - ```CBTRouter(config-line)# password NEW_PASSWORD```
    - Require login for the console
      - ```CBTRouter(config-line)# login```


## Telnet Password
  - Purpose: To require a password to access the device remotely over telnet
  - Steps
    - Enter general configuration mode
      - ```CBTRouter# conf t```
    - Enter vty configuration mode
      - ```CBTRouter(config)# line vty 0 15```
    - Create a password
      - ```CBTRouter(config-line)# password NEW_PASSWORD```
    - Require login for vty access
      - ```CBTRouter(config-line)# login```


## Enable Password
  - Purpose: To require a password when entering privileged mode
  - Steps
    - Enter general configuration mode
      - ```CBTRouter# conf t```
    - Create a secret password
      - ```CBTRouter(config)# enable secret NEW_PASSWORD```


## Encrypt passwords in config
  - Purpose: Encrypt the passwords stored in the device configuration
  - Steps
    - Enter general configuration mode
      - ```CBTRouter# conf t```
    - Enable encryption for configuration passwords
      - ```CBTRouter(config)# service password-encryption```


## IP Address
  - Purpose: Assign an IP address to the router
  - Steps
    - Enter general configuration mode
      - ```CBTRouter# conf t```
    - Enter vlan 1 configuration mode
      - ```CBTRouter(config)# interface fastEthernet 0/0```
    - Assign an IP address to the port
      - ```CBTRouter(config-if)# ip address 192.168.1.1 255.255.255.0```


## Default Gateway
  - Purpose: Assign the default gateway the router will route traffic through
  - Note: Most of the time, a router will not have a default gateway
    - Instead, we usually set static routes
    - To view static routes:
      - ```CBTRouter(config)# ```
  - Steps
    - Enter general configuration mode
      - ```CBTRouter# conf t```
    - Set the port we will send all traffic out of
      - ```CBTRouter(config)# ip route 0.0.0.0 0.0.0.0 fastEthernet 0/1```


## Shutdown
  - Purpose: Disable a port
  - Steps
    - Enter general configuration mode
      - ```CBTRouter# conf t```
    - Enter configuration for the interface being disabled
      - ```CBTRouter(config)# interface fastEthernet 0/1```
    - Disable the port
      - ```CBTRouter(config)-if# shutdown```


## Logon Banner
  - Purpose: Provide a message to all users logging into the server
  - Steps
    - Enter general configuration mode
      - ```CBTRouter# conf t```
    - Configure the banner
      - ```CBTRouter(config)# banner motd %Unauthorized access. Prohibited!%```


## Saving Configurations
  - Purpose: Persist your running configuration across reboots
  - Steps
    - Copy the running configuration to the startup configuration
      - ```CBTRouter# copy running-config startup-config```

---
 
[Back to main](https://github.com/rot0xd/CBTNuggets/blob/master/CCNA/ICND-1/README.md)

