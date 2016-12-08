# Video 31 Notes

## Configuring and Applying Extended Access Control Lists
- **Process of applying Extended ACL's**
  - Extended access lists filter on source/dest IP, protocol, port, and more
  - Extended access lists listen to best match
  - Apply extended ACL's as close to the source as possible
  - Configuration
    - Configuring the access list
    - Apply the access list
  - To view the access lists:
    - ```CBTRouter1# show ip access-list```


- **Extended Access-Lists: Practice Examples**
  - Use extended ACL's to block 192.168.1.0/24 from reaching 192.168.2.128/25
    - ```CBTRouter1(config)# access-list 100 deny ip 192.168.1.0 0.0.0.255 192.168.2.128 0.0.0.127```
    - ```CBTRouter1(config)# access-list 100 permit ip any any```
    - ```CBTRouter1(config)# interface fastEthernet 0/0```
    - ```CBTRouter1(config-if)# ip access-group 100 in```
  - Use extended ACL's to block 192.168.1.50 from reaching 192.168.2.50 on HTTP or HTTPS
    - ```CBTRouter1(config)# ip access-list extended 100```
    - ```CBTRouter1(config-ext-nacl)# 11 deny tcp 192.168.1.50 0.0.0.0 192.168.2.50 0.0.0.0 eq 80```
    - ```CBTRouter1(config-ext-nacl)# 12 deny tcp 192.168.1.50 0.0.0.0 192.168.2.50 0.0.0.0 eq 443```
  - Permit 192.168.2.0/25 to access 10.1.1.1 using only Telnet and SSH
    - ```CBTRouter2(config)# ip access-list extended ALLOW_PC1_TELNET_SSH```
    - ```CBTRouter2(config-ext-nacl)# permit tcp 192.168.2.0 0.0.0.127 host 10.1.1.1 range 22 23```
    - ```CBTRouter2(config-ext-nacl)# deny ip 192.168.2.0 0.0.0.127 host 10.1.1.1```
    - ```CBTRouter2(config-ext-nacl)# permit ip any any```
    - ```CBTRouter2(config)# interface fastEthernet 0/0```
    - ```CBTRouter2(config-if)# ip access-group ALLOW_PC1_TELNET_SSH in```
  - Use extended ACL's to block 192.168.1.0/24 from reaching any WAN IP addresses
    - ```CBTRouter1(config)# ip access-list extended BLOCK_WAN```
    - ```CBTRouter1(config-ext-nacl)# deny ip 192.168.1.0 0.0.0.255 10.1.1.0 0.0.0.3```
    - ```CBTRouter1(config-ext-nacl)# deny ip 192.168.1.0 0.0.0.255 10.1.1.4 0.0.0.3```
    - ```CBTRouter1(config-ext-nacl)# permit ip any any```
    - ```CBTRouter1(config)# interface fastEthernet 0/0```
    - ```CBTRouter1(config-if)# ip access-group BLOCK_WAN in```
  - Permit Access to 192.168.2.50 using only SMTP, POP3, IMAP4 from anywhere
    - ```CBTRouter2(config)# ip access-list extended ALLOW_SMTP_POP3_IMAP```
    - ```CBTRouter2(config-ext-nacl)# permit tcp any host 192.168.2.50 eq 25```
    - ```CBTRouter2(config-ext-nacl)# permit tcp any host 192.168.2.50 eq 110```
    - ```CBTRouter2(config-ext-nacl)# permit tcp any host 192.168.2.50 eq 143```
    - ```CBTRouter2(config-ext-nacl)# deny ip any host 192.168.2.50```
    - ```CBTRouter2(config-ext-nacl)# permit ip any any```
    - ```CBTRouter2(config)# interface fastEthernet 0/0```
    - ```CBTRouter2(config-if)# ip access-group BLOCK_WAN out```


---
 
[Back to main](https://github.com/rot0xd/CBTNuggets/blob/master/CCNA/ICND-1/README.md)

