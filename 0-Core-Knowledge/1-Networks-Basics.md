# Networks Basics

## Internet Protocol (IP)
The Logical Address or the machine address on the network, for example: 192.168.1.10. consists of 4 numbers seperated by 3 dots.
``` 
IPv4 = 32 bits range (4 octets of 8 bits, from 0-255 each(4))

11000000.10101000.00000001.00001010   [IPv4 binary]
   192  .   168  .   1   .  10        [IPv4 decimal]
```
you can get your IP by typing `ifconfig` in the terminal on linux or `ipconfig` in the command prompt on windows

## MAC Address (Media Access Control)
The physical address that uniquely identifies the machine, associated with the Network Interface Card (NIC).

## Port
Entry or exit to the machine, used to organize communication of different processes on the same machine. \
Each machine has 2<sup>16</sup> = 65,535 valid port, but some ports are reserved for certain protocol. \
usually dynamic port are >= 49,152
| port | protocol | Abbreviation |
| - | - | - |
| 80 | HyperText Transfer Protocol | HTTP |
| 443 | HyperText Transfer Protocol Secured | HTTPS |
| 20/21 | File Transfer Protocol | FTP |
| 22 | Secure Shell | SSH |
| 23 | Telnet | Telnet |
| 25 | Simple Mail Transfer Protocol | SMTP |
| 53 | Domain Name System | DNS |
| 3306 | MySQL Database | MySQL |
| 3389 | Remote Desktop Protocol | RDP |

## Node
Refer to any machine connected on the network.

## Packet
A data sent between nodes on the network

## Router
A hardware device that manages to communication between nodes within the network and to other networks.

## Dynamic Host Configuration Protocol (DHCP)
Protocol used to distribute IPs to nodes on the network, usually implemented in the router.

## Network Area Translation (NAT)
A method used by the router to provide network access to nodes with fewer public IPs. by providing the internal devices with private IPs, and are mapped to another public IPs. and multiple nodes can share the same public IP. but with different private IPs.


## Subnet
subnetting is a way to divide the network available addressed to smaller seperate sub-network called subnets. by using a subnet mark to divide the IP to network ID and nodes portion. for example the subnet mask `255.255.255.0` divide the IP `192.168.1.10` to `192.168.1.x` to be the network ID, and `192.168.1.0` to `192.168.255` are available for nodes on this network. \
The subnect mask can also be written as a number after the IP, for example: `192.168.1.10/24` where 24 is the number of 1s from the left.
```
11111111.11111111.11111111.00000000
   255  .   255  .  255   .   0     
```

## Transmission Control Protocol/Internet Protocol (TCP/IP)
Communication standard that enable data to bet transmitted between processes/application and nodes on the network. by breaking down the message into organized data packets. \
TCP uses a three-way handshake to establish a reliable connection that guarantee packets integrity, delivery and order of arrival.
| Flag | Name | Function |
| - | - | - |
| SYN  | Synchronize | initialize communication and negotiating of parameters and sequence numbers |
| ACK  | Acknowledgment | Acknowledgement to the SYN flag.  Always sent after initial SYN |
| RST  | Reset | Forces termination for the connection |
| FIN  | Finish | Close to communications |
| PSH  | Push | Forces the delivery and ignore buffering |
| URG  | Urgent | Data inside is being sent out of band.  Example is cancelling a message |

## User Datagram Protocol (UDP)
A simpler form of data transport protocol that provide data corruption detection, but does not guarrantee the packet loss of order or arrival, usually ussed in streamming appliations, where speed is more important than accuracy.

## Address Resolution Protocol (ARP)
A layer 2 protocol used to map MAC addresses to IP addresses on the network


---
> For more questions email: nagy@aast.edu