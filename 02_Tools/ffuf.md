# ffuf Cheatsheet

* ffuf stands for Fuzz Faster U Fool. It's a tool used for web enumeration, fuzzing, and directory brute forcing.

## Basics

* The 'FUZZ' keyword is used to tell ffuf where to insert the wordlist items


### Help

```bash
ffuf -h                     # General help page
```

---

## Syntax

```bash
ffuf -w [wordlist] -u [target_URL] [commands]                   # Basic 
ffuf -w wordlist1:W1,wordlist2:W2 -u [target_URL] [commands]    # Use multiple wordlists
```


## Examples

```bash
# Basic example
ffuf -u http://10.10.57.100/FUZZ -w /usr/share/wordlists/SecLists/Discovery/Web-Content/big.txt

# Multiple wordlists
ffuf -u http://W1.10.10.57.100/W2 -w /usr/share/wordlists/SecLists/Discovery/Web-Content/big.txt:W1,/usr/share/wordlists/SecLists/Discovery/Web-Content/quickhits.txt

```

