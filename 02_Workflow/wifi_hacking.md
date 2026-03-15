# WIFI hacking

## Basic information

### Terminology
- WPA2-PSK: Wifi networks that you connect to by providing a pre-shared password that's the same for everyone
- WPA2-EAP: Wifi networks that you authenticate to by providing a username and password, which is sent to a RADIUS server.
- RADIUS: A server for authenticating clients, not just for wifi.

## Tools

## aircack-ng

## airodump-ng

## airmon-ng
```bash
# Start listening on an interface (Turns interface into "monitor mode")
sudo airmon-ng start INTERFACE

# Stop listening (Turn interface back into "managed mode")
sudo airmon-ng stop INTERFACE

# Check (and kill) processes that could intefere
sudo airmon-ng [kill]
```
