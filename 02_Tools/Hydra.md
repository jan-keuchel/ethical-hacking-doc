# THC-Hydra

## Basics

## Syntax

```bash
hydra [OPTIONS] -L [userlist] -P [passlist] [PROTOCOL]://[TARGET]
```

- `-L <file>` Path to file with list of usernames
- `-l <username>` Single username
- `-P <file>` Path to file with list of passwords
- `-p <password>` Single password
- `-s <num>` Port (if non-default)
- `-t <num>` Number of parallel connections (default: 16)
- `-V` Verbose mode (shows every attempt)
- `-f` Exit after the first valid login
- `-o <file>` Specify the output file

---

## Examples

### SSH

```bash
hydra -l root -P passwords.lst $IP -t 4 ssh
```

### FTP

```bash
hydra -l user -P passwords.lst ftp://$IP
```

### HTTP POST Form (Custom Login Form)

```bash
hydra -L users.txt -P passwords.txt 192.168.1.100 http-post-form \
"/login.php:username=^USER^&password=^PASS^:F=incorrect"
```

- The string is built up like this: `<path>:<post-data>:<condition>[:optional-elements]`
- The `post-data` are the URL-encoded fields of the given form.
- **F**ailure and **S**uccess conditions can be specified with the `F=<string>` and the `S=<string>` option.
- Both failure and success condition are a string for which hydra searches on the resulting page. If the string is present the condition is met.

### SMB

```bash
hydra -L users.txt -P passwords.txt smb://192.168.1.100
```

---
### Usefull commands

Run `hydra -U <module>` to see further information on a specific module.

---

## Logging Results

```bash
hydra -L users.txt -P passwords.txt -o results.txt ssh://192.168.1.100
```

---

## References

* [Hydra GitHub Repository](https://github.com/vanhauser-thc/thc-hydra)
* [THC Hydra Usage Guide (HackTricks)](https://book.hacktricks.xyz/pentesting/password-cracking/thc-hydra)
* [SecLists – User/Password Wordlists](https://github.com/danielmiessler/SecLists)
