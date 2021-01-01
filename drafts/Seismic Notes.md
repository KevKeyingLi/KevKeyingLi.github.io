# Seismic Basics

## Motivation
* Web components: web standard for extending the web platform and encapsulating behavior by defining a new HTML tag
* Built on web components, built to stand the test of time.
    - The internal implementation details, including the view technology, are free to change: react, snabbdom, etc
    - while the component contract, properties in and actions (events) out, remains intact. Based on the web components standard.

## Core Concepts
### Immutable data/state
* new state created from pure function, not mutation
* immutability ensures the state is always valid: makes it **easier to reason**, because no other code could change it without dev's knowledge

### Unidirectional Dataflow
* An action is dispatched from the view, state is updated by action, and the updated state is passed back to the view ad infinitum.
* no more bi-directional dataflow, making **reasoning(debugging) much easier**. 

### Effectful code is isolated
Any code that causes side effects (e.g., a state update) should only be ran in the effect function for an action handler.
* This keeps all other code free from side effects -> making code **easier to reason** about and test.
* side effects are easy to test because they are just functions that take arguments.

## Web Components
### Life cycles
Webcomponent has it's native life cycles, but Seismic recommends using the framework's life cycles. The reason:
* the life cycle code is decoupled from the view(web component tag), resulting in easier refactoring.

### Shadow DOM
The Shadow DOM provides true **encapsulation** for web components shielding components from fragility of the global environment that has plagued web application development. 
* styles are scoped. No styles bleed in or out.
* The DOM is isolated as well, so other libraries can’t accidentally select and manipulate the component’s DOM. All component views and styles are rendered in the Shadow DOM (shadowRoot).


### slots
a placeholder that the component author has chosen for consumers to insert markup

Benefit: it prevents a poor design: the parent could have knowledge of a child or vice versa. 

Slots are the **composition** model for components.

## Security of Seismic
* principle: don't render untrusted content
* JSX will escape malicious content, and render it as string
* `dangerouslyCreateElementFromString` to create element from trusted source
* url need to be sanitized before rendering
* Data should be sanitized before it is stored and retrieved from platform services. 

# snabbDom
# immer
https://immerjs.github.io/immer/docs/introduction

[Introducing Immer: Immutability the easy way](https://medium.com/hackernoon/introducing-immer-immutability-the-easy-way-9d73d8f71cb3)

Immer is a package that 
* helps with enforcing immutability
* reduce boilerplate code
* doesn't introduce new complex library specific way of writing code
## Features

Immer works by writting **Producers**
```
import produce from "immer"

const nextState = produce(currentState, draft => {
  // empty function
})

```

* `produce` is the way you specify what's the next state
* immer uses **structural sharing**, so
    - any part that is not changed are still using the same reference
    - any part that is modified is a new object
* produced states are auto freezed, any further modification is not allowed.
* currying on produce, so you can pass the 
* reduces boilerplate code, and doesn't introduce new libary specific things to learn(like a immutable)

## The inner working
 1) Copy-on-write. 2). Proxies

# structural sharing

# Side notes
## Redux 
a *predictable* state container for javascript apps
* for any javascript, not just react
* state container
* predictable: all state transition are explicit and easy to keep track of. **easy to reason**

Core concepts:
* store: holds the state of your application
* action: describes the changes that happened 
* reducer: updates the state, based on the action

Principles
* State in a single store: the state tree
* only way to change state: emit an action, an object describing what happened. Instead of directly update state object
* **Pure** reducers: specify how the state tree is transformed by actions. `(prevState, action) => newState

Why react need redux?
* in react, shared data need to be lifted to parent component. if this sharing continue to change over time, it means continued state lifting.
* Everytime a child need an exising piece of data as a new prop, change need to be made in the parent. 
* functions are passed to child when child need to update parent state.

Redux lift all the state data out side of the react component tree, and each component can reference the data they need. 