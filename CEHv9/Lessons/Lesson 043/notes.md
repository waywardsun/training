#### Video 43 Notes

##### SMTP Enumeration

---

- Simple Mail Transfer Protocol (SMTP)
  - Ports associated with e-mail
    - POP3 TCP:110 for plaintext, TCP/995 for encrypted
    - IMAP TCP:143 for plaintext, TCP/993 for encrypted
    - SMTP TCP:25
  - Can slow down enumeration of an attacker using teer grube (tarpit) approach

#### Sample SMTP enumeration flow
```
root@kali:~# nslookup smtp.cox.net
Server:         8.8.8.8
Address:        8.8.8.8#53

Non-authoritative answer:
Name:   smtp.cox.net
Address: 68.6.19.8

root@kali:~# telnet 68.6.19.8 25
Trying 68.6.19.8...
Connected to 68.6.19.8
Escape character is '^]'.
220 fed1rmimpo209.cox.net cox ESMTP server ready
HELO
501 HELO requires valid address
HELO OurTest.com
250 fed1rmimpo209.cox.net hello [70.180.202.69], pleased to meet you
MAIL FROM:bob@cox.net
250 2.1.0 <bob@cox.net> sender ok
RCPT TO:jon@cox.net
250 2.1.0 <jon@cox.net> recipient ok
^]
root@kali:~# smtp-user-enum -M RCPT -u bob@cox.net -t smtp.cox.net
```

---

[Back to main](https://github.com/rot0xd/CBTNuggets/blob/master/CEHv9/README.md)

