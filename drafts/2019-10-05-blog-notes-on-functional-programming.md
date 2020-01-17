# Curry and Function Composition - Eric Elliott Medium
https://medium.com/javascript-scene/curry-and-function-composition-2c208d774983

## Covers following key concepts
* A **curried function** is a function that takes multiple arguments one at a time.
* A **partial application** is a function which has been applied to some, but not yet all of its arguments. In other words, it’s a function which has some arguments fixed inside its closure scope. A function with some of its parameters fixed is said to be partially applied.
* Point-free style is a style of programming where function definitions do not make reference to the function’s arguments. Me: I don't get it.
* **trace** Function composition using point-free style creates very concise, readable code, but it can come at the cost of easy debugging. trace() is a handy utility that will allow you to do just that.
* **Composition**: Curried functions are particularly useful in the context of function composition.

# article's conclusion

> A curried function is a function which takes multiple parameters one at a time, by taking the first argument, and returning a series of functions which each take the next argument until all the parameters have been fixed, and the function application can complete, at which point, the resulting value is returned.
A partial application is a function which has already been applied to some — but not yet all — of its arguments. The arguments which the function has already been applied to are called fixed parameters.
Point-free style is a way of defining a function without reference to its arguments. Generally, a point-free function is created by calling a function which returns a function, such as a curried function.
Curried functions are great for function composition, because they allow you to easily convert an n-ary function into the unary function form needed for function composition pipelines: Functions in a pipeline must expect exactly one argument.
Data last functions are convenient for function composition, because they can be easily used in point-free style.


# Util functions that are available
* curry
* compose and pipe
* trace
* flip




