# Video 06 Notes

## How Applications Speak
- **TCP and UDP**
  - The primary transport layer protocols used today
  - UDP - User Datagram Protocol
    - "I hope it gets there"
    - Used when reliable communication is not necessary
    - Examples: VoIP, DNS
  - TCP - Transmission Control Protocol
    - "I know it got there"
    - 3-Way Handshake (SYN, SYN-ACK, ACK)
    - Used when reliable communication is needed
    - Examples: HTTP, FTP, SSH

- **TCP Windowing**
  - TCP keeps packets in order with sequence numbers
  - Data being sent is broken into packets starting at ~1500bytes
  - If the packet is received successfully, packet size increases
  - Packet size continues to increase until data is lost in transit
  - If data is lost, packet size decreases until transfer stabilizes
  - Packets are ACKed as they are received by their sequence numbers

- **Wireshark**
  - Allows user to view network traffic
  - Available at ```www.wireshark.org```
  - Allows expressions to filter traffic
    - Example: ```ip.addr == XX.XX.XX.XX```

- **nslookup**
  - Allows you to ask questions to DNS

---
 
[Back to main](https://github.com/rot0xd/CBTNuggets/blob/master/CCNA/ICND-1/README.md)

