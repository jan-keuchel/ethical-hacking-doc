# Nmap Cheatsheet

## Scan Hosts from a File

```bash
nmap -iL hosts.txt
```

---

## Host Discovery (No Port Scanning)

Use the `-sn` option to disable port scanning:

- **ARP Scan** (Local network only):
  ```bash
  sudo nmap -PR -sn MACHINE_IP/24
  ```

- **ICMP Echo Scan**:
  ```bash
  sudo nmap -PE -sn MACHINE_IP/24
  ```

- **ICMP Timestamp Scan**:
  ```bash
  sudo nmap -PP -sn MACHINE_IP/24
  ```

- **ICMP Address Mask Scan**:
  ```bash
  sudo nmap -PM -sn MACHINE_IP/24
  ```

- **TCP SYN Ping Scan**:
  ```bash
  sudo nmap -PS22,80,443 -sn MACHINE_IP/30
  ```

- **TCP ACK Ping Scan**:
  ```bash
  sudo nmap -PA22,80,443 -sn MACHINE_IP/30
  ```

- **UDP Ping Scan**:
  ```bash
  sudo nmap -PU53,161,162 -sn MACHINE_IP/30
  ```

### Useful Options

- `-n`: No DNS resolution  
- `-R`: Reverse DNS resolution for all hosts  
- `-sn`: Host discovery only (no port scan)  
- `-sL`: List targets to verify input before scanning

---

## Port Scanning

```bash
sudo nmap [options] [IP]
```

- By default, Nmap scans the top **1000** ports.

### Scan Types

- `-sT`: TCP Connect Scan (3-way handshake)
- `-sS`: SYN Scan (Stealthy)
- `-sU`: UDP Scan

### Scanning Options

- `-F`: Fast scan (top 100 ports)
- `-p[range]`: Scan specific ports (e.g. `-p10-1024`)
- `-p-`: Scan **all** 65535 ports
- `-p-25`: Scan ports 1 through 25

---

## Version & OS Detection

- `-sV`: Version detection  
- `-O`: OS detection  
- `-A`: Aggressive scan (includes OS detection, version, traceroute, scripts, etc.)

---

## Force a Scan

- `-Pn`: Skip host discovery — treat all hosts as online

---

## Scan Timing & Speed

- `-T0` to `-T5`: Timing templates (0 = paranoid, 3 = normal, 5 = insane)
- `--min-parallelism <num>` / `--max-parallelism <num>`: Number of parallel probes
- `--min-rate <rate>` / `--max-rate <rate>`: Rate of packets per second
- `--host-timeout <time>`: Timeout per host (e.g., `--host-timeout 30s`)

---

## Output Formats

- `-v`: Verbose output  
- `-d`: Debugging mode (very verbose)  
- Output to file:
  - `-oN <file>`: Normal output
  - `-oX <file>`: XML output
  - `-oG <file>`: Greppable output
  - `-oA <prefix>`: Output in all major formats
