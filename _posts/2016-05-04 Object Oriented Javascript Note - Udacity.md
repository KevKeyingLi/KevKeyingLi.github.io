This semester, I did my first JavaScript project without even knowing JavaScript before that. It was an unforgetable experience getting hands on all those stranger concepts and tools like anonymous function, JQuery, AJAX, D3JS... Finally, the end has came for this messed up semester, and I find some time to **Systematically** go through the details of JavaScript. 

This is the learning note that I wrote down, when I took the *Object Oriented Javascript* course on Udacity. This note was originally in my Evernote, but I figured it would be better to translate it into Markdown. 

The course is nice and compact. The description says it would take approx 5 weeks, but if you play the video at x1.5 and super focus, it could just take three or four days. For JavaScript beginners, I would suggest start with the JavaScript Basic[https://www.udacity.com/course/javascript-basics--ud804] course. Other nice related courses like Intro to AJAX[https://www.udacity.com/course/intro-to-ajax--ud110], JavaScript Design Patterns[https://www.udacity.com/course/javascript-design-patterns--ud989], could be found on Udacity website. 

---------------------------------
## Scope:

- in JavaScript only functions create new scope, if, else does not create new scope
- in function scope if assign an variable with out declaring, then the variable will be automatically be global. “a=1;” instead of “var a=1”

Execution Context : in memory scope, related to function calls
     The execution state of the code in memory
     This shows that the execution of the same function may return different result(of course reasonable )

## Closure:
Closures are functions that are still available when outer scope quits.
They are instances of functions.
To make inner function be usable by outer scope:

-      use settimeout
-      return the function
-      save the function to global var

Though a inner function can be accessed by the global scope, its execution context is still the inner scope. So actually, though the function returns, its execution context is still accessible because its inner function is still accessible.

## This
Stands for the current object. But sometimes can be confusing.
Two differences between normal parameters and this parameter:

- this is predefined. do not need to assign a name
- the way you bind values to this is different to others (about 5 different ways) see later.

example: what this refers to:
var obj = {
     fn: function(a,b){     log(this);     };
};
     var ob = {method: obj.fn};
     obj.fn(3,4)
Not the following: the function: {f}, a new instance of the function: {}, the method object fn in ob, the container object of the declaration of fn, the invocation of the function
Actually, this refers to the runtime caller of the function, the obj in obj.fn(3,4)
There is no parameter binding until a function is called.
This is just like an argument. It is only bound to value when it is invoked.
When no dot, the this is bound to global scope
fn.call(a,b,c) is a way to bind function to an object a, and b, c are its first and second parameters
callback functions are different

## Prototype Chain, just like inheritance in Java

make one object behave like another.
Example
     var gold = {a:1} //
     console.log(gold.a); //property look up
One time property copying
     var blue = extend({},gold);
     blue.b = 2;//new property
Prototype delegation: when accessing property, it fall through to the original object. If rose contain a, then use it, if not, fall through to gold
     var rose = Object.create(gold);
     console.log(rose.a); //on-going lookup-time delegation, rose fall through to gold for value of a

In javascript, there is a top level object that all objects eventually delegate to. the object prototype. Containing functions like .toString() .constructor()
Array prototype delegates to the Object prototype.

## Object Decorator Pattern

code reuse:
     write generalized code to work in many scenarios,
Functions makes it possible to refactoring
Decorator Function: use adjective as decorator function:
     example: var catlike = function(obj, loc){obj.loc = loc; return obj;} var car1 = carlike( {}, 1 )
Decorator Functions can be seen as taking an existing object and make it contain other properties.

Function classes

classes: usually defined as the constructor function, usually Capitalized.
The constructor function looks like the decorator function. But quite different
Decorator tends to duplicate the functions in memory.
Can move the definition of the function out of the constructor function. Called shared functions. like:

     var Car = function(){//this is a constructor
          obj.move = move;
          return obj;
     }
     var move = function(){//something;}

But this way is problematic —> can use something like extend(obj, methods); and methods is a global variable contains all the methods, like this:

     var Car = function(){//this is a constructor
          extend(obj, Car.methods);
          return obj;
     }
     Car.methods = {
          move: function(){/*do something*/}
          other: function(){;}
     };
This is similiar to what Javascript uses Prototype
In Javascript everything is a function!!!
In ES6, class are introduced.

## Prototypal Classes

Two ways of creating an object:

- var obj = {attr: val};
- Object.create(prototype method object)


With the <example> :

     var Car = function(loc){//this is a constructor
          var obj = Object.create(Car.methods);
          obj.loc = loc;
          return obj;
     }
     Car.methods = {
          move: function(){/*do something*/}
          other: function(){;}
     };

from last section(The car example), we can go on explore Javascript way of defining prototypes.
In JavaScript, every Object is already provided a prototype component that contains all the methods, which works the same way as the Car.methods in the <Example>

As the prototype already exists every time you create a new object, we don't need to define it, but just add methods into it as we needed:

     Car.prototype.move = function(){;}// move is a new function.
The <example> becomes this:

     var Car = function(loc){//this is a constructor
          var obj = Object.create(Car.prototype);
          obj.loc = loc;
          return obj;
     }
     Car.prototype.move= function(){/*do something*/};// adding a new function to Car class.

Some important details about this code snippet and how to comprehend the concept of Prototype:

- The constructor function is a function object. And prototype is its member. Prototype helps it to construct new objects.
- New objects constructed by the constructor, delegates their methods to the prototype. The constructor only constructs their member and assign this delegation.
- Each new object can be treated as an object of Car.prototype, because they all follow the behaviour of the prototype.
- A constructor's prototype usually means its member, and an object's prototype usually means the prototype it delegates to.

Each prototype in javascript, has a special member property of constructor which points to its constructor.
Car.prototype.constructor  = Car. All isntances of the object have this property, which can find its constructor.

## Psuedo Class Pattern
Javascript style of new .
Since all constructors of object inevitably contains a line of Obj.create() and a line of returning it. Javascript automatically adds these two lines for you when you invoke a function with the keyword new.
When using new, the Obj.create() and return obj; lines are automatically inserted. Thus the defination of a constructor function will not need those lines anymore.
var new-instance = new Car(loc);
The definition of Car only need to worry about its member properties. Adding functions to prototype if needed.
Use this to indicate the new object in the constructor function and prototype methods.  It looks like this:

     var Car = function(loc){
          this.loc = loc;
     }
     Car.prototype.move = function(){ this.loc++; };

functional

prototype/Psuedo-class

var Car = function(loc){
     obj = {loc:loc}
     obj.move = function(){
                obj.loc++;
          };
     return obj;
     };

This woul create a lot more function objects as the code is runing.

     var Car = function(loc){
          this.loc = loc;
     }
     Car.prototype.move = function(){
           this.loc++;
     };

## Superclass and subclass:
Now we know three class patterns: functional/prototypal and Psuedoclassical. \
Psuedo is more documented than the functional.

Creating subclass
In subclass, instead of calling Obj.create()
we call the constructor of the superclass like var obj =  Car(loc)
This is used in the functional pattern.

## Psuedoclassical Subclass
Use psuedocalssical pattern in base class.
To run a function in the context that we want it to, we can use the call() function.
The call function, binds its first parameter to its caller.
To define a subclass of a superclass, we can use the call function of the superclass in the subclass definition. To make the superclass constructor to be called in the context of the subclass. :

var Van = function(loc){
     Car.call(this, loc);// this line calls the Car function so that the this of the Car function is bound to the Van's instance.
};

So far, the loc property of van instance is delegated to a potential car instance, next is prototype. For now, van.prototype delegates to Object.prototype.
     Van.prototype = Object.create(Car.prototype);
     Van.prototype.constructor = Van
