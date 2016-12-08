#### Video 25 Notes

##### DNS Tools

---

- DNS Record Types
  - `A` - IPv4 Address record
  - `AAAA` - IPv6 Address record
  - `CNAME` - Alias to another record
  - `MX` - Mail exchange record
  - `NS` - Nameserver record
- Making queries
  - CLI
    - `nslookup`
      - `nslookup` without an argument enters interactive mode
      - `set type=AAAA` returns only `AAAA` records
      - `server 192.168.1.212` uses `192.168.1.212` to resolve dns requests
  - Web-based tools
    - `network-tools.com/nslook`

---

[Back to main](https://github.com/rot0xd/CBTNuggets/blob/master/CEHv9/README.md)

