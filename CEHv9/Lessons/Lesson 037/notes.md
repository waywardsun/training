#### Video 37 Notes

##### NetBIOS Enumeration

---

- NetBIOS enumeration
  - Runs on port 138/139 on tcp, 137 on UDP
  - Discover computers, shares, services
  - NetBIOS codes can be found at https://en.wikipedia.org/wiki/NetBIOS
  - Done over CLI or GUI
    - `nmap`/`zenmap` on Kali to determine if NetBIOS is running
    - `nbtstat` on Windows to query NetBIOS
    - `net` is used to update, fix, or view the network settings on Windows
    - `NetBIOS Enumerator` is a Windows GUI tool for enumerating NetBIOS


#### `nbtstat` usage examples
```
# Query NetBIOS service on 192.168.1.1
C:\> nbtstat -A 192.168.1.1

# View cached NetBIOS information of networked computers
C:\> nbtstat -c
```


#### `net` usage examples
```
# View shares on 192.168.1.1
C:\> net view \\192.168.1.1

# View devices associated with the WORKGROUP domain
C:\> net view /DOMAIN:WORKGROUP
```

---

[Back to main](https://github.com/rot0xd/CBTNuggets/blob/master/CEHv9/README.md)

