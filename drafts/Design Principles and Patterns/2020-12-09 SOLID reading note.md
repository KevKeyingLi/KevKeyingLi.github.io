[SOLID Principles: The Software Developer's Framework to Robust & Maintainable Code [with Examples]](https://khalilstemmler.com/articles/solid-principles/solid-typescript/)

[S.O.L.I.D: The First 5 Principles of Object Oriented Design](https://www.digitalocean.com/community/conceptual_articles/s-o-l-i-d-the-first-five-principles-of-object-oriented-design#interface-segregation-principle)

S.O.L.I.D is an acronym for the first five object-oriented design(OOD)** principles** popularized by Robert C. Martin (Uncle Bob) in 2004-ish

* S - Single-responsiblity principle
* O - Open-closed principle
* L - Liskov substitution principle
* I - Interface segregation principle
* D - Dependency Inversion Principle

# Primary Benefits
* write code that's testable
* write code that's easily understood
* write code where things are where they're expected to be
* write code where classes narrowly do what they were intended to do
* write code that can be adjusted and extended quickly
* write code that can be adjusted and extended quickly without producing bugs
* write code that separates the policy (rules) from the details (implementation)
* write code that allows for implementations to be swapped out (think swapping out Email APIs, ORMs or web server frameworks)

## Single responsibility Principle
SRP: **A class should have one and only one reason to change, meaning that a class should have only one job.**

Design Tip: If we see lots of code in switch statements, that should be a signal to us of a potential refactoring from a switch statement to several classes.

## Open-closed Principle
**Objects or entities should be open for extension, but closed for modification.**Generally, this principle is all about writing your code in such a way so that when you need to add new functionality, it shouldn't require changing the existing code.

Intially written about by Bertrand Meyer in the 1980s, Uncle Bob calls this the "most important principle of object-oriented design". 

we write interfaces and abstract classes in order to dictate the higher-level policy that needs to be implemented, and then we implement that policy using concrete classes.**Coding to an interface is an integral part of S.O.L.I.D**

> Higher level-components are protected from changes to lower level components.

This goes hand-in-hand with the Dependency Inversion Principle of depending on an interface instead of concretions, and closely with Liskov Substitution Principle in terms of being able to swap out implementations as long as the same type/interface is being depended on.

### From an architectural standpoint
This principle still makes a lot of sense when we think about the larger picture of software architecture. **Always think of a system as a hierarchy, and identify the higher level components**

Example: use case/app server is the core(hier level) component, and different UI(web, mobile), database are less important, lower level components. Changes to lower level components shouldn't require change in higer level components.

## Liskov substitution principle
**Let q(x) be a property provable about objects of x of type T. Then q(y) should be provable for objects y of type S where S is a subtype of T.**: plain English: every subclass/derived class should be substitutable for their base/parent class.

In Uncle Bob's "Clean Architecture", he says:

>"To build software systems from interchangeable parts, those parts must adhere to a contract that allows those parts to be substituted one for another."

## Interface segregation principle
**A client should never be forced to implement an interface that it doesn’t use or clients shouldn’t be forced to depend on methods they do not use.** 
**Prevent classes from relying on things that they dont need.**


In an interface, if there are methods that are not common for all its subclasses, specify it as a seperate interface. So subclasses can inherit as needed, instead of being forced to implement unnecessary methods.

## Dependency Inversion principle

**Entities must depend on abstractions not on concretions. It states that the high level module must not depend on the low level module, but they should depend on abstractions.**This principle allows for decoupling from implementation.

Abstractions should not depend on details. Details should depend on abstractions.


# TODO
* [S.O.L.I.D The first 5 principles of Object Oriented Design with JavaScript](https://medium.com/@cramirez92/s-o-l-i-d-the-first-5-priciples-of-object-oriented-design-with-javascript-790f6ac9b9fa)
