# Video 15 Notes

## Cisco Switching - Day to Day
- **"The Network is Slow!" - Speed and Duplex**
  - Cisco's default duplex is auto
  - Speed always detects correctly
  - Duplex often mis-detected in 10Mbps and 100Mbps connections
  - For key devices, manually configure speed and duplex. Don't rely on auto
    - To configure speed
      - ```Switch(config-if)# speed 100```
    - To configure duplex
      - ```Switch(config-if)# duplex full```
  - Auto MDIX - Allows use of either crossover cables and straightthrough cables
  - If auto mode is disabled, Auto MDIX no longer works


- **Understanding Key Interface Counters**
  - To view the collisions on an interface:
    - ```Switch# show interfaces fastEthernet 0/1```
    - Late collisions always indicate a duplex mismatch


- **Finding Devices: MAC Address Tables**
  - To view the MAC address table:
    - ```Switch# show mac address-table```
  - To filter by MAC address
    - ```Switch# show mac address-table | include 0000.0000.0000```


---
 
[Back to main](https://github.com/rot0xd/CBTNuggets/blob/master/CCNA/ICND-1/README.md)

