# Nmap Cheatsheet for Ethical Hacking

## Scan Types

- `-sS` : SYN (Stealth) scan (default, fast and unobtrusive)
- `-sT` : TCP connect scan (used when SYN is not possible)
- `-sU` : UDP scan
- `-sN` : TCP Null scan
- `-sF` : FIN scan
- `-sX` : Xmas scan
- `-sA` : ACK scan - check for ports unfiltered by the firewall
- `-sW` : window scan - check for ports unfiltered by the firewall

## Options
- `-T[1,2,3,4,5]` speed

## Port Scanning Techniques

* `-p <ports>` : Scan specific ports (e.g., `-p 22,80,443`, `-p20-80` or `-p-` for all 65535)
* `-F` : Fast scan (default top 100 ports)
* `--top-ports <n>` : Scan top N ports

## Version Detection

```bash
nmap -sV <target>
```
- Nmap completes 3WH and tries to detect the Version of the service

## OS Detection

```bash
nmap -O <target>
```

- OS detection based on TCP/IP stack behavior
- Combine with `-v` and `--osscan-guess` for verbose guessing

## Aggressive Scan

```bash
nmap -A <target>
```

- Enables: OS detection, version detection, script scanning, and traceroute
- Good overview, but noisy

## Output Options

- `-oN <file>` Normal output
- `-oX <file>` XML output
- `-oG <file>` Grepable output
- `-oA <basename>` Output in all formats with given base name

## Script Scanning (NSE)

* `-sC` Run default scripts
* `--script \<name/category>` Run specific scripts
* `--script-args <args>` Provide arguments to scripts
* `--script-help <script>` Show script description
* Scripts are stored at `/usr/share/nmap/scritps`

## Other information

* `--reason` List how the state of the port was determined

Examples:

```bash
nmap -sC -sV <target>
nmap --script=vuln <target>
nmap --script=http-enum <target>
nmap -p 445 --script=smb-enum-shares.nse,smb-enum-users.nse <target> # enumerate samba shares
nmap -p 111 --script=nfs-ls,nfs-statfs,nfs-showmount MACHINE_IP # enumerate nfs
```

## Scan Examples

```bash
nmap -T4 -p- -A $IP
```

```bash
# Basic scan
nmap 192.168.0.1

# Scan multiple targets
nmap 192.168.0.1 192.168.0.2
nmap 192.168.0.1-10
nmap 192.168.0.0/24

# Stealth scan with version detection
nmap -sS -sV 192.168.0.1

# Full TCP port scan
nmap -p- 192.168.0.1

# OS and service detection
nmap -O -sV 192.168.0.1

# Aggressive scan
nmap -A 192.168.0.1

# Evade firewall with decoys
nmap -D RND:10 192.168.0.1

# UDP scan
nmap -sU -p 53,67,123 192.168.0.1

# Script scan for vulnerabilities
nmap --script vuln 192.168.0.1
```
