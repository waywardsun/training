#### Video 36 Notes

##### Enumeration Concepts

---

- enumeration concepts
  - direct access
  - gain more information
  - typically done from internal network
- possible enumeration sources
  - Server
    - Determine shares, folders 
  - Router
    - Obtain routing table
    - introduce routes for mitm attacks
  - DNS Server
    - obtain internal hostname/ip address mappings
  - hosts
    - get hostnames, groups, port scans, applications
  - snmp, netbios, ldap, ntp
    - provides wealth of information about host/device/network
- example goals of enumeration
  - Get usernames using email id
    - possibly from business cards?
  - Get information using the default password
    - look up default passwords for service/device and login
  - Get usernames using snmp
    - not uncommon to see defaults being used
  - Brute force active directory
    - AD is the corporate infrastructure standard. 
  - Get user groups from windows
    - learn different types of accounts and associations between users
  - Get information using dns zone transfer
    - learn all ip addresses being mapped by hostname

---

[Back to main](https://github.com/rot0xd/CBTNuggets/blob/master/CEHv9/README.md)

