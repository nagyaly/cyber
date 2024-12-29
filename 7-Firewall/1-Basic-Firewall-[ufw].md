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

```bash
Status: active

To                         Action      From
--                         ------      ----
Bind9                      ALLOW       Anywhere
Bind9 (v6)                 ALLOW       Anywhere (v6)
```
---
### 2- enable ufw
`sudo ufw enable`


>[!TIP]
>you may prompt with the following if you are connected via ssh, just reply with yes (y)
>```
>Command may disrupt existing ssh connections. Proceed with operation (y|n)?
>```

```bash
Firewall is active and enabled on system startup
```
