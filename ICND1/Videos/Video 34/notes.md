# Video 34 Notes

## IPv6 Concepts
- **Will We Ever Need To Upgrade To IPv6?!?**
  - There is an IP address shortage.
  - Current IP addresses poorly allocated
  - New network devices on the rise
  - NAT (our current solution) is seend as a hinderance to innovation
  - Potential future features: 
    - IPSec everywhere
    - Mobility
    - Simple header


- **IPv6 Addressing Format**
  - Address size moved from 32-bit (IPv4) to 128-bit (IPv6)
  - Provides 340,282,366,920,938,463,463,374,607,431,770,000,000 IP addresses!
  - To make addresses more manageable, divided into 8 groups of 4 hex characters
    - Example: ```2001:0050:0000:0000:0000:0AB4:1E2B:98AA```
  - Rule 1: Eliminate Groups of consecutive zeroes
    - Example: ```2001:0050::0AB4:1E2B:98AA```
      - Double colon indicates shortened group of zeroes
      - Can only use the double colon once in the address
  - Rule 2: Drop leading zeroes
    - Example: ```2001:50::AB4:1E2B:98AA```


- **IPv6 Headers and Address types**
  - Headers
    - IPv6 header is bigger than IPv4 header due simply to the address size
    - Much simpler due to less fields
    - Extension headers possible with "next header" field
  - Types of Communication
    - Unicast: One-to-One communication
    - Multicast: One-to-Many communication
    - Anycast: One-to-Closest communication
    - Broadcast has been removed in IPv6
      - The concept had been grouped into multicast
  - Types of Addresses
    - Link-Local Scope Address: Layer 2 domain
      - Assigned automaticalls as an IPv6 host comes online
      - Local-subnet-only address (Think IPv4's 169.254.x.x)
      - Begins with ```FE80``` followd by 54 zero bits
      - Host portion uses EUI-64
      - EUI-64: Uses MAC address as host portion of IP address
        - Example: MAC address is ```11:22:33:44:55:66```
          - Places ```FF:FE``` in the middle of the MAC address
          - IPv6 Address: ```FE80::11:22:33:FF:FE:44:55:66```
    - Unique/Site-Local Scope Address: Organization
      - Equivalent to private IPv4 addresses (192.168.x.x, etc)
      - If there is enough public addresses, do we need these?
    - Global Scope Address: Internet
      - Equivalent to public IPv4 addresses
      - Enough addresses for all devices in the world to have a public IP
      - IANA handles address distribution
      - Have their high-level 3 bits set to 001
        - Mask: ```2000::/3```
          - Could also be ```3000::/3``` but much less common
      - Global routing prefix is 48 bits or less
      - Subnet ID is comprised of bits left over after global routing prefix
      - Primary addresses expected to comprise IPv6 internet are ```2001::/16``` subnet
        - ```/32``` subnets are assigned to providers. (Global Prefix)
        - ```/48, /56, /64``` subnets are assigned to customers


---
 
[Back to main](https://github.com/rot0xd/CBTNuggets/blob/master/CCNA/ICND-1/README.md)

