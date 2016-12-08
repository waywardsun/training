# Video 08 Notes

## Configuring Cisco Devices
- **Console Connections and Rollover Cables**
  - Console Port
    - RJ-45 Jack
    - Accepts a console cable (rollover cable)
    - Console cable is RJ-45 -> 9-Pin Serial
    - Modern devices can use USB Serial adapter
  - Newer devices have USB port to access the console 
  - Access Servers
    - One device that is designated to communicate with all Cisco equipments.
    - Used for to perform actions not available over telnet/ssh
    - Octo-cables allow it to connect to multiple devices at the same time.

- **Connecting to a Cisco Switch**
  - Get a console cable
  - Plug the serial end into your computer
  - Plug the RJ-45 into the console port of the switch
  - Telnet to serial line (example: ```COM1```)
    - Speed: ```9600```
    - Data bits: ```8```
    - Stop bits: ```1```
    - Parity: ```None```
    - Flow Control: ```None```
  - Telnet Programs
    - Windows
      - Putty
      - Tera Term
      - HyperTerm
    - Linux/Mac
      - Minicom
    - Windows/Linux/Mac
      - SecureCRT ($$$)

- **Cisco Device Boot Process**
  - Can take anywhere from 1 to 10 minutes
  - Decompresses IOS from flash memory to copies to RAM

---
 
[Back to main](https://github.com/rot0xd/CBTNuggets/blob/master/CCNA/ICND-1/README.md)

