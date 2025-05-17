# Basic Webpage assessment

## 1. Exploring the Webpage

* Look through the webpage and note down all the different pages along their usecase

---

## 2. Look through the pages source code

* Look for hidden links, comments containing useful information or other directories

---

## 3. Specific pages

Look for specific files such as ...

* `/robots.txt` - Contains the pages that are not allowed to be crawled
* `/sitemap.xml` - Contains all the pages that should be found by the search engine

---

## 4. Google Dorking

| Filter    | Example              | Description                                   |
|-----------|----------------------|-----------------------------------------------|
| site      | site:tryhackme.com   | Only show results from specified site         |
| inurl     | inurl:admin          | Return results with specified word in the url |
| filetype  | filetype:pdf         | Returns results with specified file extension |
| intitle   | intitle:admin        | Returns results with specified word in title  |

[More Google Dorking examples](https://gist.github.com/sundowndev/283efaddbcf896ab405488330d1bbc06)

## Content discovery and subdomains

* [Gobuster](../02_Tools/Gobuster.md)
* When an SSL/TLS certificate is issued that process is reported in a CT-Log (Certificate Transparency). This can be used to discover subdomains. View logged subdomains at [crt.sh](https://crt.sh/?q=tryhackme.com).
* dnsrecon : Brute force DNS requests to disover subdomains.
* sublist3r : Brute force DNS requests to disover subdomains.
