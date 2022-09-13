# Internet
https://github.com/kamranahmedse/developer-roadmap/tree/master/content/roadmaps/100-frontend/content/100-internet

https://github.com/kamranahmedse/developer-roadmap/tree/master/content/roadmaps/101-backend/content/100-internet

# The Internet Explained - Article
https://www.vox.com/2014/6/16/18076282/the-internet
## Keywords
* Three parts of internet
* IP
* Packet
* WWW
* SSL
* DNS

1969

The internet is not the web, web is just one application of internet.

## Three basic parts of internet
* the last mile: cable, fiber, cellular tower
* Data centers: 
    - host servers
    - fast internet access
    - usually hosted in remote areas where land and electricity are cheap
* The backbone: long-distance networks mostly on fiber optic cables
    - networks from different providers are connected at **internet exchange points**, usually major cities.


No one runs the internet. It’s organized as a decentralized network of networks. 
* The shared technical standards that make the internet work are managed by an organization called the Internet Engineering Task Force. 
* The Internet Corporation for Assigned Names and Numbers (ICANN) is sometimes described as being responsible for internet governance. As its name implies, ICANN is in charge of distributing domain names (like vox.com) and IP addresses. 

IP: Internet protocol.

## Packet
Packet: A packet is the basic unit of information transmitted over the internet.
* Two parts:
    - header contains information that helps the packet get to its destination, including 
        + the length of the packet
        + its source and destination
        + a checksum value that helps the recipient detect if a packet was damaged in transit
    -  the actual data. A packet can contain up to 64 kilobytes of data, which is roughly 20 pages of plain text.
* Routers discard packets when experience congestion
* It’s the sending computer’s responsibility to detect that a packet didn’t reach its destination and send another copy

WWW - World Wide Web
1991
* A way to publish information on the internet. hyperlinks, images, audio, video
* World Wide Web Consortium (W3C) to be the web’s official standards organization.
* In practice, the organizations with the most influence over the web are Microsoft, Google, Apple, and Mozilla, the companies that produce the leading web browsers. Any technologies adopted by these four become de facto web standards.


## SSL
SSL: Secure Sockets Layer: a family of encryption technologies that allows web users to protect the privacy of information they transmit over the internet.
* encrypts your message

## DNS
Domain Name System
* The system is hierarchical. 
    - e.g. Verisign manages .com

A standard called **DNSSEC** seeks to beef up DNS security with encryption, but few people have adopted it.
Two types of domain names:
* generic top-level domains (gTLDs) such as .com, .edu, .org, and .gov.
* country-code top-level domains (ccTLDs): .us, .uk, .cn


# How Does the Internet Work? - Article Stanford

http://web.stanford.edu/class/msande91si/www-spr04/readings/week1/InternetWhitepaper.htm

