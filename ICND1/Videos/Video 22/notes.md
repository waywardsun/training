# Video 22 Notes

## IP Subnetting, Creating Subnets Based on Network Requirements
- **Subnetting Process**
  - Determine number of networks and convert to binary
    - Determine the most significant bit as ```2^n```
  - Reserve bits in subnet mask and find your increment
    - From left to right in the subnet mask binary, replace ```n``` 0's with 1's
  - Use increment to find your network ranges
    - The increment is lowest network bit of the octet converted back to decimal

- **Subnetting Based on Networks: Scenario #1**
  - Organization has purchased Class C address 216.21.5.0
  - They want to use this range to assign addresses in their 5 networks.
  - Subnet Process:
    - Determine number of networks and convert to binary:
      - 5 networks = 00000101
      - Minimum number of bits required to represent 5 = 3
        - 101
    - Reserve bits in subnet mask and find your increment:
      - Original Subnet Mask: 255.255.255.0   (11111111 11111111 11111111 00000000)
      - New Subnet Mask:      255.255.255.224 (11111111 11111111 11111111 11100000)
      - Increment: 00100000 = 32
    - Use increment to find your network ranges:
      - Start: ```216.21.5.0```
        - Network 1 Network Address: ```216.21.5.0```
        - Network 1 Broadcast Address: ```216.21.5.31```
        - Network 1 Subnet Mask: ```255.255.255.224```
      - Increment by 32: ```216.21.5.32```
        - Network 2 Network Address: ```216.21.5.32```
        - Network 2 Broadcast Address: ```216.21.5.63```
        - Network 2 Subnet Mask: ```255.255.255.224```
      - Increment by 32: ```216.21.5.64```
        - Network 3 Network Address: ```216.21.5.64```
        - Network 3 Broadcast Address: ```216.21.5.95```
        - Network 3 Subnet Mask: ```255.255.255.224```
      - Increment by 32: ```216.21.5.96```
        - Network 4 Network Address: ```216.21.5.96```
        - Network 4 Broadcast Address: ```216.21.5.127```
        - Network 4 Subnet Mask: ```255.255.255.224```
      - Increment by 32: ```216.21.5.128```
        - Network 5 Network Address: ```216.21.5.128```
        - Network 5 Broadcast Address: ```216.21.5.159```
        - Network 5 Subnet Mask: ```255.255.255.224```


- **Subnetting Based on Networks: Scenario #2**
  - Organization has purchased Class C address 195.5.20.0
  - They want to use this range to assign addresses in their 50 networks.
  - Subnet Process:
    - Determine number of networks and convert to binary:
      - 50 networks = 00110010
      - Minimum number of bits required to represent 50 = 6
        - 110010
    - Reserve bits in subnet mask and find your increment:
      - Original Subnet Mask: 255.255.255.0   (11111111 11111111 11111111 00000000)
      - New Subnet Mask:      255.255.255.252 (11111111 11111111 11111111 11111100)
      - Increment: 00000100 = 4
    - Use increment to find your network ranges:
      - Start: ```195.5.20.0```
        - Network 1 Network Address: ```195.5.20.0```
        - Network 1 Broadcast Address: ```195.5.20.3```
        - Network 1 Subnet Mask: ```255.255.255.252```
      - Start: ```195.5.20.4```
        - Network 1 Network Address: ```195.5.20.4```
        - Network 1 Broadcast Address: ```195.5.20.7```
        - Network 1 Subnet Mask: ```255.255.255.252```
      - Start: ```195.5.20.8```
        - Network 1 Network Address: ```195.5.20.8```
        - Network 1 Broadcast Address: ```195.5.20.11```
        - Network 1 Subnet Mask: ```255.255.255.252```
      - And so on, and so on, and so on.....


- **Subnetting Based on Networks: Scenario #3**
  - Organization has purchased Class B address 150.5.0.0
  - They want to use this range to assign addresses in their 100 networks.
  - Subnet Process:
    - Determine number of networks and convert to binary:
      - 100 networks = 01100100
      - Minimum number of bits required to represent 100 = 7
        - 01100100
    - Reserve bits in subnet mask and find your increment:
      - Original Subnet Mask: 255.255.0.0   (11111111 11111111 00000000 00000000)
      - New Subnet Mask:      255.255.254.0 (11111111 11111111 11111110 00000000)
      - Increment: 00000010 = 2
    - Use increment to find your network ranges:
      - Start: ```150.5.0.0```
        - Network 1 Network Address: ```150.5.0.0```
        - Network 1 Broadcast Address: ```150.5.1.255```
        - Network 1 Subnet Mask: ```255.255.254.0```
      - Start: ```150.5.2.0```
        - Network 1 Network Address: ```150.5.2.0```
        - Network 1 Broadcast Address: ```150.5.3.255```
        - Network 1 Subnet Mask: ```255.255.254.0```
      - Start: ```150.5.4.0```
        - Network 1 Network Address: ```150.5.4.0```
        - Network 1 Broadcast Address: ```150.5.5.255```
        - Network 1 Subnet Mask: ```255.255.254.0```
      - And so on, and so on, and so on.....


- **Subnetting Based on Networks: Scenario #4**
  - Organization has purchased Class A address 10.0.0.0
  - They want to use this range to assign addresses in their 1000 networks.
  - Subnet Process:
    - Determine number of networks and convert to binary:
      - 1000 networks = 1111101000
      - Minimum number of bits required to represent 100 = 10
        - 1111101000
    - Reserve bits in subnet mask and find your increment:
      - Original Subnet Mask: 255.0.0.0   (11111111 00000000 00000000 00000000)
      - New Subnet Mask:      255.255.192.0 (11111111 11111111 11000000 00000000)
      - Increment: 00100000 = 64
    - Use increment to find your network ranges:
      - Start: ```10.0.0.0```
        - Network 1 Network Address: ```10.0.0.0```
        - Network 1 Broadcast Address: ```10.0.63.255```
        - Network 1 Subnet Mask: ```255.255.192.0```
      - Start: ```10.0.64.0```
        - Network 1 Network Address: ```10.0.64.0```
        - Network 1 Broadcast Address: ```10.0.127.255```
        - Network 1 Subnet Mask: ```255.255.192.0```
      - Start: ```10.0.128.0```
        - Network 1 Network Address: ```10.0.128.0```
        - Network 1 Broadcast Address: ```10.0.191.255```
        - Network 1 Subnet Mask: ```255.255.192.0```
      - And so on, and so on, and so on.....


- **Homework**
  - Class C: 200.1.1.0   - Break into   40 networks
  - Class C: 199.9.10.0  - Break into   14 networks
  - Class B: 170.50.0.0  - Break into 1000 networks
  - Class A: 12.0.0.0    - Break into   25 networks


---
 
[Back to main](https://github.com/rot0xd/CBTNuggets/blob/master/CCNA/ICND-1/README.md)

