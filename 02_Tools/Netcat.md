# Netcat Cheatsheet

## Basics

* Can be used to listen for incomming connections from a reverse shell.

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
* `-p` : Specify the port to use.

In order to blend in, use well known ports to listen on.

---

## Examples

```bash
# Basic most common use case
nc -lnvp 443

```
