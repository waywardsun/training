#### Video 29 Exercises

##### Network Scanning Tools

---

## `nmap`

#### `nmap` usage examples
```
# Basic nmap scan on a single host
root@bt:~# nmap 192.168.1.24

# Ping scan
root@bt:~# nmap -sP 192.168.1.*
root@bt:~# nmap -sP 192.168.1.1-254
root@bt:~# nmap -sP 192.168.1.1/24

# -sS = Syn Scan
# -P0 = Protocol scan (check all protocols (TCP, UDP, ICMP, etc))
# -sV = Attempt to detect version of operating system/services found
# -O  = Attempt to detect operating system
root@bt:~# nmap -sS -P0 -sV -O 192.168.1.0-50

# Don't wait long for responses
root@bt:~# nmap -T5 192.168.1.0/24

# Scan only the top 20 common ports
root@bt:~# nmap --top-ports 20 192.168.1.0/24

# Find out who is running web services on port 80
# -sT = perform a TCP connect scan
root@bt:~# nmap -sT -p 80 192.168.1.1-50

# -sS = TCP SYN scan
# -D  = Decoy mode. Send actual request along with decoy requests using provided IPs.
root@bt:~# nmap -sS 192.168.1.1-5 -D 192.168.1.98,192.168.1.99

# Scan with verbose output
root@bt:~# nmap -v 192.168.1.1

# -F  = Same as '--top-ports 100'
# Don't scan 192.168.1.1,192..168.1.2
root@bt:~# nmap -F 192.168.1.0/24 --exclude 192.168.1.1,192.168.1.2

# -Pn = Assume all hosts are running, don't bother pinging to see if up
root@bt:~# nmap -Pn 192.168.1.6

# -6  = Use IPv6
root@bt:~# nmap -6 2001:db8:6783:1::1

# List local interfaces and addresses associated with them
root@bt:~# nmap --iflist

# -A  = Enable OS detection, version detection, script scanning, and traceroute
root@bt:~# nmap -A -T4 192.168.1.1
```

#### `nmap` Scripting Engine (NSE)
```
# Use default NSE scripts for services found
root@bt:~# nmap --script=default 192.168.1.24

# -sC = Shortcut for running default scripts
root@bt:~# nmap -sC 192.168.1.24

# Get help on all scripts in the discovery group
root@bt:~# nmap --script-help discovery

# Run all scripts in the groups safe and default
root@bt:~# nmap --script="safe or default" 192.168.1.24

# Run scripts that are included in both discovery and version groups
root@bt:~# nmap --script="discovery and version" 192.168.1.24
```

---

## `scapy`

- Scapy usages:
  - written in python
  - used for packet manipulation
    - capture
    - create
    - play
    - replay
    - scan
    - discover
  - scapy prompt
    - To exit, press `ctrl+d`
    - To view contents of headers: `L3.show()` where L3 is the variable name
    - `send(IP(src="192.168.1.55",dst="192.168.1.1")/ICMP()/"OurPayload")`
      - Sending a packet
        - source address of `192.168.1.55`
        - destination address of `192.168.1.1`
        - uses ICMP with data of "OurPayload"

#### Sending a packet
```
>>> L2 = Ether(src="01:23:45:67:89:ab")
>>> L2.show()
>>> L3 = IP(ttl=99,dst="192.168.1.1")
>>> L3.show()
>>> L3.dst="192.168.1.2"
>>> L3.show()
>>> L4 = TCP(sport=6783, dport=22, flags="A")
>>> L4.show()
>>> send=sendp(L2/L3/L4)
```

#### Sniffing traffic
```
>>> sniff(iface="eth0", prn=lambda x: x.show())
>>> sniff(iface="eth0", prn=lambda x: x.summary())
>>> sniff(filter="host 192.168.1.1", count=5)
>>> a=_
>>> a.nsummary()
>>> a[1]
```

---

## `hping3`

- hping3
  - used for:
    - Port Scanning
      - SYN, ACK, IP, others
    - Host Discovery
    - Fingerprinting
    - Sniffer
    - Flooding
    - File Transfer
  - usage examples
    - `hping3 -S $HOST -p $PORT -c $COUNT`
      - `-S` - sets SYN flag
      - `$HOST` - the host to ping
      - `-p $PORT` - the port to scan
      - `-c $COUNT` - the number of packets to send
    - `hping3 -S $HOST -p ++50 -c $COUNT`
      - `-S` - sets SYN flag
      - `$HOST` - the host to ping
      - `-p ++50` - start with port 50 and increment for each packet sent
      - `-c $COUNT` - the number of packets to send
    - `hping3 -1 192.168.1.x --rand-dest -I eth0`
      - `-1` uses traditional ICMP
      - `192.168.1.x` - scans all IPs in subnet
      - `--rand-dest` - don't do the scan in order
      - `-I eth0` - specifies the interface to send packets out of
    - `hping3 -1 $HOST --icmp-ts -c $COUNT`
      - `-1` uses traditional ICMP
      - `$HOST` - the host to ping
      - `icmp-ts` - shows timestamps      
      - `-c $COUNT` - the number of packets to send
    - `hping3 -8 50-56 -S $HOST`
      - `-8` uses Scan mode
      - `50-56` - scan from ports 50-56
      - `$HOST` - the host to ping
    - `hping3 -2 $HOST -p $PORT -c $COUNT`
      - `-2` - uses UDP
      - `$HOST` - the host to ping
      - `-p $PORT` - the port to scan
      - `-c $COUNT` - the number of packets to send
    - `hping3 -F -P -U $HOST -c $COUNT`
      - `-F` - sets the FIN flag
      - `-P` - sets the PSH flag
      - `-U` - sets the URG flag
      - `$HOST` - the host to ping
      - `-c $COUNT` - the number of packets to send
    - `hping3 $HOST -Q -p 139 -S`
      - `$HOST` - the host to ping
      - `-Q` - Show the sequence numbers
      - `-p 139` - send the packet to port 139
      - `-S` - sets SYN flag
   - `hping3 -S $HOST1 -a $HOST2 -p 22 --flood`
      - `-S` - sets SYN flag
      - `$HOST1` - the host to ping
      - `-a $HOST2` - set the source address of the packet (spoof ip)
      - `-p 22` - send the packet to port 22
      - `--flood` - Send as many packets as we can to this destination
    - `hping3 -2 $HOST -p ++44444 -T -n`
      - `-2` - sets UDP mode
      - `$HOST` - the destination host
      - `-p ++44444` - start with port 44444 and increment for each packet sent
      - `-T` - sets traceroute mode
        - `ctrl-z` will skip a hop if it is not responding
      - `-n` - Don't attempt to do name resolution
    - `hping3 -S $HOST -p 53 -T`
      - `-S` - sets SYN flag
      - `$HOST` - the destination host
      - `-p 53` - send the packet to port 53
      - `-T` - sets traceroute mode
        - `ctrl-z` will skip a hop if it is not responding
    - `hping3 -S $HOST -p 80 -T --ttl 13 --tr-keep-ttl -n`
      - `-S` - sets SYN flag
      - `$HOST` - the destination host
      - `-p 80` - send the packet to port 80
      - `-T` - sets traceroute mode
        - `ctrl-z` will skip a hop if it is not responding
      - `--ttl 13` - set the ttl to 13
      - `--tr-keep-ttl` - do not change the ttl
      - `-n` - Don't attempt to do name resolution
    - `hping3`
      - interactive mode
      - sample:
        - `hping send "ip(saddr=192.168.1.55,daddr=192.168.1.38,ttl=15)+tcp(sport=6783,dport=80,flags=s)"`

---

[Back to main](https://github.com/rot0xd/CBTNuggets/blob/master/CEHv9/README.md)

