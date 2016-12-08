# Video 16 Notes

## Understanding VLANs and Trunks
- **The View of a "Normal Switch"**
  - Multiple Collision Domains
    - Pool of devices that collide with each other
  - One Broadcast Domain
    - How far a broadcast goes before it is stopped
  - One IP Network (Subnet)
    - Everybody's IP address begins with same prefix
  - One "Failure" Domain
    - If one device corrupts network, all devices affected
  - Limited Security
    - One device has access to other devices on switch


- **VLAN Foundations**
  - Logically groups users
  - Segments broadcast domains
  - Subnet correlation
  - Access control
  - Quality of Service (QoS)
    - Allows switch to assign priority to devices on the network


- **Trunk**
  - Carries all traffic out of a Cisco device
  - Contains all traffic from all VLANs
  - Non-Cisco calls this a "Tagged Port"


- **VLANs... What they make possible!**
  - "Like Type" Segmentation
    - Group similar devices on a network
    - Ex: All phones on a network, all sales computers, etc
  - Server Virtualization
    - Can set up a hypervisor's port as a trunk
    - Allows virtualized servers to be on seperate VLANs
  - Unified Network and WiFi
    - Can have devices located in seperate buildings on same network
    - Don't lose WiFi connection as user walks across buildings


---
 
[Back to main](https://github.com/rot0xd/CBTNuggets/blob/master/CCNA/ICND-1/README.md)

