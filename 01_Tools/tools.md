# Tools

* [Nmap](#Nmap)
* [ffuf](#ffuf)

## Nmap

### Nmap behavior
- privileged user on local network: ARP request
- privileged user outside local network: ICMP echo request, ICMP timestamp request, TCP ACK and TCP SYN
- unprivileged user outside local netowrk: TCP 3WH

### Host discovery

#### ARP
```bash
nmap -sn TARGETS # Don't do port scan

nmap -PR -sn TARGETS # ARP scan
```

#### ICMP
```bash
# Most systems block echo requests: not reliable
nmap -PE -sn TARGETS # ICMP echo request

# Blocked less frequently than ICMP echo requests
nmap -PP -sn TARGETS # ICMP timestamp request

# Blocked less frequently than ICMP echo requests
nmap -PM -sn TARGETS # ICMP address mask request
```

#### TCP and UDP
```bash
nmap -PS21-25 -sn TARGETS # SYN scan (3WH, unprivileged)

# Doesn't complete the entire 3WH
sudo nmap -PS80,443,8080 -sn TARGETS # SYN scan (SYN-RST, privileged)

# Default port is 80
# Unprivileged user would complete 3WH
sudo nmap -PA443 -sn TARGETS # TCP ACK Ping (expects a RST as response)

# UDP Ping doesn't expect a response if port is open.
# Could be blocked by firewall: No response -> might be up
# Expects a ICMP port unreachable if port is closed: Host up
sudo nmap -PU -sn TARGETS # UDP Ping
```

## ffuf
