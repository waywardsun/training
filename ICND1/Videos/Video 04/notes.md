# Video 04 Notes

## Basics of IP Addressing
- **IP Addresses**
  - Four octets, each with a value of 0 to 255
  - Three core classes
  - Combined with a subnet mask and usually a default gateway
    - IP Address defines your home
    - Subnet mask defines your neighborhood

- **Subnet Mask**
  - Subnet mask defines the network your host lives on.
  - Example: 255.255.255.0
    - 11111111 11111111 11111111 00000000
    - First three octets define the network
    - Last octet defines the host
  - Example: 255.255.240.0
    - 11111111 11111111 11110000 00000000
    - First 20 bits define the network
    - Remaining zero bites defines the host

- **ARP**
  - MAC Address Sonar
  - Finds MAC address for a requested IP address.
  - ```arp -a``` - lists all known MAC addresses on the network
  - ```arp -d``` - deletes all ARP entries

- **Default Gateway**
  - The path off of your network
  - Usually your router
  - If router does not know the path, it uses default route
    - ```0.0.0.0``` - IPv4 default route

---
 
[Back to main](https://github.com/rot0xd/CBTNuggets/blob/master/CCNA/ICND-1/README.md)

