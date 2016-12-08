# Video 25 Notes

## Variable Lenth Subnet Masking (VLSM)
- **VLSM Concepts**
  - Change subnet mask whenever you want
  - VLSM Process
    - Determine number of bits to accomodate largest subnet
    - Reserve bits in the subnet mask and find our increment
    - Determine network range
    - Repeat for remaining networks


- **VLSM: Scenario #1**
  - Subnet 192.168.1.0/24 to accomodate the following networks:
    - 20 Users on Network 1
    - 20 Users on Network 2
    - 60 Users on Network 3
    - A single WAN link between the 3 networks
    - Use the most efficient addressing possible
  - VLSM Process
    - First network:
      - Determine number of bits to accomodate largest subnet
        - 60 Users = 00111100  = 6 Bits
      - Reserve bits in the subnet mask and find our increment
        - Original subnet mask = ```255.255.255.0 (11111111.11111111.11111111.00000000)```
        - New subnet mask = ```255.255.255.192 (11111111.11111111.11111111.11000000)```
        - Increment = 01000000 = 64
      - Network Range:
        - ```192.168.1.0 - 192.168.1.63/26```
    - Next network:
      - Determine number of bits to accomodate largest subnet
        - 20 Users = 00010100  = 5 Bits
      - Reserve bits in the subnet mask and find our increment
        - Original subnet mask = ```255.255.255.0 (11111111.11111111.11111111.00000000)```
        - New subnet mask = ```255.255.255.224 (11111111.11111111.11111111.11100000)```
        - Increment = 00100000 = 32
      - Network Range:
        - ```192.168.1.64 - 192.168.1.95/27```
    - Next network:
      - Determine number of bits to accomodate largest subnet
        - 20 Users = 00010100  = 5 Bits
      - Reserve bits in the subnet mask and find our increment
        - Original subnet mask = ```255.255.255.0 (11111111.11111111.11111111.00000000)```
        - New subnet mask = ```255.255.255.224 (11111111.11111111.11111111.11100000)```
        - Increment = 00100000 = 32
      - Network Range:
        - ```192.168.1.96 - 192.168.1.127/27```
    - Finally, the WAN links:
      - Determine number of bits to accomodate largest subnet
        - 2 Users = 00000010  = 2 Bits
      - Reserve bits in the subnet mask and find our increment
        - Original subnet mask = ```255.255.255.0 (11111111.11111111.11111111.00000000)```
        - New subnet mask = ```255.255.255.252 (11111111.11111111.11111111.11111100)```
        - Increment = 00000100 = 4
      - Network Ranges:
        - ```192.168.1.128 - 192.168.1.131/30```
        - ```192.168.1.132 - 192.168.1.135/30```
        - ```192.168.1.136 - 192.168.1.139/30```


---
 
[Back to main](https://github.com/rot0xd/CBTNuggets/blob/master/CCNA/ICND-1/README.md)

