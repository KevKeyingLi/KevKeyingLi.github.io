# GraphQL essential training
https://www.linkedin.com/learning/graphql-essential-training/
## 0 Intro

## 1 Setup and Introduction
### IDE and required tools
GraphQL doesn't require anything special outside of the tools you're currently using as a developer, so a good IDE or code editor will do the trick. There are some options with extensions or plugins that will make your experience as a developer smoother working with GraphQL. 
VSCode with a GraphQL extension that provides several nifty tools when working with this framework
Atom also has a few packages you can use to support you in your GraphQL development. atom-graphql, language-graphql

WebStorm, paid IDE with a GraphQL plugin

### GraphQL overview
GraphQL is a query language for any kind of APIs and is able to fulfill any queries across multiple databases. It's a query language.

The main benefits of using it is that you can ask for exactly what you want, and you get those results and nothing else.

GraphQL allows to describe what type of data you can expect.

### Server setup with ES6 support
For setting up our GraphQL environment
* a base server: node expressjs
* babel for declarative ES6 syntax to import and export our dependencies

steps:
* `npm init` to create a new package.json file.
* `npm install --save express nodemon` --save is for legacy npm
* `npm install --save-dev babel-cli babel-preset-env babel-preset-stage-0`
    - babel-preset-env for environment
    - babel-preset-stage-0: cover all the latest versions of JavaScript, like ES7 and further.
* insert a little script here when we start our server: `"start": nodemon ./index.js --exec babel-node -e js` 
    - nodemon: restart or refresh the server whenever we change a file in the server
    - `/index.js` where is the entry point of the server.
    - `--exec babel-node -e js` making sure that we can run ES6 code inside of node
* new file `.babelrc`: 
```{
    "presets": [
        "env",
        "stage-0"
    ]
}
```
    - two presets will allow us to run ES6 code in our server. It will precompile the code into JavaScript code that the browser or any JavaScript compiler can read.
* create another new file `index.js`
    - create the base server
    - get base URL `/` and do a request, response
    - listen to a port, e.g. 8080

> CH01/01_03/end :

```
import express from 'express';

const app = express();

app.get('/', (req, res) => {
    res.send('GraphQL is amazing!');
});

app.listen(8080, () => console.log('Running server on port localhost:8080/graphql'));
```
### The initial GraphQL setup
* create `schema.js`. 
```
import { buildSchema } from 'graphql';

const schema = buildSchema(`
    type Query {
        hello: String
    }
`)

export default schema;
```

* update server file to run GraphQL, `index.js`
    - import {graphqlHTTP} from express-graphql
    - import schema
    - create a new variable, `root`: this is basically resolver: resolversis the function that returns the data that we need when we make a query with GraphQL.
    - `app.use` to create a brand new path `graphql` and use graphqlHTTP
```
import express from 'express';
import {graphqlHTTP} from 'express-graphql';
import schema from "./schema";

const app = express();

app.get('/', (req, res) => {
    res.send('GraphQL is amazing');
})

app.listen(8083, () => console.log('running server on port 8083'));

//resolver: 
const root = {
    hello: () => {
        return 'Hi I am K'
    }
};

app.use('/graphql', graphqlHTTP({
    schema: schema,
    rootValue: root,
    graphiql: true
}));
```
* add new dependencies package.json: express-graphql, graphql


Now we can use graphiql to test our graphql service
Or directly accessing localhost:8080/graphql will show the web version of  GraphiQL
### Basic GraphQL schema
To be able to make graph QL queries you need to define a schema which defines the query type and resolver for each api input. 

* **type definition** provides what type of data we expect
* **resolver** gets the data for us

Example: 
* defining our friend's type for application and then resolve it with fake data
    - update schema
```
const schema = buildSchema(`
    type Friend {
        id: ID,
        firstName: String
        lastName: String
        gender: String
        language: String
        email: String
    }
    type Query {
        friend: Friend
    }
`)

```

* Update resolver to match the new type `friend`. 
```
const root = {
    friend: () => {
        return {
            'id': "12346",
            "firstName": "Kevin",
            "lastName": "Li",
            "language":"Klingon",
            "email": "kl@kl",
            "gender": "unknown"
        }
    }
};
```
* test in graphiQL




## 2 Types and Schemas
### Object types and fields

Everything in GraphQL is defined by types as we've done already in our schema. 

A type: 
* the shape of how this data will be 
* what type of data it expects


Different types"
* String, ID...
* Array of Type, e.g. emails: [Email]!
```
//Schema
const schema = buildSchema(`
    type Email {
        email: String
    }
    type Friend {
        id: ID,
        firstName: String
        lastName: String
        gender: String
        language: String
        primaryEmail: String,
        emails: [Email]!
    }
    type Query {
        friend: Friend
    }
`)
```
```
//index.js


const emails = [
    {email: "111@11.com"},
    {email: "2222@22.com"},
    {email: "3333@33.com"}
];

//resolver: 
const root = {
    friend: () => {
        return {
            'id': "12346",
            "firstName": "Kevin",
            "lastName": "Li",
            "language":"Klingon",
            "primaryEmail": emails[0].email,
            "emails": emails,
            "gender": "unknown"
        }
    }
};

```
### Query and mutation types
The query type is responsible for defining what will return when we make the query.


Mutations: GraphQL's way of changing data, updating, or creating new data

```
`
input FriendInput {
    id: ID
    firstName: String !
    lastName: String
    ...
}

type Mutation {
    createFriend(input: FriendInput): Friend
}
`
```


* create is a type Mutation
* type Mutation will use a resolver, e.g. createFriend
* this resolver will take an input, e.g. FriendInput.
* it will return a Friend.
So once we use that mutation, we'll use the resolver create a friend, take the input that we'll define in a second, and then return the friend of that new input.
* create an input, e.g. `input FriendInput` will take all the same values as the type Friend here
* make any of those values mandatory, use an exclamation point
 


Then go on in the index.js and change the resolvers

```
//index.js

const root = {
    //the friend resolve from previous
    friend: () => { return {...}},
    createFriend: ({input}) => {
        //node native crypto package
        let id = requrie('crypto').randomBytes(10).toString('hex');
        return new Friend(id, input);
    }
}
```


For the timing, we'll just use an in-memory database


When you do a mutation query, you have the possibility of returning something. You need at least to return one item. And usually the id is the one by default

### What is the resolver and its role

Resolvers are the functions that respond to queries and mutations. They are the function that gives us the result of the query. 

The standard approach: leave the schema only for type definition, so resolvers are defined separate from the schema. 
* you can get either have them in a separate file(`resolvers.js`) and then import them into your main server file
* or have them into your main entry server file, in this case our index.js. 


Resolvers have names that corresponds to schema fields, and returns object with the type/structre as specified by the schema.

### Scalar types

Scalar types are basic types that comes GraphQL and can be used without having to create type beforehand.
* int, for integers, your regular number
* float, which is a float number, which basically includes a decimal point. 
* string, for any list of characters, like we've used so far
* ID, which is a unique identifier for each entry in GraphQL
* boolean, which has a value of true or false.

For each field we enter into our type, like our friend type, we need to define what scalar type it takes.

### Enumeration types

Enumeration type, or commonly called enums, is a special scale type that allows you to define a specific set of data the field takes, and restrict the input to what you list in the enum type.
```
const schema = buildSchema(`
    ...
    enum Gender {
        MALE
        FEMALE
        OTHER
    }
`)
```

**all the fields inside of an enum should be uppercase**. 
For any change in your schema, always check your resolvers, just to make sure that you don't have to make any changes for it.

### List of types inside another
In many cases you will need to have inside of a field, multiple values. This is where you can create a type and use the array characters to signify a list of items inside the field.

```
const schema = buildSchema(`
    ...
    type Friend {
        ...
        contacts: [Contact]
    }
    type Contact {
        firstName: String
        lastName: String
    }
    input ContactInput {
        firstName: String
        lastName: String
    }
    input FriendInput {
        ...
        contacts: [ContactInput]
    }
`)
```

Then update the resolver.


### Using GraphQL tools
In the GraphQL community there are multiple tools you can use to work with your schema to keep it clean and use GraphQL syntax first like we've done thus far, but for some of the future subjects we'll cover, using an approach similar to the syntax used with GraphQL tools will be beneficial for us, and therefore we'll continue with this tool and refactor our code a little bit.


* `npm install --save graphql-tools`
* update schema
Instead of `const schema = buildSchema();`
```
//schema.js
import { resulvers } from './resolvers';
import { makeExecutableSchema } from 'graphql-tools';

const typeDefs = `... the schema`;
const schema = makeExecutableSchema({ typeDefs, resolvers});
export { schema };

//resolvers.js
/* instead of
const resolvers = {
    getFriend: () => {...},
    createFriend: () => {}
};
we do resolver map */
const resolvers = {
    Query: {
        getFriend: () => {}
    },
    Mutation: {
        () => {}
    }
}

//index.js
import { schema } from './schema';
//no need to import resolver, since it's built into schema
//And remove the rootValue from graphqlHTTP
app.use('/graphql', graphqlHTTP({
    schema,
    //rootValue: root,
    graphiql: true
}))
```



#### On a side note
In the community, two approaches to write schemas
* exactly the same as we've been doing here in this schema
* another one that has a lot more code to it and is also more JavaScript friendly.

See example here: https://graphql.org/graphql-js/cnostructing-types

##### First approach:
```
import { buildSchema } from 'graphql';
const shema = buildSchema(`
    ...
`);
```

##### Second approach

```
import graphql from 'graphql';

const userType = new graphql.GraphQLObjectType({
    name: 'User',
    fields: {
        id: { type: graphql.GraphQLString },
        name: { type: graphql.GraphQLString }
    }
});

```


## 3 Setting Up Persistence
Persistence generally means database
### Installing Mongo for GraphQL
* Install brew, MongoDB
* create folder for db `sudo mkdir -p /data/db`, `sudo chmod 777 /data/db`
* `mogod`
* install `mongoose` `npm install --save mongoose`
### Final setup of Mongo with GraphQL
* refactor directory structure
    - new folder `data`
    - move resolvers.js into `data`
    - move schema.js into data
    - update dependencies of imports
* new file `dbConnectors.js`
```
import mongoos from 'mongoose';
//Mongo connection
mongoose.Promise = global.Promise;
mongoose.connect('mongodb://localhost/friends', {
    useMongoClient: true
});

const friendSchema = new mongoose.Schema({
    firstName: {
        type: String
    },
    lastName: {
        type: String
    },
    gender: {
        type: String
    },
    age: {
        type: Number
    },
    language: {
        type: String
    },
    email: {
        type: String
    },
    contacts: {
        type: Array
    }
});

export const Friends = mongoose.model('friends', friends);
```
* In `resolver.js`, import mongoose, Friends and update query and mutation.
  

### Data persistence with SQL
* `npm install --save casual lodash sequelize sqlite`
    - casual: dummy data
    - lodash
    - sequelize: for creating and generate database
    - sqlite: sql inside of local project. 
* import loadash, Sequelize, casual
* define SQL schema
```
const sequelize = new Sequelize('database', null, null {
    dialect: 'sqlite',
    storage: './aliens.sqlite'
});

const Aliens = sequelize.define('aliens', {
    firstName: { type: Sequelize.STRING},
    ...
});

Aliens.sync({ force: true }).then(() => {
    lodash.times(10, (i) => {
        Aliens.create({
            firstName: casual._first_name,
            ...
        });
    });
});

export {Aliens};
```
* update graphql schema

## Mutations
run `npm start` to test the project so far. 


## Queries in Depth
## Next steps
* graphql doc
* apollo/graphql articles
* cheat sheet https://github.com/sogko/graphql-schema-language-cheat-sheet
* Graphql community on slack
* GraphQL and Relay, Other course
   - Data Fetching with Relay
   - Learning Apollo
