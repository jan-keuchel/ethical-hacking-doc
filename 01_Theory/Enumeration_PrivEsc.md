# Enumeration for privilige escalation on linux

## Usefull commands and files

| Command               | Usecase                                                               |
| --------------------- | --------------------------------------------------------------------- |
| `hostname`            | Displays the hostname of the target machine                           |
| `uname -a`            | Print system information and details about the kernel                 |
| `/proc/version`       | Print system information and details about the kernel                 |
| `/etc/issue`          | Information about the OS                                              |
| `ps`                  | Process status. Usefull flags, settings: `-A`, `aux`                  |
| `env`                 | Show environment variables                                            |
| `sudo -l`             | Show commands current user is allowed to run as sudo                  |
| `id`                  | Provide information about the users privilege level and groups        |
| `/etc/passwd`         | Can be used to discover users                                         |
| `history`             | Search through history. Maybe credentials can be found                |
| `ifconfig`            | Information about the network interfaces                              |
| `netstat`             | Information about existing connections                                |
| `find`                | Find files on the system                                              |
| `/etc/crontab`        | Contains cronjobs which are executed as the owner                     |


## Other commands

* `cat /etc/passwd | cut -d ":" -f 1` : List all the users in the `/etc/passwd` file
* `cat /etc/passwd | grep home` : "real" users have their folders in the `/home` dir. (Discover users)
* `netstat -a` : Show all ports and established connections
* `netstat -a[tu]` : Show all ports and established connections using TCP/UDP
* `netstat -l` : Show all ports in listening mode and established connections. These ports are ready to accept incomming connections.
* `getcap -r / 2>/dev/null` : List files with capabilities set. Search GTFObins for exploits.

### find command

* `find . -name flag1.txt 2>/dev/null` : find the file named “flag1.txt” in the current directory
* `find / -type d -name config 2>/dev/null` : find the directory named config under “/”
* `find / -type f -perm 0777 2>/dev/null` : find files with the 777 permissions (files readable, writable, and executable by all users)
* `find / -perm a=x 2>/dev/null` : find executable files
* `find /home -user frank 2>/dev/null` : find all files for user “frank” under “/home”
* `find / -mtime 10 2>/dev/null` : find files that were modified in the last 10 days
* `find / -atime 10 2>/dev/null` : find files that were accessed in the last 10 day
* `find / -cmin -60 2>/dev/null` : find files changed within the last hour (60 minutes)
* `find / -amin -60 2>/dev/null` : find files accesses within the last hour (60 minutes)
* `find / -size 50M 2>/dev/null` : find files with a 50 MB size
* `find / -size +50M 2>/dev/null` : find files with size larger than 50 MB
* `find / -writable -type d  2>/dev/null` : Find world-writeable folders
* `find / -perm -222 -type d 2>/dev/null` : Find world-writeable folders
* `find / -perm -o w -type d 2>/dev/null` : Find world-writeable folders
* `find / -perm -o x -type d 2>/dev/null` : Find world-executable folders
* `find / -type f -perm -04000 -ls 2>/dev/null` : List files that have SUID or SGID bits set
