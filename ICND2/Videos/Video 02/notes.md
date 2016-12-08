#### Video 02 Notes

##### ICND1 Review Lab, Part 1: Base Configurations
- **Rebuilding the Structure**
  - Corporate Office Subnets:
    - Default (VLAN 1): 10.24.0.0/24
    - Accounting (VLAN 2): 10.24.5.0/24
    - IT Team (VLAN 3): 10.24.2.0/24
  - Branch Office Subnets:
    - Default (VLAN 1): 10.23.1.0/24


- **Basic Router Configuration**

```
R1# conf t
R1(config)# hostname R1
R1(config)# line console 0
R1(config-line)# no exec-timeout
R1(config-line)# password NuggetLove
R1(config-line)# login
R1(config-line)# exit
R1(config)# line vty 0 4
R1(config-line)# no exec-timeout
R1(config-line)# password NuggetLove
R1(config-line)# transport input ssh telnet
R1(config-line)# login
R1(config-line)# exit
R1(config)# enable secret cisco
R1(config)# no ip domain-lookup
R1(config)# banner motd +
***********************************************
BEWARE :: BEWARE :: BEWARE :: BEWARE :: BEWARE
***********************************************
+
```

---

[Back to main](https://github.com/rot0xd/CBTNuggets/blob/master/CCNA/ICND-2/README.md)

