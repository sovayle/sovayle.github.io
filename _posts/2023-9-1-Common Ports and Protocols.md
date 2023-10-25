---
title: "Common Ports and Protocols"
categories: knowledge
permalink: /blogs/common-ports-and-protocols
#header:
#  teaser: /assets/images/white.jpg
---

# Port numbers

**TCP**
* FTP 21
* SSH 22
* Telnet 23
* SMTP 25
* DNS 53
* HTTP 80 HTTPS 443
* POP3 110
* NETBIOS windows 139
* SMB 139 + 445 (fileshares)
* wannacry, SMB, 445
	* SAMBA, _v important in kali_
* IMAP 143

**UDP**
* DNS 53
* DHCP 67,68
* TFTP 69 (trivial ftp)
* SNMP 161 (simple network management protocol)

# IP addresses
> ifconfig
> inet is the ip
> 32 bits = 4 bytes
-   210.48.222.13 18 july
-   inet 192.168.244.128
- privates? 10 ALL
- 172.16 -172.31.255.255
- 192 168 - 192.168.255.255

### Table:
- A 0-127
- B 128-191
- C 192-223
- D 224-239
- E 240-255

## Media Access Control
>ether 00:0c:29     :eb:29:ab
>first 3 is identifiers
>ie this vmware
### Transmission Control Protocol
> TCP VS UDP
>  USER DATAGRAM PROTOCOL
>  SYN > SYN ACK > ACK
>  port http:80 443:https