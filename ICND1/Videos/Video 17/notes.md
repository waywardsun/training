# Video 17 Notes

## Understanding VTP and 802.1Q
- **Understanding How Trunks Really Work**
  - Review: What is Trunking
    - Also known as "tagging"
    - Passes multi-VLAN information between switches
    - Places VLAN information into each frame
    - Layer 2 feature
    - Uses 802.1Q or ISL (Interswitch Link) to tag the frame
      - 802.1Q replaces ISL becoming the industry standard
  - 802.1Q
    - Adds 4 byte tag to a frame
      - 3 bits for CoS (Class of Service)
      - 12 bits for VLAN tag
        - Supports up to 4096 VLANs
    - VLAN tag used for switch-to-switch communication
    - VLAN tag always removed before packet send to endpoint

- **Catching the VLAN Lingo: Native VLANs**
  - Untagged traffic is used for management protocols
    - Examples: CDP, SSH, Telnet
  - Untagged traffic belong to a native VLAN
  - If a trunk receives data with no tag, it becomes part of native VLAN
  - Switches must have matching native VLAN numbers
  - A switch sending traffic to native VLAN does not add VLAN tag
  - If native VLANs do not match, traffic gets an unwanted merge across VLANs


- **How VTP Can Help... or Destroy... Your Network**
  - VLAN Trunking Protocol
    - Not really a trunking protocol
    - The only trunking protocols are 802.1Q and ISL
    - Should have been called VLAN Replication Protocol
  - The Idea:
    - Link all switches with Trunks
    - All switches start with VTP revision 0
    - If a switch updates it's VLANs, updates it VTP revision to 1
    - All switches with lower revisions copy the new VLAN configuration
  - The Problem:
    - No verification that update is wanted
    - A switch plugged with a higher VTP revision overwrites lower revisions
    - Rogue/Malicious switch can destroy your VLAN configuration
    - VTP Revisions survive configuration resets
  - The Protection:
    - VTP works through domain names
    - VLAN configurations with mismatching domain names will not propogate
  - VTP not recommended for use due to destructive capability
  - Safer to manually configure VLANs on each device


- **VTP Modes**
  - Server (Default)
    - Power to change VLAN information
    - Sends and receives VTP updates
    - Saves VLAN configuration
  - Client
    - Cannot change VLAN information
    - Sends and receives VTP updates
    - Does not save VLAN configuration
  - Transparent (Recommended)
    - Power to change VLAN information
    - Forwards (Passes through) VTP updates
    - Does not listen to VTP advertisements
    - Saves VLAN configuration
  - Cisco recommends only one server, the rest as clients 
  - There is no way to turn off VTP.
    - The closest is transparent mode, which ignores VTP configuration


- **VLAN Pruning**
  - Keeps unnecessary broadcast traffic from crossing Trunk links
  - If broadcast is destined for VLAN not downstream, don't send it any further
  - Only works on VTP servers


---
 
[Back to main](https://github.com/rot0xd/CBTNuggets/blob/master/CCNA/ICND-1/README.md)

