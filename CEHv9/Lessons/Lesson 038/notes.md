#### Video 38 Notes

##### SNMP Enumeration Concepts

---

- Simple Network Management Protocol (SNMP)
  - Uses port 161/162 on UDP
  - Key Terms
    - `OID` - Object ID
    - `MIB` - Management information base
  - Community Strings are the equivalent of passwords
    - Default RO: `public`
    - Default RW: `private`
  - Version differences
    - v1/v2 send traffic over plaintext
    - v3 supports authentication, encryption, data integrity when configured
  - SNMP filtering allows communication with only authorized hosts
  - SNMP walking
    - Station makes a request to see everything an agent has

Cisco IOS SNMP Configuration
```
R1# show ip int brief
R1# access-list 1 permit 192.168.1.0 0.0.0.255
R1# snmp-server community public RO 1
R1# snmp-server community private RW 1
R1# show run
R1# show snmp
```

---

[Back to main](https://github.com/rot0xd/CBTNuggets/blob/master/CEHv9/README.md)

