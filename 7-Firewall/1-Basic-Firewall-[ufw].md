## Basic Firewall [ufw]

<img src="https://cdn4.iconfinder.com/data/icons/devine_icons/Black/PNG/System%20and%20Internet/Firewall.png" style="width:120px;"/>

UFW (Uncomplicated Firewall) is a user-friendly command-line interface for managing the Linux firewall. It simplifies the configuration of iptables, making it easier for users to define rules for allowing or blocking network traffic based on source/destination addresses, ports, and protocols.


------------------------------------------------------------------------------
### 1- install ufw on debian based linux

`sudo apt install -y ufw`

------------------------------------------------------------------------------
### 2- check ufw state
`sudo ufw status`

```bash
Status: inactive
```
Or if the firewall is active
```bash
Status: active

To                         Action      From
--                         ------      ----
Bind9                      ALLOW       Anywhere
Bind9 (v6)                 ALLOW       Anywhere (v6)
```
------------------------------------------------------------------------------
### 2- Enable/disable the firewall
to enable `sudo ufw enable` \
to disable `sudo ufw disable`

>[!NOTE]
>$\color{#4492f8}\textsf{You may prompt with the following if you are connected via ssh, just reply with yes (y)}$\
>Command may disrupt existing ssh connections. Proceed with operation (y|n)?

```bash
Firewall is active and enabled on system startup
```

------------------------------------------------------------------------------
### 3- ufw parameters

- Direction:
  + `from`      ingoing
  + `to`      outgoing

- Target:
  + `allow`     allow connection
  + `deny`      drop the packets
  + `reject`    reject the packet (the user get notified)
  + `limit`     allow but limit the rate to 6 connections per 30 seconds (to avoid logon brute force)

- Protocol
  + `proto tcp`
  + `proto udp`

- Protocol
  + `proto tcp`
  + `proto udp`

- Interface
  + `in on eth0` specify the interface eth0

------------------------------------------------------------------------------
### 4- Basic Examples
- Block all incoming connection from the host `192.160.70.5` \
  `sudo ufw deny from 192.160.70.5`

- Block all incoming connections from the entire subnet \
  `sudo ufw deny from 192.160.70.0/24`

- Enable the connections from the specified host \
`sudo ufw allow from 192.160.70.5`

- Block all incoming connection from the host on the interface `eth0` \
`sudo ufw deny in on eth0 from 192.160.70.5`

- Allow incoming connection from the host `192.160.70.5` to port `22` \
`sudo ufw allow from 192.160.70.5 to any port 22`

- Allow incoming connection from the host `192.160.70.5` to port `22` with protocol `tcp` \
`sudo ufw allow from 192.160.70.5 proto tcp to any port 22`

- Allow incoming connection from any host on port `80` and `443` with protocol `tcp` \
`sudo ufw allow proto tcp from any to any port 80,443`

- Block outgoing connections on port 25 (SMTP Mail) \
`sudo ufw deny out 25`


------------------------------------------------------------------------------
### 5- list all rules
`sudo ufw status`
```bash
Output
Status: active

To                         Action      From
--                         ------      ----
Anywhere                   DENY        192.160.70.5
```

------------------------------------------------------------------------------
### 6- Delete a rule
you can delete a specific rule by doing the following

`sudo ufw delete allow from 192.160.70.5`

or by index, you can list all the rules with index using `sudo ufw status numbered`
```bash
Output
Status: active

     To                     Action      From
     --                     ------      ----
[1] Anywhere                DENY IN     192.160.70.0/24          
[2] Anywhere                ALLOW IN    192.160.70.5
```

and delete by index `sudo ufw delete 2`

------------------------------------------------------------------------------
### 7- Application Profile

Applications that rely on network communications will typically set up a UFW profile such as ssh or nginx web server

To list available application profile `sudo ufw app list`
```bash
Available applications:
  Bind9
  Nginx HTTP
  OpenSSH
```

To enable a specific profile `sudo ufw allow OpenSSH`

Profile rule can be deleted same as regular rules `sudo ufw delete allow OpenSSH`

------------------------------------------------------------------------------
> For more questions email: nagy@aast.edu
