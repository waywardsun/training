#### Video 30 Notes

##### Stealth Idle Scanning

---

- Idle Scan (Stealthy)
  - Find and probe zombie
    - Send SYN/ACK to Zombie
    - Receive RST and take note of fragment ID
  - Send spoofed packets
    - Use source address of Zombie to send SYN to Target
    - Target responds to Zombie with SYN/ACK if open incrementing zombies fragment ID
    - Target responds to Zombie with RST if closed and fragment ID does not increment
  - Probe zombie again
    - Send SYN/ACK to Zombie
    - Receive RST and take note of fragment ID
      - If fragment ID is one greater than initial fragment ID, port is not open

#### nmap usage examples
```
# Find which hosts on the network are up and running
nmap -sn 192.168.1.0/24

# -Pn = Assume all hosts are up, do not ping
# -sI = Idle scan
# 192.168.1.216 = Zombie
# 192.168.1.212 = Target
nmap -Pn -sI 192.168.1.216 192.168.1.212
```

---

[Back to main](https://github.com/rot0xd/CBTNuggets/blob/master/CEHv9/README.md)

