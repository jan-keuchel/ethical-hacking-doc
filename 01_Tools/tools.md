# Tools

* [Nmap](#Nmap)
* [ffuf](#ffuf)

## Nmap
* [Nmap behavior](#nmap-behavior)
* [Host discovery](#host-discovery)

### Nmap behavior
- privileged user on local network: ARP request
- privileged user outside local network: ICMP echo request, ICMP timestamp request, TCP ACK and TCP SYN
- unprivileged user outside local netowrk: TCP 3WH

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

## ffuf
