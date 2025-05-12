# Basic Webpage assessment

## 1. Exploring the Webpage

* Look through the webpageg and note down all the different pages along their usecase

---

## 2. Look through the pages source code

* Look for hidden links, comments containing useful information or other directories

---

## 3. Specific pages

Look for specific files such as ...

* `/robots.txt` - Contains the pages that are not allowed to be crawled
* `/sitemap.xml` - Contains all the pages that should be found by the search engine

---

## Google Dorking

| Filter    | Example              | Description                                   |
|-----------|----------------------|-----------------------------------------------|
| site      | site:tryhackme.com   | Only show results from specified site         |
| inurl     | inurl:admin          | Return results with specified word in the url |
| filetype  | filetype:pdf         | Returns results with specified file extension |
| intitle   | intitle:admin        | Returns results with specified word in title  |

[More Google Dorking examples](https://gist.github.com/sundowndev/283efaddbcf896ab405488330d1bbc06)

## Gobuster for content discovery

[Gobuster](../02_Tools/Gobuster.md)
