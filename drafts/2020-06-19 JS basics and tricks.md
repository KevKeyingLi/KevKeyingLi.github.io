## Basics

### [JS Standard built-in objects](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects)
...

Function properties
* isNaN()
* eval()
* parseInt()
* parseFloat()
* encodeURI() decodeURI()

...

### setTimeout
#### setTimeout without delay
```setTimeout(function() {
    ...
}, 0);
```

https://stackoverflow.com/questions/9083594/call-settimeout-without-delay
#### wrap setTimeout in a promise
setTimeout(F, t);

new Promise((resolve, reject) => {
    if ()
        resolve(someValue);
    else
        reject(someValue);
})

new Promise((resolve) => setTimeout(resolve, time));

Sleep in async function
```await (async () => new Promise(resolve => setTimeout(resolve, 1000)))();```

### bind apply call
#### [bind](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_objects/Function/bind): The `bind()`` method creates a new function that, when called, has its this keyword set to the provided value, with a given sequence of arguments preceding any provided when the new function is called.
```let boundFunc = func.bind(thisArg[, arg1[, arg2[, ...argN]]])```

Usage:
* Creating a bound function
* Partially applied functions
* With `setTimeout()`
* Bound functions used as constructors
* Creating shortcuts


#### [apply](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/apply)
The apply() method calls a function with a given this value, and arguments provided as an array (or an array-like object).

```func.apply(thisArg, [ argsArray])```

#### [call]()


### replacing bad spaces

```
export function replaceBadSpaces(string) {
	return decodeURIComponent(
		encodeURIComponent(string).replace(
			/%09%09|%C2%A0%20|%20%C2%A0|%C2%A0%C2%A0/g,
			''
		)
	);
}
```
## Concepts
### [Closure](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures)
Functions form closures. A closure is the combination of a function bundled together (enclosed) with references to its surrounding state (the lexical environment). In other words, a closure gives you access to an outer function’s scope from an inner function. In JavaScript, closures are created every time a function is created, at function creation time.

#### usage
Closures are useful because they let you associate data (the lexical environment) with a function that operates on that data. This has obvious parallels to object-oriented programming, where objects allow you to associate data (the object's properties) with one or more methods.

Consequently, you can use a closure anywhere that you might normally use an object with only a single method.

Every closure has three scopes:
* Local Scope (Own scope)
* Outer Functions Scope(could be chained by nesting functions)
* Global Scope

### [Hoist]

var hoists to function scope. 


### Macro tasks vs Micro tasks
JS runtimes are single threaded
Two queues for tasks 
