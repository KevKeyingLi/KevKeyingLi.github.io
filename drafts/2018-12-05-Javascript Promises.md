# Javascript Promises
This is the learning note for Udacity course Javascript Promises

# Overview
Promises is recomended way to handle asynchronous events in javascripts, according to MDN: *The Promise object represents the eventual completion (or failure) of an asynchronous operation, and its resulting value.* 

The course covers how to use Promises in four blocks:
* Wrapping: creating a Promise with asynchronous operation
* Thenning: [promise -value-> action] handling success 
* Catching: [promise -value-> recovery] handling failures
* Chaining: [promise -> promise -> promise]

A good note on promises: JavaScript Promises - Jake Archibald https://developers.google.com/web/fundamentals/primers/promises

Four states of a Promise:
* Fulfilled(resolved)
* Rejected
* Pending: Neither fulfilled, or rejected
* Settled: Either fulfilled, or rejected

##promise timeline
a promise can only settle once.

an event can fire as many times, but a promise can only settle once. 
Promise happens in main thread, so they are blocking. de-asynchronous-ed. 

## syntax
**Wrapping stage**:
 
Promise is a try-catch wrapper that could finish at anytime

Example: 
```
new Promise(function(resolve, reject)) {
    var value = doAsyncWork();
    if (thingsWorked)
        resolve(valueA);
    else if (somethingWhenWrong)
        reject();
}).then(function(valueA){
    //success
    doNextThing();
    return something;
}).catch(){}
```

code after `resolve` and `reject` are still executed.

Passing values or `undefined` through `resolve()` and `reject()` to `.then` and `.catch`: The values themselves aren't being passed to `.then` or `.catch`, rather they're being passed to the functions called by `.then` or `.catch`.

Usually `resolve` and `reject` are called in the async operations callback function. 

## Compare Promise-like implementations across web technologies
* Javascript native Promises come into being in 2014
* JQuery has it's own Promises, but had some serious issues
* 1 version of Angular use Q-style promises
* Angular 2 take advantage of native javascript promises
* Native Promises are not compatible with Opera mini, and IE(Dec 2015). 
* Service worker API: **a total game changer**, an additional layer between you and your network, you app can work offline. 
Next quiz: Fetch API for xml http request. 


A few links:
* Issues with jQuery Promises:
    - 
    - 10 June 2016 update! With the 3.0 release, jQuery promises now satisfy Promises/A+ compliance! https://blog.jquery.com/2016/06/09/jquery-3-0-final-released/
    - You're Missing the Point of Promises - Domenic Denicola (Pre-jQuery 3.0) https://blog.domenic.me/youre-missing-the-point-of-promises/
    - jQuery Deferred Broken - Valerio Gheri (Pre-jQuery 3.0) https://thewayofcode.wordpress.com/tag/jquery-deferred-broken/
* Q Style Promises
    - They're an implementation of the Promises/A+ spec. https://promisesaplus.com/
    - $q service Documentation. https://docs.angularjs.org/api/ng/service/$q
* Browser Implementation
    - Can I Use... - Promises https://caniuse.com/#search=promises
    - ES2015 Promises Polyfill https://github.com/stefanpenner/es6-promise
    - Q Library https://github.com/kriskowal/q
    - Bluebird Promises https://github.com/petkaantonov/bluebird
* APIs that Use Promises
    - Service Worker API https://developers.google.com/web/fundamentals/primers/service-workers/
    - Fetch API https://davidwalsh.name/fetch

## QUIZ: XHR is not easy to use(too complex), Fetch API simplifies it
Fetch API https://davidwalsh.name/fetch

A useful yet somewhat confusing quiz, when I `console.log` `response.json()` in the `get(url).then()`'s callback, it shows a promise, and when I log it in the `getJSON.then()` callback, it is an object. 

## Summary
Promises are thenable, thenable objects can be chained up as a chain of async work, catch is also thenable. 
* When creating a chain, each subsequent link in the chain will receive either 
    - the fulfilled value of the previous promise, or
    - the return value of the previous .thens function. 
This way, you can pass information collected from one async method to the next. 
The thenables: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise#Methods
# Lesson 2 Chaining.
### Error Handling Strategies: two syntaxes

Instead of `get().then().catch()` we can do `get().then(resolveFunc).then(undefined, rejectFunc)`, or simply `get().then(resolveFunc, rejectFunc)`. 

In case of `get().then(resolveFunc, rejectFunc)`, if there is no `resolveFunc`, this `then` will be skipped, and the next `then` will be called. 

In all cases when a promise is rejected, the javascript engine will skip to next reject function **in the chain**, a `.catch` or a `.then`. Anything going wrong inside of `.then` will also skip directly into the next reject **in the chain**. 

* `.then().catch` has better readability
* `.then(resolveFunc, rejectFunc)` will only execute one of the functions, while `.then().catch()` can both get called. 

resolve does not always mean success, read at https://jakearchibald.com/2014/resolve-not-opposite-of-reject/
### Actions in Series & Actions in Parallel
How do you make parallel calls appear in the correct order -> next chap
### Array Methods and Promises
#### forEach 
* run Promises in parellel with forEach, no order guarantee
* run Promises in sequence with forEach, ordered. But not efficient and the code is error prone. :
```
    var sequence = new Promese.resolve();
    arr.forEach(function(url) {
        sequence = sequence.then(function() {
            return get(url);//the real async call
        }).then(function(){
            //code that handles the async call
        });
    })
```


#### map
map each promise to an array which maintains the order?


#### promise.all

Promise.all(arrayOfPromises) {
    function(arrayOfValues) {

    }
}
returns an array of values in the same order as the original array of promises
.all fails fast, if one of the promises reject, the whole thing rejects. 
if all resolve, this resolves. 





