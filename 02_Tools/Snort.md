
# Snort Cheatsheet for Ethical Hacking

## Table of Contents

* [Getting Started](#getting-started)
* [Modes](#modes)

---

## Getting Started

```bash
snort          # Launch snort
```

### Modes

* **Packet sniffer mode**: Simply reads in all the traffic without taking any action.
* **Packet logging mode**: Dont listen on the network. Instead, read in a PCAP file and perform detection there.
* **Network IDS Mode**: Monitor network traffic and create an alert if set rules apply.

### Config

* Snort config files are stored at `/etc/snort`. The main config file is `snort.conf`.
* The rules snort applies are stores at `/etc/snort/rules`.
* Custom rules can be saved at `/etc/snort/rules/local.rules`

### Rules

* Snort rules are written in the following format:
```bash
ACTION PROTOCOL SOURCE_IP SOURCE_PORT -> DESTINATION_IP DESTINATION PORT (MESSAGE; SIGNATURE_ID; RULE_REVISION;)

# Example:
# '$HOME_NET' is a variable defined in snort.conf
alert icmp any any -> $HOME_NET any (msg:"Ping Detected"; sid_10001; rev:1;)
```
