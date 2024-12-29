## Basic Firewall [ufw]

<img src="https://cdn4.iconfinder.com/data/icons/devine_icons/Black/PNG/System%20and%20Internet/Firewall.png" style="width:120px;"/>

UFW (Uncomplicated Firewall) is a user-friendly command-line interface for managing the Linux firewall. It simplifies the configuration of iptables, making it easier for users to define rules for allowing or blocking network traffic based on source/destination addresses, ports, and protocols.


---
### 1- install ufw on debian based linux

`sudo apt install -y ufw`

---
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
---
### 2- Enable/disable the firewall
`sudo ufw enable`

>[!NOTE]
>$\color{#4492f8}\textsf{You may prompt with the following if you are connected via ssh, just reply with yes (y)}$\
>Command may disrupt existing ssh connections. Proceed with operation (y|n)?

```bash
Firewall is active and enabled on system startup
```

---
### 3- Specify Direction
you may used the firewall to allow/deny specific connection ingoing `IN` or outgoing `to` specific hosts or subnet.

the following will block all incoming connection from the host `192.160.70.5`
`sudo ufw deny from 192.160.70.5`

---
### 4- block a subnet
The following command will block all incoming connections from the entire subnet

`sudo ufw deny from 192.160.70.0/24`

---
### 5- enable a host
The following command will enable the connections from the specified host

`sudo ufw allow from 192.160.70.5`

---
### 6- specify the network interface

the following will block all incoming connection from the host on the interface `eth0`

`sudo ufw deny in on eth0 from 192.160.70.5`

---
### 7- list all rules
`sudo ufw status`
```bash
Output
Status: active

To                         Action      From
--                         ------      ----
Anywhere                   DENY        192.160.70.5
```

---
### 8- Delete a rule
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
