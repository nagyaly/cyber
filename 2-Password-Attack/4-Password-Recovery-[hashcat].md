# Advanced Password Recovery [hashcat]
<img src="https://www.kali.org/tools/hashcat/images/hashcat-logo.svg" style="width:120px;"/>

Hashcat is the world’s fastest CPU-based password recovery tool. supports  hashing  algorithms like Microsoft LM Hashes, MD4, MD5, SHA-family, Unix Crypt formats, MySQL, Cisco PIX.. and more.

---

### 1- Discover Current network pereference
`hashcat -a 0 -m 1800 hash.txt wordlist.txt`

- `-a` is the `straight` attack mode (check `man hashcat` for other modes)
- `-m` is the `sha512crypt` hash type (check `man hashcat` for other types)
- `hash.txt` contain the password hash, this command extract generate a hash for testing purpose `mkpasswd -m sha-512 nagy SALTSALT > hash.txt`
- `wordlist.txt` assuming you generated a wordlist using crunch.


hashcat will display the recovered password beside the hash`$6$SALTSALT$goXKGsfeMZ8Z/wKe7Z1nSxtXwZy6rH5eW3YgjjhodhTfkv.kYBHzbr3sbDlGLLc/pXKz0WeLOgT5Dx94xP2YU/:nagy`

```
hashcat (v6.2.6) starting

OpenCL API (OpenCL 3.0 PoCL 6.0+debian  Linux, None+Asserts, RELOC, LLVM 17.0.6, SLEEF, POCL_DEBUG) - Platform #1 [The pocl project]
====================================================================================================================================
* Device #1: cpu--0x000, 1082/2228 MB (512 MB allocatable), 2MCU

Minimum password length supported by kernel: 0
Maximum password length supported by kernel: 256

Hashes: 1 digests; 1 unique digests, 1 unique salts
Bitmaps: 16 bits, 65536 entries, 0x0000ffff mask, 262144 bytes, 5/13 rotates
Rules: 1

Optimizers applied:
* Zero-Byte
* Single-Hash
* Single-Salt
* Uses-64-Bit

ATTENTION! Pure (unoptimized) backend kernels selected.
Pure kernels can crack longer passwords, but drastically reduce performance.
If you want to switch to optimized kernels, append -O to your commandline.
See the above message to find out about the exact limits.

Watchdog: Hardware monitoring interface not found on your system.
Watchdog: Temperature abort trigger disabled.

Host memory required for this attack: 0 MB

Dictionary cache built:
* Filename..: wordlist.txt
* Passwords.: 256
* Bytes.....: 1280
* Keyspace..: 256
* Runtime...: 0 secs

$6$SALTSALT$goXKGsfeMZ8Z/wKe7Z1nSxtXwZy6rH5eW3YgjjhodhTfkv.kYBHzbr3sbDlGLLc/pXKz0WeLOgT5Dx94xP2YU/:nagy

Session..........: hashcat
Status...........: Cracked
Hash.Mode........: 1800 (sha512crypt $6$, SHA512 (Unix))
Hash.Target......: $6$SALTSALT$goXKGsfeMZ8Z/wKe7Z1nSxtXwZy6rH5eW3Ygjjh...xP2YU/
Time.Started.....: Sun Nov 17 10:14:58 2024 (0 secs)
Time.Estimated...: Sun Nov 17 10:14:58 2024 (0 secs)
Kernel.Feature...: Pure Kernel
Guess.Base.......: File (wordlist.txt)
Guess.Queue......: 1/1 (100.00%)
Speed.#1.........:      111 H/s (5.19ms) @ Accel:32 Loops:512 Thr:1 Vec:2
Recovered........: 1/1 (100.00%) Digests (total), 1/1 (100.00%) Digests (new)
Progress.........: 32/256 (12.50%)
Rejected.........: 0/32 (0.00%)
Restore.Point....: 0/256 (0.00%)
Restore.Sub.#1...: Salt:0 Amplifier:0-1 Iteration:4608-5000
Candidate.Engine.: Device Generator
Candidates.#1....: nnnn -> nayy

Started: Sun Nov 17 10:14:51 2024
Stopped: Sun Nov 17 10:14:59 2024
```

---
> For more questions email: nagy@aast.edu