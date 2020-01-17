# Chap 1
Lawlessness is good if you're a criminal, but in this book, we'll want to acknowledge and obey the laws of math.

# Chap 2: First Class Functions
It is obnoxiously verbose and, as it happens, bad practice to surround a function with another function merely to delay evaluation

a few examples of omitting redundant function calls.

Writing something like `(arg1, arg2, ...) => myFunc(arg1, arg2, ...)` is just simply unecessary. 
* this is equivalent to `myFunc`, since function is a first class object
* if one day you want to add one more `argn` to the argument list, you'll need to change all the places that call `myFunc` like this. 
* Besides the removal of unnecessary functions, we must name and reference arguments. Names are a bit of an issue, you see. We have potential misnomers - especially as the codebase ages and requirements change. Having multiple names for the same concept is a common source of confusion in projects. 
* There is also the issue of generic code. By using specific naming, we've seemingly tied ourselves to specific data. This happens quite a bit and is a source of much reinvention.

There's really no need when writing functional code. However, when interfacing with other libraries, you might have to acquiesce to the mad world around us.


# Chapter 03: Pure Happiness with Pure Functions

> A pure function is a function that, given the same input, will always return the same output and does not have any observable side effect.

Difference of `slice` and `splice`:
* `slice`: pure
* `splice`: mutates the original array

Pure functions:
* shouldn not mutate it's input
* should not depend on mutatable/non-local variables.
    - **Dependent on system state is disappointing because it increases the cognitive load by introducing an external environment.
    - this reliance upon state is one of the largest contributors to system complexity (http://curtclifton.net/papers/MoseleyMarks06a.pdf)

There's nothing intrinsically bad about effects and we'll be using them all over the place in the chapters to come. It's that side part that bears the negative connotation.

> A side effect is a change of system state or observable interaction with the outside world that occurs during the calculation of a result.

A list of examples of side effects:
* changing the file system
* inserting a record into a database
* making an http call
* mutations
* printing to the screen / logging
* obtaining user input
* querying the DOM
* accessing system state

**The philosophy of functional programming postulates that side effects are a primary cause of incorrect behavior.**
It is not that we're forbidden to use them, rather we want to contain them and run them in a controlled way-> *functors* and *monads* 

Side effects disqualify a function from being pure. 


**Pure functions are mathematical functions and they're what functional programming is all about.**


## benefits of pure functions
### Cacheable
* pure functions can always be cached by input. This is typically done using a technique called memoization
* You can transform some impure functions into pure ones by delaying evaluation. 
    - e.g. `const pureHttpCall = memoize((url, params) => () => $.getJSON(url, params));` returns a impure function given certain params. The function could be cached. 
    - The takeaway is that **we can cache every function no matter how destructive they seem**

### Portable/ Self-documenting/Self contained
Pure functions are completely self contained. 
* a function's dependencies are explicit and therefore easier to see and understand - no funny business going on under the hood。 the pure function must be honest about its dependencies and, as such, tell us exactly what it's up to **Self documented**
* we're forced to "inject" dependencies, or pass them in as arguments, which makes our app much more flexible. All variable things are parametized. To change a usage, instead of rewriting logic, we pass in different params
* pure functions can be run anywhere, because all the dependencies are from input, not environment **Portable**
* In a JavaScript setting, portability could mean serializing and sending functions over a socket. It could mean running all our app code in web workers. Portability is a powerful trait. 

### Testable
Pure functions make testing much easier. We simply give the function input and assert output.

*strongly encourage you to search for and try Quickcheck - a testing tool that is tailored for a purely functional environment.*

### Reasonable
referential transparency: A spot of code is referentially transparent when it can be substituted for its evaluated value without changing the behavior of the program.

This ability to reason about code is terrific for refactoring and understanding code in general. **equational reasoning**

### Parallel Code
we can run any pure function in parallel since it does not need access to shared memory and it cannot, by definition, have a race condition due to some side effect.

# Chapter 04: Tool 1: Currying
The concept is simple: You can call a function with fewer arguments than it expects. It returns a function that takes the remaining arguments.

the returned function remembers the first argument from then on via the closure. "pre-load" a function with an argument or two in order to receive a new function that remembers those arguments.


## Curry - special sauce

We can transform any function that works on single elements into a function that works on arrays simply by wrapping it with `map`, `sort`, `filter`...and other higher order functions (a higher order function is a function that takes or returns a function). We typically don't define functions that work on arrays

Giving a function fewer arguments than it expects is typically called partial application. Partially applying a function can remove a lot of boiler plate code. 

Pure function: Currying does exactly this: each single argument returns a new function expecting the remaining arguments. 


# Chapter 05, Tool 2: Compose: coding by composing
```
const compose = (...fns) => (...args) => fns.reduceRight((res, fn) => [fn.call(null, ...res)], args)[0];
```
a human friendly version:
```
const compose2 = (f, g) => x => f(g(x));
```

`f` and `g` are functions and `x` is the value being "piped" through them. The composition of two functions returns a new function.

In our definition of compose, the `g` will run before the `f`, creating a **right to left flow of data**. This is much more readable than nesting a bunch of function calls. We could define a left to right version, however, we mirror the mathematical version much more closely as it stands. **composition is straight from the math books**

NOTE: composition could very well be defined in a **left to right manner** 

Composition is associative, meaning it doesn't matter how you group two of them. `compose(f, compose(g, h)) === compose(compose(f, g), h);`(Why? pure functions!)

Since it is associative => we can just compose all funcs all together. `compose(exclaim, toUpperCase, head, reverse);`

> compose is available in libraries like lodash, underscore, and ramda.

One pleasant benefit of associativity is that **any group of functions can be extracted and bundled together in their very own composition**.

```
const loudLastUpper = compose(exclaim, toUpperCase, head, reverse);
//equivalent to:
const last = compose(head, reverse);
const angry = compose(exclaim, toUpperCase);
const loudLastUpper = compose(angry, last);
```

## Pointfree
**Pointfree style** means never having to say your data. Excuse me. It means functions that never mention the data upon which they operate. *First class functions*, *currying*, and *composition* all play well together to create this style.
* Currying allows us to prepare each function to just take its data, operate on it, and pass it along. **functions to be composed need to only take one input**
* we don't need the data to construct our function in the pointfree version, whereas in the pointful one, we must have our data available before anything else.

## Debugging
A common mistake is to compose something like map, a function of two arguments, without first partially applying it.

To debug a compose sequence is super simple, simply create an impure trace function, and add it to the composing sequence. 
```
const trace = curry((tag, x) => {
  console.log(tag, x);
  return x;
});
```

## Category Theory



