# REST
## Principles
## Methods
Think of these four methods corresponds to CRUD.

|HTTP Verb|CRUD         |Entire Collection (e.g. /customers) |Specific Item (e.g. /customers/{id})|
|-------|---------------|------------------------------------|------------------------------------|
|POST   |Create         |201 (Created), 'Location' header with link to /customers/{id} containing new ID.|404 (Not Found), 409 (Conflict) if resource already exists..|
|GET    |Read           |200 (OK), list of customers. Use pagination, sorting and filtering to navigate big lists.|200 (OK), single customer. 404 (Not Found), if ID not found or invalid.|
|PUT    |Update/Replace |405 (Method Not Allowed), unless you want to update/replace every resource in the entire collection.|200 (OK) or 204 (No Content). 404 (Not Found), if ID not found or invalid.|
|PATCH  |Update/Modify  |405 (Method Not Allowed), unless you want to modify the collection itself.|200 (OK) or 204 (No Content). 404 (Not Found), if ID not found or invalid.|
|DELETE |Delete         |405 (Method Not Allowed), unless you want to delete the whole collection—not often desirable.|200 (OK). 404 (Not Found), if ID not found or invalid.|


# Security



## XSS: Cross Site Scripting

User input malicious text, that gets executed as Javascript in the browser. 
    * steal user cookies, thus allowing pretending to be that user
    * modify page behavior

User inputs `<script>` tag, if the site doesn't escape it, and shows it on it's site again, or some how evaluates it. You then end up executing the user's input. 

XSS and SQl injection are similar, they both are caused by user inputting malicious text, the difference is one gets executes in the browser, one in SQL. 

## SQL injection
Cause: user input is not sanitized and used to construct SQL query. Resulting in bad sql queries getting executed, bad user gaining access to the system, record/table modification/deletion.

Solution: check user input strings for certain characters, or use tools to do scan for injection possibility.
q
## CSRF: Cross Site Request Forgery
Good video on this: https://www.youtube.com/watch?v=vRBihr41JTo&ab_channel=Computerphile

Problem: random/fake sites(client page) can mimic sending requests and changing stuff
Solution: add a token for each form requested, and validate the id when form is submitted




## Man in the middle attach
