# Metasploit

- Open with `msfconsole`

---

## Basics
### Module categories:
- Auxiliary: Any supporting module, such as scanners, fuzzers.
- Encoders: Encode payloads such that antivirus tools don't detect them.
- Evasion: Helpers to void security measures
- Exploits: exploits...
- NOPs: Don't do anything. Used as buffers for actual payloads
- Payloads: Malicious code
    - Adapter: Convert a payload into a different format
    - Single (aka "inline"): Self-contained payloads that don't need to download anything else and run on their own
    - Stager: Setting up a connection to download further data
    - Stages: Downloaded by stagers
- Post: Post-exploitation

(Singles are seperated by underscores ("_"), staged payloads are seperated by slashes ("/"))

### Navigating
- Get information about selected module: `info`
- Select a module: `use <module>` (e.g. `use exploit/windows/smb/ms17_010_eternalblue`)
- leave exploit: `back`
- show available options of the selected module: `options`
- list exploits/payloads etc.: `show [exploits|options|payloads|...]`
- run the exploit: `[run|exploit]`

### Searching
- Only search for a specific module type: `search type:auxiliary telnet`

### Options within a module
- Set an option to a value: `set <option> <value>`
- Unset the value: `unset <option>`
- Unset all values: `unset all`
- Set value of option globally: `setg <option> <value>`

### Sessions
- If an exploit was successful, a session is created. This can be set to run in the background with `background` or `CTRL+Z`
- All active sessions can be listed with `sessions`
- Go back into a session with `sessions -i <num>`

## Meterpreter
### Basics
- Runs in memory and is not stored on a disk to avoid being detected.
- Uses encryption when communicating with the C2 server.

### Commands
- `getpid`: Get the process ID of the current process meterpreter is running as
- `ps`: List running processes
- `help`: Get all commands that are available in this session
- `getuid`: Display the user with which meterpreter is running
- `migrate <pid>`: Switch to another process
- `hashdump`: List contents of SAM (Security Account Manager) database; password hashes etc.
- `shell`: Launch regular command line shell
