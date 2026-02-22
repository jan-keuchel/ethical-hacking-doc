# What to do when stuck in pentesting

## Situations

### Brute forcing
- Try different wordlist
    - `/usr/share/wordlists/rockyou.txt`
    - `/usr/share/wordlists/fasttrack.txt`
    - `/usr/share/seclists/Passwords/Common-Credentials/best110.txt`

### Enumeration
- Scan all ports with `nmap`
- Try logging in with default credentials or `anonymous` on every service

### Local enumeration
- Look for database files. Might contain password hashes or usernames
- Read the description of expoitls on exploitDB
