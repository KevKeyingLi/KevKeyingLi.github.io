---
layout: post
title: Angular2 Learning Note
author: Kevin
---
I have been recently working on a project to download online files from a website. Here I would like to describe and record how I tackled it and what are the methods that I used. Due to privacy concerns I will not be able to disclose the name of the website. 

## Problem Overview

The website provides a text/condition search engine that can be used to retrieve document IDs of files. Given the document IDs, one can easily access the desired file by editing the url. 

A major problem here would be how to avoid being blocked when downloading files programmatically. Continuously and robotically accessing the website and downloading files can impose heavy load on the server. The server may end up blocking (refuse to serve) such client for sake of security. 

## Preparation

To decide how to download the files programmatically, we need to first examine the website to see where can we break into it. 

A initial idea of getting search results(document IDs) and dowloading files is to use a tool to programmatically imitate the behaviour of a client -- a browser. After some googling, I found two ways: 

- Use Selenium Webdriver with any browser can do exactly "programmatically mimic surfing the internet". And PhantomJS, a javascript headless browser is a good fit to work with Selenium Webdriver. 
- Another possible way, is to imitate browser issuing HTTP requests to server to get data. This requires two things: the server communicates with the client through a REST API, and the knowledge of this API. (I am not sure if the word REST API is accurate here. I always have difficulty understanding the idea of RESTful API. Please let me know if I am wrong.)

The first approach is universally usable, but requires far more processing when rendering and parsing the webpage. The second, is easier and more efficient.

I choosed to try out the HTTP request approach prior to the webdriver one.

## HTTP method

As mentioned above, to be able to use this approach, we need to make sure the server's HTTP API is usable for requesting desired data. Thus I started examining the behaviour and source code of the website. 

My attention focuses on the search result page. This page behaves as a single page application. Every time the user changes the searching criteria or go to the next page, the browser can load results without rerendering the whole page. This behaviour implies that it probably uses some ajax-like method to get data from server. (To my limited knowledge this is the only way to do it. Is there any other ways? )

Next step, I started to examine the source code with the help of Chrome developer tool. By using the Network tool and searching for keywords in source code, I located the few lines of code that initiates requests. 






