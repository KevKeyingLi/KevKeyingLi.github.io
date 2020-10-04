# Learning GraphQL

## Intro

## 1 What is GraphQL
### Intro and history
* GraphQL is a **declarative data fetching** specification and query language 
* was created at Facebook in 2012. 
* open sourced GraphQL in 2015. 
* GraphQL is just a query language. Lanuage agnostic
* used by companies like Pinterest, Intuit, Coursera, GitHub, and Shopify, and it's gaining popularity due to the ease of use and the performance benefits.

### Why?


REST, or representational state transfer. Now, there are many different flavors of REST, but typically we'll request or update resources on different URI's. 

e.g. Let's say we have some data about Ohio. To fetch all of the data about Ohio, I could find it at the /api/ohio route. Then we might make another get request for some data at the Cleveland route. This all starts out very innocently, but REST endpoints have a way of quickly starting to multiply as our data-fetching needs expand. If we're looking for people in Ohio with hats, we might create a custom endpoint for this data. Requesting it would require several different requests, one for Ohio, another for people, then we have to find all of the people with hats in Ohio. The chaos starts to pile on pretty quickly, and due to this, the response time can be slower than we'd like, or slower than is acceptable on mobile networks. 

With GraphQL, we define a query. A query looks a whole lot like a JSON object without the values. Then we send this query as a string to a GraphQL server. We notice that the response looks a whole lot like the query. With our query, we specify exactly the data that we need, and we get nothing more than that. As we change the data that we want to fetch, we can update the query and fill in the fields. The query is nested and issued at once.

> So here if we're looking for a state with a name, population, and people, all of those are going to be nested inside of one another. Then, if we need to access the value of fields from one of the objects inside of the people array, we're going to request that once also. 
 
This is particularly useful when loading UI components. We'll populate the components with data, and we'll only ask for it in one request. 

ton of benefits
* It defines the shape of the desired data it calls for at once. This way we **avoid multiple REST calls, and the performance problems of over and under-fetching**.
* GraphQL is also **backwards compatible and version-free**, meaning you can add new fields to an existing GraphQL server without breaking the current clients and old fields can be deprecated and can still continue to function. 
* We can also use GraphQL to wrap around our existing API. So you don't have to set up everything from scratch, you can use it as part of your existing setup.
* GraphQL is language agnostic, so you can implement GraphQL solutions in a range of different languages.


### GraphiQL and Github API
After years of using REST for their APIs, GitHub open sourced the Graph API in 2016 at GitHub Universe.

A good resource on this API is an article from the GitHub Engineering blog. This describes really well the process and methodology, behind the launch of this GraphQL API.

I also want to bring your attention to the GraphQL GitHub API explorer.

This uses another tool called GraphiQL, which is sort of like an in-browser IDE that you can use to run queries. 

## 2 GraphQL Queries
### Create basic queries

**The query has the exact same same shape as the results.**

Also, a quick note here that queries can have comments. All of these are going to start with a pound symbol or hash.

### Use multiple fields

If you're wondering what fields are available not just by letter, but all of them. What you can do is hit *control and space* and that's going to populate an entire list for you. Awesome. 


Now keep in mind when I make this query this is returning the live data to me. 

So prettify is something that you can use as your queries start to become more complex and sometimes the spacing gets off-kilter.

Awesome, so we're querying the viewer field, we have many different nested fields inside of the viewer fields. All of this is returning live data from the GitHub API.

### Passing arguments
By querying fields, we've already been able to gather a ton of useful data. With arguments, we can drill down into specific fields to select specific data. In GraphQL, every field and every nested object can have its own set of arguments. 

when we want to add any arguments
* use parentheses
* use the argument and set that equal to some value

Awesome. So we've requested the data for repositoryOwner, associated with a particular login, provided from the arguments.


### Required arguments

double quotes are a requirement. You have to use them, single quotes aren't going to work.

And we see our first error message over here on the right. And it says, field repository is missing required arguments, owner. So this is really descriptive about which argument must be provided. So, I can make an educated guess here that I also need to add owner. So, I'm just going to comma separate this and I'll say owner and I'm going to look for the owner of this account and that's going to be Facebook.

So there we go the repository field takes in two arguments, both are strings and both are required. In the next videos we're going to take a closer look at how these fields and arguments are set-up in GraphQL schema.


## 3 Understanding Schemas
### What is a GraphQL schema?

The schema
* provides all of the different object types 
* specifies the types for all of these values. 

What's nice about using the graphiQL interface is that the schema is very well documented right here in the browser.
* click on this docs option
* we provide a schema, the documentation will automatically generate.
* 
So, here we have two different types. We have **queries** for getting data, and we have **mutations** for changing data, which we'll discuss in a later chapter.

### View schema types
These are all really well documented in the GraphiQL Documentation Explorer. So if we want to see what Types are available in the Schema, we can always look for them, and the Types are these capitalized Objects. 

We have all of these different Types associated with the field. So these are more common Types, like Booleans, or Strings, et cetera. 

When a Schema is defined, we are similarly specific about the types of Input Values that are allowed. These could be Argument Values, or Field Values.

possible Types
* Integers
* Floats
* Strings
* Booleans
* Null
* Enums
* Lists
* Objects

**if we see an exclamation point, we know that this is required.**

GraphQL is self-documenting. When we define the Schema, the documentation is created.


### Query the __schema
In addition to the built-in documentation in the graphical interface, you can query the schema directly. This is particularly useful when we're working outside of the graphical interface. 

```
{
    __schema {
        queryType {
            name
            description
            fields {
                name
                description
            }
        }
    }
}

{
    __type(name: "blabla") {
        kind
        name
        description
    }
}

```

So, we can look at the values that are part of the schema, inside of the graphical interface or we can query the __schema or __type fields to check out the architecture and the values.


## 4 Handling Data

### Aliases


There's an argument conflict because we've made a request for the same field with two different arguments. So to solve this, I can use an alias. 

**Aliases allow us to give the field a customized name and to request data from the same fields with different arguments**. 

keep this in mind when using aliases. They mess up the auto-complete features a little bit in GraphiQL.

### Fragments

Fragments are reusable sets of fields that can be included in queries as needed.

Now there are many different choices. You can use fragments on any of your objects. 

To use a fragment, use three dots and then the name of the fragment.

What these three dots are going to do is it's going to take all of our fields and spread them out into each of our queries.

So **fragments are used heavily in GraphQL**. It makes it easier to request for recurring fields and this is **particularly useful when populating data into user interface components that use the same data**.

### Nested fields

error message"you must provide a 'first' or 'last' value to properly paginate the 'repositories' connection". It means it's looking for an argument


So we've used nested fields inside of our original query. Next, we'll take a look at the schema and get a better sense of what's going on within this repositories field.


### Connections

In the previous video, we looked at this viewer query. Then we added the Repositories field, a plural, which indicates that there's multiple different values for this field. We can take a little bit of a closer look inside of our docs panel to figure out what's going here.

The RepositoryConnection represents the *relationship between our one field and another object.* *A **one to many** relationship*. We have a Repositories field and that's connected to each individual Repository. You can think of it like an array of objects. Now *Edges represents a connection to another array of data*. And then *each Node is an individual Repository*.

**Connections field, with Edges and Nodes is a common pattern. This pattern can be used for many different types of data.** e.g.
* An album might be connected to many different songs.
* a ski resort might have a connection with many different lifts

From a OOD point of view, connection is a interface, that different types of connnectionImpls can implement. 

This mirrors how many data relationships look already. And we're just handling it using the language of GraphQL with Connections, Edges, and Nodes.


```
repositories: {
    edges: [
        {
                node: {
                    id: "..."
                    name" "..."
                }
        },
        {...}
        ...
    ]
}
```


### Multiple nested fields

One of the most important benefits of working with GraphQL is the fact that in one request, we can get all of the data that we need, even from complex, nested fields.


With multiple level of nested fields, we can query for this set of tiered data in just one simple request.


### Pagination and filtering

In addition to `first` and `last`, there are numerous other ways to **paginate results**. They are defined in the schema, and used through arguments

Check for schema doc for info, what are the arguments for a field.

## 5 Operations and Variables
### Operation names
```
{
    organization(login: "facebook") {
        id
        name
        ...
    }
}
```


So this syntax here is actually a shorthand. We're omitting the optional `query` keyword from line 1. If you've ever worked with anonymous functions in your programming language of choice, this is a similar concept. 

The query works, but it might be a little harder to find this query in a sea of others in your code base. As an alternative, you can **create an operation name, or query name**, to distinguish queries from one another.

It's commonplace to see these query names capitalized. But it'll work with lowercase letters as well.

```
query MyQuery {
    organization(login: "facebook") {
        id
        name
        ...
    }
}
```


### Variable definitions

In the previous video, we looked at how to create an operation name to keep better track of our queries. Now, we're going to make these queries more dynamic by incorporating query variable definitions.

```
query MyQuery($myVar: String!) {
    organization(login: $myVar) {
        id
        name
        ...
    }
}
```


As soon as I set up a variable, GraphiQL is going to recognize it in the query variables panel.

With variables, we can make our queries much more flexible and dynamic using this query variables panel.


### Multiple variable definitions

So GraphQL is always keeping us really honest when it comes to types. It's very sensitive about that, so this is very useful when dealing with data.

So you can set as many of these variable definitions as you'd like to. You just need to make sure you're setting it to the right type.

### What is a mutation?

In GraphQL, data modifications are made with mutations.
* PUT, DELETE in REST
* instead of sending new data to a route, we're going to send data as a payload in the mutation.
* GraphQL assumes a mutation has side effects, and changes the dataset behind the schema.
* The API defines which mutations are allowed, and they, like queries, are in a specific shape.
 

all of the names of the possible mutations are created in the API, so when you create your own graph server, you'll be able to define your own mutations.

not all GraphQL APIs have mutations


### Create mutations
The GitHub GraphQL API has a ton of different mutations that we can take advantage of. Docs panel -> Mutation

this should demonstrate that mutations are fairly easy to execute, and they're very repeatable.


### Add a reaction mutation(github reactions in comments)

I personally think that's very fun. It's a fun way to practice with these mutations, addReaction and addComment are just two of a great many mutations that you can use on the github API, and I encourage you to play around with more of them.

## Conclusion
### Next step
Courses:
* GraphQL Essential Training
* Learning Apollo
* GraphQL: Data Fetching with Relay
 

You should also check out
* the documentation for GraphQL
* the documentation site for Apollo

# My summary

