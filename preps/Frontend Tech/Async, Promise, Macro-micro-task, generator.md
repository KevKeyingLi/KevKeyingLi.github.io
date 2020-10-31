# [Asynchrony: Under the Hood - Shelley Vohr - JSConf EU](https://www.youtube.com/watch?v=SrNQS8J67zc&t=459s&ab_channel=JSConf)

Event loop: an endlessly running singly threaded loop, where each iteration, it runs some code.

Microtask: comes with ES6 

Javascript has **run-to-completion** semantics, each task has complete control over all current states. 
* current task always finishes before next task
* or it explicitly yield control to event loop.

Components of Browser engine:
* call stack: for function calls
* heap: irrelevant variables?
* task queue(s) for managing tasks
    - macro
    - micro
* event loop: to execute tasks


## Callbacks are big in async world
**Callback hell**: nested callbacks...often identified by the **pyramid shape and all the `})` at the end**

Callback hell is hard to read and reason with, human brain like to read top down, not skipping around. 


Inversion of control: hand things to callbacks, and hope them do the right thing. The callbacks are like blackboxes to the functions accepting a callback, this creates trust issues.

To better understand the **IoC blackboxes and trust issues with callback**: https://www.youtube.com/watch?v=bAlczbDUXx8&ab_channel=StevieJay
* in short: passing a callback for someone else to execute is unsafe, while when using promise, you'll only get a resolved value, and you'll do your next step with that value, instead of someone else doing it for you.

In callback land, two ways error is reported:
* callback: handled within the callback. 
* exceptions: exception thrown from the callback, expecting someone else might be able to handle.
    - In async world, this won't be good, since the exceptions are synchronous. Throwing it out from callback, will lose context. 
    - In callback hell, this is hard to reason, what the context of exception is. 

One aspect of dealing with errors in callbacks, is to make sure it all been handled. 

## Promises
Before promise, javascript engine only executes what it is told to. And dev need to arrange the things by timeouts and callbacks to shuffle their place in the event loop.

Promises comes in ES6, with the invention of microtasks.

Promises act like placeholders, making devs able to reason about things that haven't happened yet. 

When it settles, it becomes an immutable value

Promises still uses callback, but they changes where the callback has passed to, and remove the blackbox effect. Promise gives us a function for us to know when the async is completed and act on it. 


traditional callbacks is just 

```
//A asyc-ly calls callback that calls B, and B doing the same to C
//A, B are Async, execution sequence: A, D, B, C
A(() => {
    B(() => {
        C();
    });
})
D();
```


promise:

```
const p = Promise.resolve('hello');

p.then(val => {
    return `${val} world`;
}).then(newVal => {
    return newVal + '!';
});

```

Promise chaining makes it easy to do a sequence of async steps.

Two Promise characteristics that allow us to do async in steps:
* `.then()` **creates** and returns a new promise, or thenable.
* the fulfilled value is passed to next `then()`'s callback as a param

Microtask: here is a thing I need to do later, but I want to do it immediately later, before anything happens. 

Think of Microtask queue attached to each tick of the event loop. 


When a promise is resolved/rejected, the callback is called asynchronously as a microtask, and added to the microtask queue for the current tick. 

With microtask queue:
* current task comes from either macrotask, or microtask
* microtasks generated during the current task, are added to the current microtask queue
* only when microtask queue is empty, the next macrotask can be executed.
* infinite microtask calls can drain the system. 


errors in promises:
* if not handled, it'll fail silently
* to handle error, add `.catch()` at the end of promise chain
* if exceptions are thrown in `.then()` or `.catch()` callbacks, these will convert it to rejection. 


## Generators

Key of generator is their behavior around run-to-complete.

Generators can pause in middle of execution and allow other code to run. 

Main benefit: generators provide a single threaded synchronous-looking code style, but allow us to hide the async away as implementation details. 

By hiding async, we can read the code as if it's sync, and care about the async piece later, separately. 
```
function* counter() {
    let index = 0;
    while(true) {
        yield index++;
    }
}
const gen = counter();
gen.next().value;//0
```




* \* indicates it's a generator
* `yield` is like return, it returns the value and pauses the generator
* generator returns a iterator, and everytime next() is called, it runs until yield is met. 
* generator can be **restarted** with specific value, that value will be returned in the next `next()` and the generator continues to operate
* you send message out with `yield`, and send message in with each **restart**.
* code inside the generator is synchronous
* since it's synchronous inside of generator, you can simple `try-catch` any error inside.
* you can even `.throw()` an error into the generator, and that will be catched by the generator's try-catch.  


## Async/Await
To simplify the process of chained promises. async-await always returns a promise.

Async, Await are non-blocking, and make Async code look like sync code.

* async-await works like promises, use microtask queue
* await will return the resolved value of a promise, instead the promise itself
* Missing await may result in returning a promise, not a value.
* **Attention** `await` in same code block are called sequentially. compare the following:

```
async function getAddress() {
    const street = await getStreet()
    const city = await getCity()
    const state = await getState();
}

async function getAddressParallel() {
    let [street, city, state] = await Promise.all([getStreet(), getCity(), getState()])
}
```
Error handling(22:30)
When using promises with sync code, error are catch at different places, resulting in potential duplcation:
* sync error handled by try-catch
* promise error handled by promise.catch()


When using async-await, a big try-catch block will catch all the errors inside of it, either it's from sync part, or async

## Summary
* Nested callback hell is hard to reason with.
    - lack of sequentiality
    - lack of trust
    - simple functions, easy to work with for simple tasks
    - no knowledge of async is required
    - complex async steps becomes nightmare, even with good modularity
    - error handling is hard to do if it's complex
* Promises
    - easier to reason about
    - useful for coordinating multiple async operations
    - propagate error from nested async
    - dynamically chain async
    - error handling can still be unintuitive. 
* async-await: syntax sugar on promises
    - more intuitive reading of async code
    - improved error handling compared to promises, simple try-catch block will do
    - Ironically/Jokingly, it looks so sync, that you may forget it's async when writing it.