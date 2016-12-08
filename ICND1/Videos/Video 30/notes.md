# Video 30 Notes

## Configuring and Applying Standard Access Control Lists
- **Process of applying ACL's**
  - Standard access lists only filter on source IP
  - Standard access lists only listen to first match
  - Configuration
    - Configuring the access list
      - ```CBTRouter1(config)# access-list X deny host Y.Y.Y.Y```
        - ```X``` - The access-list # to use
        - ```Y``` - The host the rule applies to
      - ```CBTRouter1(config)# access-list X permit any```
        - ```X``` - The access-list # to use
    - Apply the access list
      - ```CBTRouter1(config-if)# ip access-group X Y```
        - ```X``` - The access-list # to use
        - ```Y``` - Inbound or outbound
  - To view the access lists:
    - ```CBTRouter1# show ip access-list```


- **Standard Access-Lists: Practice Examples**
  - Use standard ACL's to block 10.1.1.1 from reaching 10.1.1.6 & 192.168.1.0/24
    - ```CBTRouter1(config)# access-list 1 deny host 10.1.1.1```
    - ```CBTRouter1(config)# access-list 1 permit any```
    - ```CBTRouter1(config)# interface serial 0/0```
    - ```CBTRouter1(config-if)# ip access-group 1 in```
  - Use standard ACL's to block 192.168.2.128/25 from reaching 192.168.1.0/24
    - ```CBTRouter1(config)# access-list 2 deny 192.168.2.128 0.0.0.127```
    - ```CBTRouter1(config)# access-list 2 permit any```
    - ```CBTRouter1(config)# interface fastEthernet 0/0```
    - ```CBTRouter1(config-if)# ip access-group 2 out```
  - Use standard ACL's to block 192.168.2.50 from reaching 10.1.1.1
    - ```CBTRouter2(config)# ip access-list standard BLOCK_PC2_ACL```
    - ```CBTRouter2(config-std-nacl)# deny 192.168.2.50 0.0.0.0```
    - ```CBTRouter2(config-std-nacl)# permit any```
    - ```CBTRouter2(config)# interface serial 0/1```
    - ```CBTRouter2(config-if)# ip access-group BLOCK_PC2_ACL out```

---
 
[Back to main](https://github.com/rot0xd/CBTNuggets/blob/master/CCNA/ICND-1/README.md)

