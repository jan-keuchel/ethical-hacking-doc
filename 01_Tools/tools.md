# Tools

* [Nmap](#Nmap)
* [ffuf](#ffuf)
* [Mail](#mail)
* [Hydra](#hydra)
* [Hashcat](#hashcat)
* [Gobuster](#gobuster)

## Nmap
* [Nmap behavior](#nmap-behavior)
* [Host discovery](#host-discovery)
* [Port scanning](#port-scanning)

### Nmap behavior

#### Running nmap privileged or unprivileged
* privileged user on local network: ARP request
* privileged user outside local network: ICMP echo request, ICMP timestamp request, TCP ACK and TCP SYN
* unprivileged user outside local netowrk: TCP 3WH

#### Useful options
* `-F` Fast mode. Only scan top 100 ports instead of top 1000.

### Host discovery

#### ARP
```bash
# Don't do port scan
nmap -sn TARGETS

# ARP scan
nmap -PR -sn TARGETS
```

#### ICMP
```bash
# Most systems block echo requests: not reliable
# ICMP echo request
nmap -PE -sn TARGETS

# Blocked less frequently than ICMP echo requests
# ICMP timestamp request
nmap -PP -sn TARGETS

# Blocked less frequently than ICMP echo requests
# ICMP address mask request
nmap -PM -sn TARGETS
```

#### TCP and UDP
```bash
# SYN scan (3WH, unprivileged)
nmap -PS21-25 -sn TARGETS

# Doesn't complete the entire 3WH
# SYN scan (SYN-RST, privileged)
sudo nmap -PS80,443,8080 -sn TARGETS

# Default port is 80
# Unprivileged user would complete 3WH
# TCP ACK Ping (expects a RST as response)
sudo nmap -PA443 -sn TARGETS

# UDP Ping doesn't expect a response if port is open.
# Could be blocked by firewall: No response -> might be up
# Expects a ICMP port unreachable if port is closed: Host up
sudo nmap -PU -sn TARGETS 
```

### Port scanning

#### Port states
| State | Meaning|
|-------|--------|
| **Open** | Service is listening on the port |
| **Closed** | No service is listening on the port, not blocked by firewall. |
| **Filtered** | Nmap can't say if it's open or closed. Blocked by firewall. |
| **Unfiltered** | Nmap can't say if it's open or closed. Not blocked by firewall. |
| **Open\|Filtered** | Nmap can't say if it's open or filtered. |
| **Closed\|Filtered** | Nmap can't say if it's closed or filtered. |

#### Examples
```bash
# First broad scan to detect open ports
nmap -T4 -p- -Pn $IP

# Version detection, OS detection, all ports, fast packets, verbose
nmap -T4 -A -p- -Pn -v $IP
```

#### Basic scanning

```bash
# TCP Connect Scan
# Complete a 3WH, then send a RST,ACK flag to terminate connection
nmap -sT TARGET

# TCP SYN Scan
# Terminate the 3WH after receiving SYN,ACK
sudo nmap -sS TARGET

# UDP Scan
# Open UDP ports don't always replay.
# Closed UDP ports answer with an ICMP port unreachable packet.
sudo nmap -sU TARGET
```

#### Specific scans

##### Usefull against a stateless firewall: Null, FIN and Xmas
```bash
# Null scan
# No flags are set. Won't trigger response.
sudo nmap -sN TARGET

# FIN scan
# Sends packet with FIN flag set. Won't trigger response.
sudo nmap -sF TARGET

# Xmas scan
# Sends packet with FIN, PSH and URG flag. Won't trigger response.
sudo nmap -sX TARGET

# All scans won't trigger a response.
# All scans expect a RST flag if the port is closed.
# No answer -> open|filtered
```

##### Get information about firewall configuration: ACK and Window scan
```bash
# ACK
# Expects a RST packet if port is not blocked by firewall -> unfiltered
# Expects no response / ICMP unreachable if blocked by firewall -> filtered
sudo nmap -sA TARGET

# Window
# Sends identical packet to ACK scan but examins the Window option of 
# the RST response.
# TCP RST with non-zero Window field -> open
# TCP RST with zero Window field -> closed
# No response/ICMP unreachable -> filtered
sudo nmap -sW TARGET
```

#### NSE
```
# Search for scripts
ls -l /usr/share/nmap/scripts | grep <search-term>

# Get basic information about the script
nmap --script-help <script>
```

## ffuf

### Basics

- The 'FUZZ' keyword is used to tell ffuf where to insert the wordlist items.
- The `-u <url>` and `-w <wordlist>` arguments are required.

### Syntax

```bash
ffuf -w [wordlist] -u [target_URL] [commands]                   # Basic 
ffuf -w wordlist1:W1,wordlist2:W2 -u [target_URL] [commands]    # Use multiple wordlists
```

### Frequently used flags
- `-c` colored output
- `-H` Header `<name>: <value>`
- `m[clrstw]` match (Filter out everything except for those responses that match the criterea) **C**ode, number of **L**ines, **R**egEx, HTTP Response **S**ize, **M**illiseconds to first response, Number of **W**ords in response
- `f[clrstw]` filter (Filter out response that matches the criterea) **C**ode, number of **L**ines, **R**egEx, HTTP Response **S**ize, **M**illiseconds to first response, Number of **W**ords in response
- `-v` verbose

### Examples

```bash
# Directory fuzzing
ffuf -u http://$IP:PORT/FUZZ -w wordlist.txt

# Multiple wordlists
ffuf -u http://W1.$IP:PORT/W2 -w /usr/share/wordlists/SecLists/Discovery/Web-Content/big.txt:W1,/usr/share/wordlists/SecLists/Discovery/Web-Content/quickhits.txt:W2

# VHost discovery
ffuf -u http://$IP -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-20000.txt -H 'Host: FUZZ.lookup.thm' -c -fs 0
```

## Mail
### POP3
#### Connecting and authentication
```bash
# Connect to the service
nc $IP <port>

# Authenticate
USER <username>
PASS <password>

# List messages
LIST

# Get/Modify messages
RETR <ID>
DELE <ID>

# Exit
QUIT
```

### SMTP
```bash
# Connect to the service
nc $IP <port>
```


## Hydra

### Basic information
- **`-l/-L`**: specify login name or list of names
- **`-p/-P`**: specify password or wordlist
- **`-s`**: specify port
- **`-S`**: Connect via SSL
- **`-V`**: Show every attempt
- **`-I`**: Skip waiting at the beginning
- **`-u`**: Switch from DFS to BFS

### Examples
#### POP3
```bash
hydra -l LOGIN -P WORDLIST -s PORT $IP pop3
```

#### ssh
```bash
hydra -l LOGIN -P WORDLIST -s PORT $IP ssh
```

#### FTP
```bash
hydra -l LOGIN -P WORDLIST -s PORT $IP ftp
```

## Hashcat

```bash
hashcat [options] -m [hash_type] -a [attack_mode] [hash_file] [wordlist|mask]
```
- Find hash types at `man hashcat` search for `Hash types`

### Attack modes
| NUM | Mode |
|-----|------|
|0| Dictionary|
|1| Combinaton (combine words of two wordlists)|
|3| Brute-force|

### Examples
#### Salted md5 hash dictionary attack
- Create file with the format `PASS:SALT`
- Attack:
```bash
hashcat -m 10 -a 0 hash_file WORDLIST
```

## John

### Cracking encrypted zip files
```bash
# Create a hash for John
zip2john ZIP_FILE > hash

# Brute-force
john --wordlist=WORDLIST hash
```

## Gobuster

### Directory fuzzing
```bash
# Fuzz for basic directories
gobuster dir -w /usr/share/wordlists/dirbuster/list -u http://$IP
```
