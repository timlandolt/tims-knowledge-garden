---
{"dg-publish":true,"permalink":"/knowledge/tcp-and-udp/","tags":["protocol","tcp","udp"]}
---

---

**TCP** = Transmission Control Protocol
**UDP** = User [Datagram](https://en.wikipedia.org/w/index.php?title=Datagram&oldid=1308928916&useskin=vector) Protocol

Both are core [[transport layer\|transport layer]] protocols in computer networking.

| TCP                                                                      | UDP                                                                               |
| ------------------------------------------------------------------------ | --------------------------------------------------------------------------------- |
| **Connection Oriented**<br>= A connection has to be established & closed | **[[Datagram\|Datagram]] Oriented**<br>= No connection => easy broadcasting                 |
| Guarantees data delivery                                                 | Cannot guarantee the delivery                                                     |
| Extensive error-checking                                                 | Error-checking with basic checksums                                               |
| Acknowledgment segment is present                                        | No acknowledgement segment                                                        |
| Data arrives in correct sequence                                         | No sequencing by default, it needs to be implemented in the [[application layer\|application layer]] |
| Relatively slow                                                          | Faster                                                                            |
| Lost packages can be retransmitted                                       | Retransmission is not possible                                                    |
| 20-60 byte header                                                        | 8 byte header                                                                     |
| Uses handshake                                                           | Is connectionless => no handshake                                                 |
| No broadcasting supported                                                | Supports broadcasting                                                             |
| Used by: [[Knowledge/HTTP\|HTTP]], HTTPS, FTP, SMTP, Telnet                              | Used by: DNS, DHCP, TFTP, SNMP, RIP, VoIP                                         |



