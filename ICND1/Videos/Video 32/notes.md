# Video 32 Notes

## NAT Concepts
- **What is Network Address Translation (NAT)**
  - Internet = Big Network
  - Too many devices compared to the number of total IP addresses
  - IP management necessary
  - Public and private divide needed
  - Welcome to NAT!
  

- **Public to Private: Let me count the ways...**
  - Static NAT
    - Mapping from internal network to external network addresses
    - These mappings do not change
    - Similar to port forwarding but bi-directional
  - Dynamic NAT
    - Specifies pool of public and private addresses
    - Creates mappings from public pool to private pool
    - Used when two networks with conflicting address spaces communicate
  - Port Address Translation (PAT)
    - Most common form
    - Uses internal IP's source port as external IP's source port
    - Table kept in router to map ports to internal machines


---
 
[Back to main](https://github.com/rot0xd/CBTNuggets/blob/master/CCNA/ICND-1/README.md)

