# 2022-08-23-Building Faster Websites: Get Started with Web Performance - Udemy.md

https://servicenow.udemy.com/course/building-faster-websites-getting-started-with-web-performance/learn/lecture/23706646#overview
# Section 2: web performance explained
## 2 What is Web Performance
Web performnace optimisation/WPO/ Front end performance
* measuring performance: continuous
* improve load times
* Perceived performance


* Accomodating users
* Looking after users
* Search engine optimization
* Improveing conversions
* Perceived performance

## 3 Accommodating users
A lot of users are on slower devices and network

The probability of bounce(leave the site without using it) increases as page load time increases
## 4 Looking after users
Main culprits of larger package size: CSS, Fonts, JavaScript, Image

Some areas network fee are charged by use. Large sites means more cost for user.

This also limits access to important information resources,

## 5 Search engine optimsation
Slow website will impact search engine ranking

Google implemented this since 2010
## 6 Improving conversions
Every website has goals: conversion
* sell product
* sell services
* provide information

Faster performance is competitive advantage

https://www.thinkwithgoogle.com/feature/testmysite/ is sunsetting in 2022
## 7 Perceived performance

Performance is not about math, it's about perception. 

Human's perception of time: psychological time:
* Active phase: 
* Passive phase: can't do anything

Slowness is mostly due to passive phase.

Two ways to reduce perceived wait time:
* Pre-emptive start, begin in active phase, and delay the switch to passive phase
* Early completion: give user something to interact with early, so it becomes active wait

# Section 3: measuring web performance

## 8. How browser load websites

Terminologies:
* HTTP
* DNS lookup: each different domain name would require additional DNS lookup (cost)
* TCP Handshake: connect to server
* TLS Handshake: https
* Response
* Round trip
* Critical rendering path: The critical rendering path refers to the minimum number of steps which the browser must complete once it begins to receive assets from the server to convert a website's HTML, CSS and JavaScript into on screen pixels.
    - DOM: HTML parser and generate doc
        + <link> tags, usually css stylesheet, triggeres HTTP calls to fetch resources, this happens async
        + <script> HTML parser pauses until the request is completed. (unless, the script tag has an attribute for defer or async). The HTML parser resumes after script is executed.
        + Once the HTML is parsed, and DOM complete. Browser fires: DOMContentLoaded

    - CSSOM: CSS Object model, build by browser by parsing css + browser defaults
        + page render should happen after css is parsed, otherwise the page will change while css is parsed.
    - Render tree = DOM + CSSOM. A representation of the styled visible content
    - Layout: the size of the DOM determines how fast layout happens
        + This is not one off. Whenever the DOM is modified, update layout happens
        + repeat layout is called reflow, and can be resource expensive - a chain reaction
    - Paint: render the layout + render tree. 
        + on first load, whole page is painted, later layout adjustments, only repaint part of the page.
* Interactivity
    + Any defer javascript will execute when paint is finished.



