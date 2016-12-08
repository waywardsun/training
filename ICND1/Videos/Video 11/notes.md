# Video 11 Notes

## Base Configuration - Part 1
- **Understanding the Physical Connections**
  - Computer NIC to wall jack
  - Wall jack to a patch panel
  - Patch panel to switch


## Base Switch IOS Configuration
  - Configuration Checklist
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
      - ```enable``` -> ```conf t```
    - Configure the hostname
      - ```hostname NEW_HOSTNAME```


## Negating Commands
  - Purpose: To remove configuration entered into the device.
  - Steps
    - Enter a command that we want to undo
      - ```hostname BadHostname```
    - Undo the command by negating it
      - ```no hostname```


## Console Password
  - Purpose: To require a password to access the device over the console port
  - Steps
    - Enter general configuration mode
      - ```enable``` -> ```conf t```
    - Enter console configuration mode
      - ```line console 0```
    - Create a password
      - ```password NEW_PASSWORD```
    - Require login for the console
      - ```login```


## Telnet Password
  - Purpose: To require a password to access the device remotely over telnet
  - Steps
    - Enter general configuration mode
      - ```enable``` -> ```conf t```
    - Enter vty configuration mode
      - ```line vty 0 15```
    - Create a password
      - ```password NEW_PASSWORD```
    - Require login for vty access
      - ```login```


## Enable Password
  - Purpose: To require a password when entering privileged mode
  - Steps
    - Enter general configuration mode
      - ```enable``` -> ```conf t```
    - Create a secret password
      - ```enable secret NEW_PASSWORD```

---
 
[Back to main](https://github.com/rot0xd/CBTNuggets/blob/master/CCNA/ICND-1/README.md)

