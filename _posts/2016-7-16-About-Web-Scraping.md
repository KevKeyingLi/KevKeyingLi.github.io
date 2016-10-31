---
layout: post
title: About Web Scraping
author: Kevin
---
I have been recently working on a project to download online files from a website. Here I would like to describe and record how I tackled it and what are the methods that I used. Due to privacy concerns I will not be able to disclose the name of the website and the project. But I promise this is totally legal action. 

## Problem Overview

The website provides a text/condition search engine that can be used to retrieve document IDs of files. Given the document IDs, one can easily access the desired file by editing the url. 

A major problem here would be how to avoid being blocked when downloading files programmatically, and download as fast as possible. Continuously and robotically accessing the website and downloading files can impose heavy load on the server. The server may end up blocking (refuse to serve) such client for sake of security. 

## Preparation

To decide how to download the files programmatically, we need to first examine the website to see where can we break into it. 

A initial idea of getting search results(document IDs) and dowloading files is to use a tool to programmatically imitate the behaviour of a client -- a browser. After some googling, I found two ways: 

- Use Selenium Webdriver with any browser can do exactly "programmatically mimic surfing the internet". And PhantomJS, a javascript headless browser is a good fit to work with Selenium Webdriver. 
- Another possible way, is to imitate browser issuing HTTP requests to server to get data. This requires two things: the server communicates with the client through a REST API, and the knowledge of this API. (I am not sure if the word REST API is accurate here. I always have difficulty understanding the idea of RESTful API. Please let me know if I am wrong.)

The first approach is universally usable, but requires far more unnecessary processing when rendering and parsing the webpage, and will produce more hits on the server. The second, is easier and more efficient. 

Thus, I chose to try out the HTTP request approach prior to the webdriver one.

## HTTP request method

As mentioned above, to be able to use this approach, we need to make sure the server's HTTP API is usable for requesting desired data. Thus I started examining the behaviour and source code of the website. 

My attention focuses on the search result page. This page behaves as a single page application. Every time the user changes the searching criteria or go to the next page, the browser can load results without rerendering the whole page. This behaviour implies that it probably uses some ajax-like method to get data from server, and then use the data to render. (To my limited knowledge this is the only way to do it. Is there any other ways? )

Next step, I started to examine the source code with the help of Chrome developer tool. By using the Network tool and searching for keywords in source code, I located the few lines of code that initiates requests. Additionally, by examining the order each javascript file are loaded in the HTML page, can also provide insight of which file might contain the useful line of code. 

## Avoid blocking
The idea to avoid blocking is to imitate the action of humanbeing accessing the website, and disguise the identity of the same visitor repeatedly requesting the same resource. Here are a few options:
* Random back off(delay): This is a nature way of imitating human browsing the website. Also, in case where our downloading client sense any indication of anger from server, it will immediately shut down itself for a few moments, so the server will quickly forget about it. After a few weeks of trial and error, I end up with a multiple-layer back-off strategy, each layer provides different level of delay. From 0 second ~ 30seconds, to 3 minutes~10minutes, to ~30minutes, to 5 hours. 
* Disguise of identity: this is another important technique that prevents the server from remembering us. After a few days of research on related topics, I noticed that other than changing IP address, changing user agent name of our scraper is also a way to cheat the server. 
* Other then these two techniques, we also need to be able to identify if we are detected by the server. This information is usually collected from what the server return to us. (e.g. some times the server would return a sign to tell the client to show *captcha code*)


(To be continued)




