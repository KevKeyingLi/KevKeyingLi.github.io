# REST
## 6 Principles or Constraints
1. Client-server: separation of UI concerns from data storage concerns, allows same API used by multiple UI
2. Stateless: Request contains all necessary information, Session state is therefore kept entirely on the client.
3. Cacheable: data within a response to a request be implicitly or explicitly labeled as cacheable or non-cacheable
4. Uniform interface: read here https://restfulapi.net/
5. Layered system: The layered system style allows an architecture to be composed of hierarchical layers by constraining component behavior such that each component cannot “see” beyond the immediate layer with which they are interacting.
6. Code on demand (optional) – REST allows client functionality to be extended by downloading and executing code in the form of applets or scripts. This simplifies clients by reducing the number of features required to be pre-implemented.

## Resource Methods
Think of these four methods corresponds to CRUD.

|HTTP Verb|CRUD         |Entire Collection (e.g. /customers) |Specific Item (e.g. /customers/{id})|
|-------|---------------|------------------------------------|------------------------------------|
|POST   |Create         |201 (Created), 'Location' header with link to /customers/{id} containing new ID.|404 (Not Found), 409 (Conflict) if resource already exists..|
|GET    |Read           |200 (OK), list of customers. Use pagination, sorting and filtering to navigate big lists.|200 (OK), single customer. 404 (Not Found), if ID not found or invalid.|
|PUT    |Update/Replace |405 (Method Not Allowed), unless you want to update/replace every resource in the entire collection.|200 (OK) or 204 (No Content). 404 (Not Found), if ID not found or invalid.|
|PATCH  |Update/Modify  |405 (Method Not Allowed), unless you want to modify the collection itself.|200 (OK) or 204 (No Content). 404 (Not Found), if ID not found or invalid.|
|DELETE |Delete         |405 (Method Not Allowed), unless you want to delete the whole collection—not often desirable.|200 (OK). 404 (Not Found), if ID not found or invalid.|



# Security


## Common attacks
### XSS: Cross Site Scripting

User input malicious text, that gets executed as Javascript in the browser. 
    * steal user cookies, thus allowing pretending to be that user
    * modify page behavior

User inputs `<script>` tag, if the site doesn't escape it, and shows it on it's site again, or some how evaluates it. You then end up executing the user's input. 

XSS and SQl injection are similar, they both are caused by user inputting malicious text, the difference is one gets executes in the browser, one in SQL. 

### SQL injection
Cause: user input is not sanitized and used to construct SQL query. Resulting in bad sql queries getting executed, bad user gaining access to the system, record/table modification/deletion.

Solution: check user input strings for certain characters, or use tools to do scan for injection possibility.
q
### CSRF: Cross Site Request Forgery
Good video on this: https://www.youtube.com/watch?v=vRBihr41JTo&ab_channel=Computerphile

Problem: random/fake sites(client page) can mimic sending requests and changing stuff
Solution: add a token for each form requested, and validate the id when form is submitted




### Man in the middle attach


## Encryption

### Aspects of data security
Data encryption in Transit vs at Rest.

Data at rest is data which is not actively moving within the system or network and does not interact with any third-party applications such as data stored in hard drives, mobile phones, flash drives, laptop, etc.   

In-transit means ‘in motion’ or simply put, data moving from one location to another. It includes data traveling from network to network or data transfer from local storage to cloud storage.   


# basics
## CORS
https://github.com/30-seconds/30-seconds-of-interviews/blob/master/questions/cors.md

Cross-Origin Resource Sharing or CORS is a mechanism that uses additional HTTP headers to grant a browser permission to access resources from a server at an origin different from the website origin.

An example of a cross-origin request is a web application served from `http://mydomain.com` that uses AJAX to make a request for `http://yourdomain.com`.

For security reasons, browsers restrict cross-origin HTTP requests initiated by JavaScript. `XMLHttpRequest` and `fetch` follow the same-origin policy, meaning a web application using those APIs can only request HTTP resources from the same origin the application was accessed, unless the response from the other origin includes the correct CORS headers.

* CORS behavior is not an error,  it’s a security mechanism to protect users.
* CORS is designed to prevent a malicious website that a user may unintentionally visit from making a request to a legitimate website to read their personal data or perform actions against their will.


* [MDN docs for CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)



