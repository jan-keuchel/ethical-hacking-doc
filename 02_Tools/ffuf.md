# ffuf Cheatsheet

- ffuf (Fuzz Faster U Fool) is a general purpose fuzzing tool.

## Basics

- The 'FUZZ' keyword is used to tell ffuf where to insert the wordlist items
- The `-u <url>` and `-w <wordlist>` arguments are required

---

## Syntax

```bash
ffuf -w [wordlist] -u [target_URL] [commands]                   # Basic 
ffuf -w wordlist1:W1,wordlist2:W2 -u [target_URL] [commands]    # Use multiple wordlists
```

## Frequently used flags
- `-c` colored output
- `-H` Header `<name>: <value>`
- `m[clrstw]` match (Filter out everything except for those responses that match the criterea) **C**ode, number of **L**ines, **R**egEx, HTTP Response **S**ize, **M**illiseconds to first response, Number of **W**ords in response
- `f[clrstw]` filter (Filter out response that matches the criterea) **C**ode, number of **L**ines, **R**egEx, HTTP Response **S**ize, **M**illiseconds to first response, Number of **W**ords in response
- `-v` verbose

## Examples

```bash
# Basic example
ffuf -u http://$IP/FUZZ -w /usr/share/wordlists/SecLists/Discovery/Web-Content/big.txt

# Multiple wordlists
ffuf -u http://W1.$IP/W2 -w /usr/share/wordlists/SecLists/Discovery/Web-Content/big.txt:W1,/usr/share/wordlists/SecLists/Discovery/Web-Content/quickhits.txt:W2

# VHost discovery
ffuf -u http://$IP -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-20000.txt -H 'Host: FUZZ.lookup.thm' -c -fs 0
```

