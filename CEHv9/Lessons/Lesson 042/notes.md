#### Video 42 Notes

##### NTP Enumeration

---

- Network Time Protocol (NTP)
  - Operates on port 123 over UDP
- `ntpdate` and `ntpdc`
  - Linux tools for configuring and interacting with NTP servers

#### NTP CLI tools usage syntax
```
root@kali:~# ntpdate 192.168.1.212
root@kali:~# ntpdc
ntpdc> help
ntpdc commands:
addpeer      controlkey   fudge        keytype      quit         timeout      
addrefclock  ctlstats     help         listpeers    readkeys     timerstats   
addserver    debug        host         loopinfo     requestkey   traps        
addtrap      delay        hostnames    memstats     reset        trustedkey   
authinfo     delrestrict  ifreload     monlist      reslist      unconfig     
broadcast    disable      ifstats      passwd       restrict     unrestrict   
clkbug       dmpeers      iostats      peers        showpeer     untrustedkey 
clockstat    enable       kerninfo     preset       sysinfo      version      
clrtrap      exit         keyid        pstats       sysstats     
ntpdc>
```

---

[Back to main](https://github.com/rot0xd/CBTNuggets/blob/master/CEHv9/README.md)

