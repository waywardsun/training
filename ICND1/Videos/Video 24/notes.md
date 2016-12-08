# Video 24 Notes

## IP Subnetting, Reverse Engineering Subnet Problems
- **Reverse Engineering Process**
  - Layout subnet mask in binary
  - Determine Increment
  - Figure out networks
  - Determine details for network of target


- **Reverse Engineering Subnets: Scenario #1```
  - Host: ```192.168.1.127```
  - Subnet Mask: ```255.255.255.224```
  - Reverse Engineering Process:
    - Layout subnet mask in binary: 
      - ```255.255.255.224``` = ```11111111.11111111.11111111.11100000````
    - Determine Increment:
      - 00100000 = 32
    - Figure out networks:
      - 192.168.1.0 - 192.168.1.31
      - 192.168.1.32 - 192.168.1.63
      - 192.168.1.64 - 192.168.1.95
      - 192.168.1.96 - 192.168.1.127
      - 192.168.1.128 - 192.168.1.159
      - and so on, and so on
    - Determine details for network of target:
      - Range: ```192.168.1.96 - 192.168.1.127```
      - Network: ```192.168.1.96/27```
      - Broadcast: ```192.168.1.127```


- **Reverse Engineering Subnets: Scenario #2```
  - Host: ```172.16.68.65```
  - Subnet Mask: ```255.255.255.240```
  - Gateway Address: ```172.16.68.62```
  - Reverse Engineering Process:
    - Layout subnet mask in binary: 
      - ```255.255.255.240``` = ```11111111.11111111.11111111.11110000````
    - Determine Increment:
      - 00010000 = 16
    - Figure out networks:
      - 172.16.68.0 - 172.16.68.15
      - 172.16.68.16 - 172.16.68.31
      - 172.16.68.32 - 172.16.68.47
      - 172.16.68.48 - 172.16.68.63
      - 172.16.68.64 - 172.16.68.79
      - and so on, and so on
    - Determine details for network of target:
      - Range: ```172.16.68.64 - 172.16.68.79```
      - Network: ```172.16.68.64/27```
      - Broadcast: ```172.16.68.79```


- **The Great Exceptions**
  - Because binary begins counting from zero:
    - These network values may throw off calculations:
      - 2, 4, 8, 16, 32, 64, 128
    - These host values may throw off calculations:
      - 3, 7, 15, 31, 63, 127
  - To be safe, always:
    - Subtract 1 when finding networks
    - Add 1 when finding hosts


---
 
[Back to main](https://github.com/rot0xd/CBTNuggets/blob/master/CCNA/ICND-1/README.md)

