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

## Examples

```bash
# Basic example
ffuf -u http://$IP/FUZZ -w /usr/share/wordlists/SecLists/Discovery/Web-Content/big.txt

# Multiple wordlists
ffuf -u http://W1.$IP/W2 -w /usr/share/wordlists/SecLists/Discovery/Web-Content/big.txt:W1,/usr/share/wordlists/SecLists/Discovery/Web-Content/quickhits.txt:W2

```

