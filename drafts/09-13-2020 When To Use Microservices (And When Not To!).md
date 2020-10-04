# GOTO 2020 • When To Use Microservices (And When Not To!) • Sam Newman & Martin Fowler - Youtube
## Intro
https://www.youtube.com/watch?v=GBTdnfD6s5Q&ab_channel=GOTOConferences
00:00 Series intro
00:50 Episode intro
01:25 Why a new book about microservices?
03:50 When to use microservices
06:14 Don't use microservices as a default option?
08:35 Top 3 reasons to introduce microservices
11:00 How to avoid a distributed monolith
14:49 Why strive for independent deployment?
20:09 Organizations & teams
22:51 Handling data
31:57 Handling people
37:05 Outro

Martin Fowler
Sam Newman: 

## Why another book on Microservices
2015 first book Building Microservices
2020 second book: initial intention is to review the first book, but when the author started from "How to break monolithic to microservices", he decided that "Monolith to Microservices" could be a book alone. 

## When to use microservices
Only when you should. **Our industry tends to focus on tech instead of the outcome. One should use microservices as a means to obtain a desired outcome, rather than for the sake of using a new technology.**

what can microservices architecture give you 
* more options to scale up applications
* independent deployability
* limit the "blast radius" of failure.

Microservices architectures buy you options - James Lewis

## Don't use Microservices as a default option
**Microservices shouldn't be the default option. If you think a service architecture could help, try it with one of the modules from a very simple monolith typology and let it evolve from there.**

## Top 3 reasons to introduce microservices
1. Zero-downtime independent deployability
    - in Saas you can't afford downtime
2. Isolation of data, and the processing around data
    - so that different data can be treated differently, due to for example regulatory, privacy reasons.
3. Enable a higher degree of organizational autonomy. Use microservices to reflect the organizational structure.
    - distribute responsibilities into teams
    - reduce coordination within org
 
## How to avoid a distributed monolith trap
Distributed monolith: things are distributed, but dependent. So not really separated. 
1. create a delpoyment mechanism
2. look for patterns
TODO