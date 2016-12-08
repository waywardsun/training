# Video 29 Notes

## Using Access Control Lists
- **Access-Lists: They're not just for access!**
  - What they are:
    - Matching mechanism
    - List of permit and deny statements
    - Examples:
      - ```permit 192.168.2.50```
      - ```deny 192.168.1.0/24```
      - ```permit tcp port 80 for 200.1.1.1```
      - ```permit all tcp traffic for 210.0.1.0/24```
  - What they can be used for:
    - Access Control
    - NAT
    - Quality of Service
    - Demand Dial Routing
    - Policy Routing
    - Route Filtering
    - Making French Toast


- **Using ACL's for Security**
  - List is read from top to bottom and stops at first match
    - Invisible implicit deny at the bottom
  - ACL is applied to an interface inbound or outbound
  - Other possibilities:
    - ACL used for NAT
    - ACL used for QoS
    - ACL used for VPN


- **Types of ACL's**
  - Standard
    - Matches based:
      - Source address
    - Lower processor utilization
    - Effect depends on application
  - Extended
    - Matches based on:
      - Source/destination address
      - Protocol
      - Source/destination port number
    - Higher processor utilization
    - Syntax takes some time to learn
  - Reflexive (Established)
    - Allows return traffic for internal requests


---
 
[Back to main](https://github.com/rot0xd/CBTNuggets/blob/master/CCNA/ICND-1/README.md)

