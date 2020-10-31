
# React questions
## Core concepts
### How does react work?
View of MVC

Front end apps on a high level is essentially doing two things:
* render content
* accept async interactions and do things like rerenders, and network calls.

At the core is the use of Virtual DOM: When state changes or new props received, react runs a diff of virtual dom, then updates the real dom.  

### How Virtual DOM works
The Virtual DOM is an abstraction of the HTML DOM. It is lightweight and detached from the browser-specific implementation details. 

ReactElements are represented in virtual DOM, and the real DOM is rendered based on virtual DOM. 

When state changes in ReactComponent, a diff is run on virtual DOM, and the diff is updated to real DOM. The point is the diff on virtual DOM is way faster, than it's done on real DOM. 

### What is JSX?
JSX is a syntax extension to JavaScript. Think of it as Syntax sugar for creating javascript objects. It provides a way for developers to easily define how elements are structured, and gets compiled into javascript objects. 

### What are the differences between a class component and functional component?

Class component is useful for stateful component, or container components. It provides access to local state, lifecycle hooks, store

Functional components usually used for presentational components, stateless components, that are pure functions that renders the DOM from props.

### props vs state
High level: both controls how the view is rendered, props gets passed from parent and are readonly, while state is managed locally by the component.

State
* local
* has default value
* mutate due to (async) interactions: user input, network calls
* rerender on change

Props:
* for component exchanging information
* immutable from inside. Only parent can change it
* two forms
    - object: top-dowm communication
    - function: bottom-up event bubbling
* rerender on change

### What are controlled components?
#### High level
this is about html elements. Instead the form elements maintaining their own state based on user input, react allows dev to handles this at the wrapping component level.

#### more detail
In HTML, form elements such as `<input>`, `<textarea>`, and `<select>` typically maintain their own state and update it based on user input. 

In React, the component containing these elements will store the value that controls these elements. A form element whose value is controlled by React in this way is called a "controlled component".

The benefit: With a controlled component, every state mutation will have an associated handler function. This makes it straightforward to modify or validate user input.

### What is a higher order component?
https://reactjs.org/docs/higher-order-components.html

A higher-order component is a function that takes a component and returns a new component.

HOCs are not part of the React API. They are a pattern that emerges from React’s compositional nature.

HOC’s allow you to reuse code, logic and bootstrap abstraction.

## React details
### What are the different phases of React component lifecycle?
Four different phases:
* **Initialization**: In this phase react component prepares setting up the initial state and default props.
* **Mounting**: The react component is ready to mount in the browser DOM. This phase covers `componentWillMount` and `componentDidMount` lifecycle methods.
* **Updating**: In this phase, the component gets updated in two ways
    - sending the new props: `componentWillReceiveProps` `shouldComponentUpdate`, `componentWillUpdate` and `componentDidUpdate`
    - updating the state: `shouldComponentUpdate`, `componentWillUpdate` and `componentDidUpdate`
* **Unmounting**: In this last phase, the component is not needed and get unmounted from the browser DOM. This phase include `componentWillUnmount` lifecycle method.

![alt text](https://miro.medium.com/max/700/0*xny6k-jnfIEoLTLJ.png "React lifecycles")

###  What is `React.createClass`?
React.createClass allows us to generate component "classes."

### What is `ReactDOM` and what is the difference between `ReactDOM` and `React`?

ReactDOM was split out from React since v0.14.

ReactDOM provides interaction with real DOM:
* mounting element
* direct access to DOM

React provides the rest:
* lifecycle hooks
* element creation
* state management
### What is children?
In JSX expressions that contain both an opening tag and a closing tag, the content between those tags is passed to components automatically as a special prop: props.children.
There are some methods available in the React API to work with this prop. These include `React.Children.map`, `React.Children.forEach`, `React.Children.count`, `React.Children.only`, `React.Children.toArray`.

This is **composition over inheritance**. 
### What is create-react-app?
the official CLI for React to create React apps with no build configuration.

It includes
> React, JSX, ES6, and Flow syntax support.
Language extras beyond ES6 like the object spread operator.
Autoprefixed CSS, so you don’t need -webkit- or other prefixes.
A fast interactive unit test runner with built-in support for coverage reporting.
A live development server that warns about common mistakes.
A build script to bundle JS, CSS, and images for production, with hashes and sourcemaps.

# Redux 
### What is Flux?
Flux is an application design paradigm, at it's core is **Unidirectional Data Flow**. action -> store -> view -> action. 

### The benefit of Unidirectional Dataflow(TODO)
easy to reason about the code. 
### What is Redux
The basic idea of Redux is that the entire application state is kept in a single store. The store is simply a javascript object. The only way to change the state is by firing actions from your application and then writing reducers for these actions that modify the state. The entire state transition is kept inside reducers and should not have any side-effects.

Redux is based on the idea that there should be only a single source of truth for your application state, be it UI state like which tab is active or Data state like the user profile details.

### what is an action
An object describing what has happened. All actions are centralized and happens one after another, no race condition to watch out for. 

they can be logged, serialized, stored, and later replayed for debugging or testing purposes.

### What is “store” in Redux?
Store is the object that holds the application state and provides a few helper methods to access the state, dispatch actions and register listeners. The entire state is represented by a single store. Any action returns a new state via reducers. That makes Redux very simple and predictable.

### What is a pure function?

* Its return value is the same for the same arguments (no variation with local static variables, non-local variables, mutable reference arguments or input streams from I/O devices).
* Its evaluation has no side effects (no mutation of local static variables, non-local variables, mutable reference arguments or I/O streams).

Thus a pure function is a computational analogue of a mathematical function.

### What is Redux Thunk used for?
Thunk is for triggering asynchronous operation, like fetching data, AKA side effects. Instead of dispatching an object as an action, we dispatch a function, and in that function we can define an async operation, that could do data fetching, and dispatch more actions. `dispatch` and `getState` are available as params in the thunk function. 

Redux provides `applyMiddleWare` so that middlewares like `thunk` can be used
Redux Thunk and Redux Saga, Redux Logic are libraries for handling side effects. 

### How would you disable the store redux, so it does not accept any changes to state?.
One way to do it is by setting an exit flag in the root state reducer, so it is set to true it just let the state pass unmodified.



TODO Q12

# References
[Frequently asked: React JS Interview Questions and Answers](https://medium.com/@vigowebs/frequently-asked-react-js-interview-questions-and-answers-36f3dd99f486)

TODO [31 Redux Interview Questions (ANSWERED) React Devs Must Know in 2020](https://www.fullstack.cafe/blog/top-26-react-redux-interview-questions-to-brush-up-2018)


TODO [An Introduction to JSX](https://www.sitepoint.com/an-introduction-to-jsx/)


Question on Frameworks:
Does react local state vs Redux: [Explained by Redux FAQ](https://redux.js.org/faq/organizing-state#do-i-have-to-put-all-my-state-into-redux-should-i-ever-use-reacts-setstate)

How seismic manage state, it seems each seismic component has it's own state. 
Is this state actually hoisted to the top in seismic. 
How does action handling actually work in seismic? 


read more on redux: https://redux.js.org/introduction/core-concepts
