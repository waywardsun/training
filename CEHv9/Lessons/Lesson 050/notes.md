#### Video 50 Notes

##### DHCP Starvation

---

- DHCP starvation
  - Why do it?
    - Flood DHCP server
    - DoS
    - Introduce another DHCP server
  - To protect yourself:
    - Limit one mac to port with `switchport port-security`
    - Enable DHCP snooping
  - Tool used
    - `yersinia`

- Common Cisco IOS DHCP commands:
  - `show ip dhcp binding`
  - `show ip dhcp server statistics`
  - `show ip dhcp pool`


#### yersinia usage example
```
# Bring up GUI mode
root@kali:~/# yersinia -G
```

---

[Back to main](https://github.com/rot0xd/CBTNuggets/blob/master/CEHv9/README.md)

