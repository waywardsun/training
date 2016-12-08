# Video 23 Notes

## IP Subnetting, Creating Subnets Based on Host Requirements
- **Subnetting Process**
  - Determine number of hosts per network and convert to binary
    - Determine the most significant bit as ```2^n```
  - Reserve bits in subnet mask and find your increment
    - Set ```n``` bits in subnet mask to 0 from right to left. The rest are 1's
  - Use increment to find your network ranges
    - The increment is lowest network bit of the octet converted back to decimal


- **Subnetting Based on Networks: Scenario #1**
  - Organization has purchased Class C address 216.21.5.0
  - They want to use this range to assign networks containing 30 hosts each
  - Subnet Process:
    - Determine number of hosts and convert to binary:
      - 30 hosts = 00011110
      - Minimum number of bits required to represent 30 = 5
        - 11110
    - Reserve bits in subnet mask and find your increment:
      - Original Subnet Mask: 255.255.255.0   (11111111 11111111 11111111 00000000)
      - New Subnet Mask:      255.255.255.224 (11111111 11111111 11111111 11100000)
      - Increment: 00100000 = 32
    - Use increment to find your network ranges:
      - Start: ```216.21.5.0```
        - Network 1 Network Address: ```216.21.5.0```
        - Network 1 Broadcast Address: ```216.21.5.31```
        - Network 1 Subnet Mask: ```255.255.255.224```
      - Start: ```216.21.5.32```
        - Network 2 Network Address: ```216.21.5.32```
        - Network 2 Broadcast Address: ```216.21.5.63```
        - Network 2 Subnet Mask: ```255.255.255.224```
      - Start: ```216.21.5.64```
        - Network 3 Network Address: ```216.21.5.64```
        - Network 3 Broadcast Address: ```216.21.5.95```
        - Network 3 Subnet Mask: ```255.255.255.224```
      - And so on, and so on, and so on.....


- **Subnetting Based on Networks: Scenario #2**
  - Organization has purchased Class C address 195.5.20.0
  - They want to use this range to assign networks containing 50 hosts each
  - Subnet Process:
    - Determine number of hosts and convert to binary:
      - 50 hosts = 00110010
      - Minimum number of bits required to represent 50 = 6
        - 110010
    - Reserve bits in subnet mask and find your increment:
      - Original Subnet Mask: 255.255.255.0   (11111111 11111111 11111111 00000000)
      - New Subnet Mask:      255.255.255.192 (11111111 11111111 11111111 11000000)
      - Increment: 01000000 = 64
    - Use increment to find your network ranges:
      - Start: ```195.5.20.0```
        - Network 1 Network Address: ```195.5.20.0```
        - Network 1 Broadcast Address: ```195.5.20.63```
        - Network 1 Subnet Mask: ```255.255.255.192```
      - Start: ```195.5.20.64```
        - Network 2 Network Address: ```195.5.20.64```
        - Network 2 Broadcast Address: ```195.5.20.127```
        - Network 2 Subnet Mask: ```255.255.255.192```
      - Start: ```195.5.20.128```
        - Network 3 Network Address: ```195.5.20.128```
        - Network 3 Broadcast Address: ```195.5.20.191```
        - Network 3 Subnet Mask: ```255.255.255.192```
      - And so on, and so on, and so on.....


- **Subnetting Based on Networks: Scenario #3**
  - Organization has purchased Class B address 150.5.0.0
  - They want to use this range to assign networks containing 500 hosts each
  - Subnet Process:
    - Determine number of hosts and convert to binary:
      - 500 hosts = 111110011
      - Minimum number of bits required to represent 500 = 9
        - 111110011
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
        - Network 2 Network Address: ```150.5.2.0```
        - Network 2 Broadcast Address: ```150.5.3.255```
        - Network 2 Subnet Mask: ```255.255.254.0```
      - Start: ```150.5.4.0```
        - Network 3 Network Address: ```150.5.4.0```
        - Network 3 Broadcast Address: ```150.5.5.255```
        - Network 3 Subnet Mask: ```255.255.254.0```
      - And so on, and so on, and so on.....


- **Subnetting Based on Networks: Scenario #4**
  - Organization has purchased Class B address 10.0.0.0
  - They want to use this range to assign networks containing 100 hosts each
  - Subnet Process:
    - Determine number of hosts and convert to binary:
      - 100 hosts = 01100100
      - Minimum number of bits required to represent 100 = 7
        - 1100100
    - Reserve bits in subnet mask and find your increment:
      - Original Subnet Mask: 255.255.0.0   (11111111 00000000 00000000 00000000)
      - New Subnet Mask:      255.255.255.128 (11111111 11111111 11111111 10000000)
      - Increment: 10000000 = 128
    - Use increment to find your network ranges:
      - Start: ```10.0.0.0```
        - Network 1 Network Address: ```10.0.0.0```
        - Network 1 Broadcast Address: ```10.0.0.127```
        - Network 1 Subnet Mask: ```255.255.255.128```
      - Start: ```10.0.0.128```
        - Network 2 Network Address: ```10.0.0.128```
        - Network 2 Broadcast Address: ```10.0.0.255```
        - Network 2 Subnet Mask: ```255.255.255.128```
      - Start: ```10.0.1.0```
        - Network 3 Network Address: ```10.0.1.0```
        - Network 3 Broadcast Address: ```10.0.1.127```
        - Network 3 Subnet Mask: ```255.255.255.128```
      - And so on, and so on, and so on.....


- **Homework**
  - Class C: 200.1.1.0   - Break into networks of   40 hosts
  - Class C: 199.9.10.0  - Break into networks of   12 hosts
  - Class B: 170.50.0.0  - Break into networks of 1000 hosts
  - Class A: 12.0.0.0    - Break into networks of  100 hosts


---
 
[Back to main](https://github.com/rot0xd/CBTNuggets/blob/master/CCNA/ICND-1/README.md)

