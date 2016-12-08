# Video 10 Notes

## Working with Cisco IOS
- **What is Cisco IOS**
  - Cisco Internetwork Operating System
  - Command-Line method of configuring a Cisco device
  - Consistent across nearly all Cisco devices
  - More powerful than a GUI

- **Help Features in Cisco IOS**
  - Hit ```?``` anywhere in IOS to list available commands.
  - Type ```?``` after a command to get help on that command
    - Example: ```ping ?```
  - Hit tab to autocomplete the current types characters

- **Cisco IOS Modes**
  - User Mode
    - Default mode after login
    - ```Switch>```
    - Limited Mode
  - Privileged Mode
    - Access through ```enable``` command from user mode
    - ```Switch#```
    - Full access to all devices functionality
    - Unable to change much on device
  - Global Configuration Mode
    - Access through ```configure terminal``` from privileged mode
    - ```Switch(config)#```
    - Allows you to modify the configuration on the device
    - From here you can move to sub-configuration modes
  - To go back up a mode, hit ```ctrl + z``` or type ```end```
  - To go back from privileged to user mode, type ```disable```
  
---
 
[Back to main](https://github.com/rot0xd/CBTNuggets/blob/master/CCNA/ICND-1/README.md)

