---
title: Writing a Performant Webcrawler in Javascript
date: '2016-09-07'
tags: ['javascript', 'webcrawling', 'performance']
draft: false
summary: A tutorial on writing a performant webcrawler in javascript, including code examples and explanations.
---

Webcrawling, also known as web scraping, is the process of extracting data from a website. It can be a useful tool for data analysis, lead generation, and price comparison. However, it can also be a taxing process on both the webcrawler and the website being crawled. In this tutorial, we will go over how to write a performant webcrawler in javascript that is both efficient and respectful to the website being crawled.


## Code
The first step in creating a webcrawler is to set up the basic structure of the script. We will be using the request and cheerio libraries to make HTTP requests and parse the HTML of the website, respectively.

```javascript
const request = require('request');
const cheerio = require('cheerio');
```
Next, we will set up the function that will handle the webcrawling. The function will take in a URL as a parameter and use the request library to make an HTTP GET request to that URL.

```javascript
function webcrawl(url) {
    request(url, (error, response, html) => {
        if (!error && response.statusCode == 200) {
            // success
        }
    });
}
```
Once the request is successful, we will use the cheerio library to parse the HTML and extract the data we need. In this example, we will extract all the links on the page.

```javascript
function webcrawl(url) {
    request(url, (error, response, html) => {
        if (!error && response.statusCode == 200) {
            const $ = cheerio.load(html);
            $('a').each((i, link) => {
                console.log($(link).attr('href'));
            });
        }
    });
}
```
To make sure we are not overloading the website with requests, we will implement a delay between requests using the setTimeout function.

```javascript
function webcrawl(url) {
    request(url, (error, response, html) => {
        if (!error && response.statusCode == 200) {
            const $ = cheerio.load(html);
            $('a').each((i, link) => {
                console.log($(link).attr('href'));
                setTimeout(() => {
                    webcrawl($(link).attr('href'));
                }, 1000);
            });
        }
    });
}
```
## Explanation
The code above sets up a basic webcrawler that makes HTTP GET requests to a given URL and extracts all the links on the page. The request library is used to make the HTTP request and the cheerio library is used to parse the HTML and extract the data. The setTimeout function is used to implement a delay between requests to avoid overloading the website.

## Conclusion
Writing a performant webcrawler in javascript is relatively simple with the use of libraries like request and cheerio. However, it is important to keep in mind the performance and ethical
