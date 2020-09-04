WebSocket reading notes
## [WebSockets, caution required!](https://samsaffron.com/archive/2015/12/29/websockets-caution-required)
This article is written based on author's experience with Ruby on Rails

WebSockets provides simple APIs to broadcast information to clients and simple APIs to ship information from the clients to the web server.
### Somewhat benefits
Since it's a open connection, once the connection establishes, all the communication happen without header parsing(quite light), and middleware process(could be heavy but optimizable).

### Drawbacks
#### The history
The history of websocket standards is long and tumultuous. Though today it is standardized, implementations in browsers are still hardly consistent. 

#### Doesn't work well with proxy servers
#### Browsers allow a good number of open WebSockets
each browser tab will have one websocket connection. Opening a lot of tabs would cause large amounts of load and consume large amounts of continuous server resources.

In comparison HTTP/2 transport is able to cope with the multiple tab problem much more efficiently than WebSockets. A single HTTP/2 connection can be multiplexed across tabs, which makes loading pages in new tabs much faster and significantly reduces the cost of polling or long polling from a networking point of view.

Unfortunately
#### WebSockets and HTTP/2 transport doesn't work well together
#### TO CONTINUE: 4) Implementing WebSockets efficiently on the server side requires epoll, kqueue or I/O Completion ports.

### Terms:
* backchannel
* console sessions
* [Rack middleware](https://stackoverflow.com/questions/2256569/what-is-rack-middleware). 
* what is middleware: Middleware is a dreadful term which refers to any software component/library which assists with but is not directly involved in the execution of some task. Very common examples are logging, authentication and the other common, horizontal processing components. These tend to be the things that everyone needs across multiple applications but not too many people are interested (or should be) in building themselves.
* Usage of a middleware could include
    - **Authentication**: when the request arrives, are the users logon details correct? How do I validate this OAuth, HTTP Basic Authentication, name/password?
    - **Authorization**: "is the user authorised to perform this particular task?", i.e. role-based security.
    - **Caching**: have I processed this request already, can I return a cached result?
    - **Decoration**: how can I enhance the request to make downstream processing better?
    - **Performance & Usage Monitoring**: what stats can I get from the request and response?
Execution: actually handle the request and provide a response.
* middleware crawl: probably means the process of going through each step of the middleware
* [6 connections per host limit](https://stackoverflow.com/questions/985431/max-parallel-http-connections-in-a-browser)
* epoll
* kqueue
* I/O completion ports

# TO READ on websocket
[Load Balancing of WebSocket Connections](https://dzone.com/articles/load-balancing-of-websocket-connections#:~:text=By%20default%2C%20a%20single%20server,%2C%20it's%20a%20half%2Dtruth.)
