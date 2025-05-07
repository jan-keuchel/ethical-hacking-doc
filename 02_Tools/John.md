
# John the Ripper Cheatsheet for Ethical Hacking

## Table of Contents

* [Introduction](#introduction)
* [Basic Usage](#basic-usage)
* [Common Modes](#common-modes)
* [Password Hash Formats](#password-hash-formats)
* [Cracking Modes](#cracking-modes)
* [Rules & Wordlists](#rules--wordlists)
* [Working with Hashes](#working-with-hashes)
* [Session Management](#session-management)
* [Advanced Usage](#advanced-usage)
* [Utilities](#utilities)
* [Tips & Tricks](#tips--tricks)

---

## Basic Usage

> Tool path: `/usr/bin/john` (or `./john` in extracted directory)

```bash
john <hashfile>                         # Crack hashes using default wordlist
john --wordlist=<wordlist> <hashfile>   # Use a custom wordlist
john --format=<type> <hashfile>         # Specify hash type explicitly
```

## Common Modes

* **Single Crack Mode**: Attempts using info from username, GECOS fields
* **Wordlist Mode**: Uses a wordlist to guess passwords
* **Incremental Mode**: Brute-force all possible password combinations

```bash
john --single <hashfile>
john --wordlist=rockyou.txt <hashfile>
john --incremental <hashfile>
```

## Password Hash Formats

Specify with `--format=<type>`:

| Format      | Description               |
| ----------- | ------------------------- |
| raw-md5     | Plain MD5 hash            |
| raw-sha1    | SHA-1 hash                |
| sha512crypt | Linux SHA-512 /etc/shadow |
| bcrypt      | bcrypt hashes             |
| NT          | Windows NTLM hashes       |
| zip         | Zip file passwords        |

List supported formats:

```bash
john --list=formats
```

## Cracking Modes

```bash
john --single <hashfile>                    # Single mode
john --wordlist=rockyou.txt <hashfile>      # Wordlist mode
john --incremental <hashfile>               # Incremental mode (brute force)
```

Incremental brute-force can also be customized:

```bash
john --incremental=Digits <hashfile>
```

## Rules & Wordlists

Enable transformation rules:

```bash
john --wordlist=rockyou.txt --rules <hashfile>
```

Use custom rule section:

```bash
john --wordlist=rockyou.txt --rules=CustomRule <hashfile>
```

Define rules in `john.conf` or `john.ini` under `[List.Rules:CustomRule]`

## Working with Hashes

### Creating Hashes

```bash
echo -n "password" | openssl passwd -1 -stdin      # MD5 crypt
mkpasswd --method=sha-512                          # SHA-512 crypt
```

### Extracting Hashes

```bash
unshadow /etc/passwd /etc/shadow > myhashes.txt    # For Linux
```

### Format for NTLM hash (Windows):

```
<username>:<uid>:<NTLM_hash>:::
```

## Session Management

```bash
john --session=<name> ...            # Start session
john --restore=<name>                # Resume session
john --status=<name>                 # Check progress
```

## Advanced Usage

```bash
john --format=NT --wordlist=rockyou.txt --rules hash.txt
john --show hash.txt                               # Show cracked passwords
john --users=jan --wordlist=rockyou.txt hash.txt   # Crack only for user 'jan'
john --incremental=All --min-length=6 --max-length=8 hash.txt
```

## Utilities

### unshadow

Combine passwd and shadow files:

```bash
unshadow /etc/passwd /etc/shadow > hashes.txt
```

### zip2john, rar2john, pdf2john

Convert encrypted files to crackable format:

```bash
zip2john file.zip > zip.hash
john zip.hash
```

### Other tools

* `ssh2john.py`: Extract from SSH private key
* `gpg2john.py`: Extract from GPG private key
* `keepass2john.py`: Extract from KeePass database

## Tips & Tricks

* Run with verbosity:

```bash
john --verbosity=5 hash.txt
```

* Resume interrupted session:

```bash
john --restore
```

* Save cracked passwords:

```bash
john --show hash.txt
```

* Clean session:

```bash
rm john.pot john.log
```
