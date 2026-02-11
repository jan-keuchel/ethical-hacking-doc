# Tools

* [Nmap](#Nmap)
* [ffuf](#ffuf)

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

## ffuf
