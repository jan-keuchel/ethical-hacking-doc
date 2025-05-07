# Nmap Cheatsheet for Ethical Hacking

## Table of Contents

* [Basic Scanning](#basic-scanning)
* [Scan Types](#scan-types)
* [Port Scanning Techniques](#port-scanning-techniques)
* [Service and Version Detection](#service-and-version-detection)
* [OS Detection](#os-detection)
* [Aggressive Scan](#aggressive-scan)
* [Firewall Evasion and Spoofing](#firewall-evasion-and-spoofing)
* [Output Options](#output-options)
* [Script Scanning (NSE)](#script-scanning-nse)
* [Scan Examples](#scan-examples)

---

## Basic Scanning

```bash
nmap <target>
```

Examples:

```bash
nmap 192.168.1.1
nmap scanme.nmap.org
```

## Scan Types

* **-sS** : SYN (Stealth) scan (default, fast and unobtrusive)
* **-sT** : TCP connect scan (used when SYN is not possible)
* **-sU** : UDP scan
* **-sN** : TCP Null scan
* **-sF** : FIN scan
* **-sX** : Xmas scan
* **-sA** : ACK scan

## Port Scanning Techniques

* **-p <ports>** : Scan specific ports (e.g., -p 22,80,443 or -p- for all 65535)
* **-F** : Fast scan (default top 100 ports)
* **--top-ports <n>** : Scan top N ports
* **--port-ratio <ratio>** : Scan ports more likely to be open

## Service and Version Detection

```bash
nmap -sV <target>
```

* Detect service versions
* Combine with `-p` to scan specific ports

## OS Detection

```bash
nmap -O <target>
```

* OS detection based on TCP/IP stack behavior
* Combine with `-v` and `--osscan-guess` for verbose guessing

## Aggressive Scan

```bash
nmap -A <target>
```

* Enables: OS detection, version detection, script scanning, and traceroute
* Good overview, but noisy

## Firewall Evasion and Spoofing

* **-D \<decoy1,decoy2,...>** : Decoy scanning
* **-S <IP>** : Spoof source IP
* **--spoof-mac <mac>** : Spoof MAC address (e.g., --spoof-mac Apple)
* **-f** : Fragment packets
* **--data-length <n>** : Append random data to packets
* **--source-port <port>** : Use specific source port (e.g., 53 or 443)

## Output Options

* **-oN <file>** : Normal output
* **-oX <file>** : XML output
* **-oG <file>** : Grepable output
* **-oA <basename>** : Output in all formats with given base name

## Script Scanning (NSE)

* **-sC** : Run default scripts
* **--script \<name/category>** : Run specific scripts
* **--script-args <args>** : Provide arguments to scripts
* **--script-help <script>** : Show script description

Examples:

```bash
nmap -sC -sV <target>
nmap --script=vuln <target>
nmap --script=http-enum <target>
```

## Scan Examples

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

---

## Notes

* Run as root or with sudo to enable some scans (e.g., SYN, OS detection)
* Use responsibly and only on systems you are authorized to test
* Combine options for more tailored scans
