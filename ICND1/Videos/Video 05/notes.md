# Video 05 Notes

## IP Addressing - Filling in the gaps
- **Assigning IP Addresses**
  - Static
    - Manually set the IP Address
    - IP Address does not change unless you change it
    - Not scalable
  - DHCP
    - Obtain an IP Address automatically from a pool of reserved addresses
    - IP Address may change after lease expires
    - New devices send broadcast requesting an IP Address assignment
  - DHCP Relay
    - Take DHCP Broadcast and send as unicast to DHCP server outside the network
    - Used when you want to use a DHCP server that is located offsite

- **Public and Private IP Addresses**
  - Private IP Addresses
    - ```10.0.0.0/8``` - 10.0.0.0 through 10.255.255.255
    - ```172.16.0.0/12``` - 172.16.0.0 through 172.31.255.255
    - ```192.168.0.0/16``` - 192.168.0.0 through 192.168.255.255
  - Automatic Addressing
    - ```169.254.0.0/16``` - 169.254.0.0 through 169.254.255.255
  - Loopback Addressing
    - ```127.0.0.0/8``` - 127.0.0.0 through 127.255.255.255
  - Special Addresses
    - First address of a network - Network address
    - Last address of a network - Broadcast address

- **Classes of Addresses**
  - Class A - First octet is 1 through 127
    - Subnet Mask: ```255.0.0.0```
    - CIDR: ```X.X.X.X/8```
  - Class B - First octet is 128 through 191
    - Subnet Mask: ```255.255.0.0```
    - CIDR: ```X.X.X.X/16```
  - Class C - First octet is 192 through 223
    - Subnet Mask: ```255.255.255.0```
    - CIDR: ```X.X.X.X/24```
  - Class D - First octet is 224 through 239
    - Multicast
  - Class E - First octet is 240 through 254
    - Experimental

- **Classful vs Classless**
  - Classful - Use a network with every intended address 
    - Example: Use X.X.X.X/8 in class A network
  - Classless - Apply a narrower subnet mask to a large class network (
    - Example: Use X.X.X.X/24 in Class A network

- **Unicast vs Multicast vs Broadcast**
  - Unicast - One message to a single destination
    - Uses: Host-to-Host Communication
  - Multicast - One message to a group
    - Uses: Internet Radio, OS Image Server
  - Broadcast - One message to everybody
    - Uses: DHCP Request, ARP

---
 
[Back to main](https://github.com/rot0xd/CBTNuggets/blob/master/CCNA/ICND-1/README.md)

