# Password Recovery [John the Ripper]
<img src="https://www.kali.org/tools/john/images/john-logo.svg" style="width:120px;"/>

John the Ripper is a tool designed to help systems administrators to find weak (easy to guess or crack through brute force) passwords, and even automatically mail users warning them about it, if it is desired.

---

### 1- Unshadow the password file

In linux user informations are stored in `/etc/paswwd` and hashed passwords are stored in `/etc/shadow`. we need to combine both so `john` can understand it.

`sudo cat /etc/passwd | grep nagy > passwd.txt`
```
nagy:x:1000:1000:Nagy Khairat,,,:/home/nagy:/usr/bin/zsh
```


`sudo cat /etc/shadow | grep nagy > shadow.txt`
```
nagy:$y$j9T$55/6AvAszIb50QynSpUfM0$F2fosqL1KLOyyTqceeasliCVNR9tlvnROXF5KzgfJR9:20040:0:99999:7:::
```

`unshadow passwd.txt shadow.txt > unshadow.txt`
```
nagy:$y$j9T$55/6AvAszIb50QynSpUfM0$F2fosqL1KLOyyTqceeasliCVNR9tlvnROXF5KzgfJR9:1000:1000:Nagy Khairat,,,:/home/nagy:/usr/bin/zsh
```

---

### 2- Crack the weak password
`john --wordlist=wordlist.txt unshadow.txt`

assuming you generated a wordlist using crunch.
```
Using default input encoding: UTF-8
No password hashes loaded (see FAQ)
```

sometimes John needs a little help with detecting the hash format

`john --wordlist=wordlist.txt unshadow.txt --format=crypt`
```
Created directory: /root/.john
Using default input encoding: UTF-8
Loaded 1 password hash (crypt, generic crypt(3) [?/64])
Cost 1 (algorithm [1:descrypt 2:md5crypt 3:sunmd5 4:bcrypt 5:sha256crypt 6:sha512crypt]) is 0 for all loaded hashes
Cost 2 (algorithm specific iterations) is 1 for all loaded hashes
Will run 2 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
nagy             (nagy)
1g 0:00:00:01 DONE (2024-11-17 01:37) 0.6097g/s 117.0p/s 117.0c/s 117.0C/s nnyn..aggy
Use the "--show" option to display all of the cracked passwords reliably
Session completed.
```

as we can see, we retreived the weak password of the user `nagy` which is also `nagy`