See:
* [[Py - Introduction to Python]]
* [[Py - Web Scrapping]]
* [[Distributed Denial of Service (DDoS)]]
Resources:
* Documentation: [BeautifulSoup](https://www.crummy.com/software/BeautifulSoup/bs4/doc/)

---

# Legality of Web-Scrapping

## What is legal?
* Web-Scrapping is legal as long as you do NOT commercialize on copyright data 

# Ethics of Web-Scrapping
* Resort to API over scrapping, if available 
* Do not scrape to the point of impacting the website's servers or triggering a DDoS attack

## What can be scrapped?
* On the main homepage of the website, type in `/robots.txt` at the end of the url
```URL
https://news.ycombinator.com/robots.txt
```

## How to Read the `robots.txt`?
* `crawl-delay:` the number of seconds or minutes to wait between scraps
* `disallow:` -- the endpoints to avoid

