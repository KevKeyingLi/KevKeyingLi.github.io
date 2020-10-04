#
By Eric Freeman and Elisabeth Robson on LinkedIn Learning, authors of *Head First Design Patterns: A Brain-Friendly Guide to Design Patterns*

## Introduction
### Don't reinvent the wheel
designs should be
* flexible
* extensible
* more maintainable, resilient to change
* easier to communicate to your teammates


Central to these design patterns are a whole new set of design principles that go beyond the core object-oriented principles. These design principles will help you to avoid problematic designs and help you understand how design patterns work.

### What you should know
In this course:

Prerequisite: Knowledge with a OO language

UML to describe the pattern
Java to implement


## Design Patterns
### OOD experience
The goal flexible, extensible

OOD basic principles:
* inheritance
* Polymorphism
* Abstraction
* Encapsulation

Design Pattern go to your brain first, then to your code.

Design Pattern started from Gang of Four, with 23 patterns 

Benefits:
* not reinvent wheel
* building resilient code
* prepareing for future addition

### What are design patterns
Design patterns are all about reusing experience, design experience. Not algorithms, not code.

A design pattern is usually
* expressed by a definition and a class diagram 
* collected into a catalog of patterns.
 

patterns are pretty abstract, it's up to you to determine
* if the pattern is right for your situation and your specific problem
* how best to implement it.


Design patterns are not specific solutions for specific kinds of software. 

Rather, design patterns are general solutions for common problems that crop up in all kinds of applications.

In this course, we'll be focusing on six of the 23 original patterns in the Gang of Four Catalog. These are the patterns you're likely to find most useful because they're approaches to the most common problems that crop up as you design and develop a software system. Once you've learned how to read and understand these six patterns, you'll be able to explore more patterns on your own.

You'll find a more complete treatment of the original 23 patterns in our book: *Head First Design Patterns: A Brain-Friendly Guide to Design Patterns*. We'll
* describe each pattern conceptually
* talk about its object oriented design in the form of a class diagram
* show code snippets to show you the key features of a pattern implemented in code.

### What are design principles


* inheritance
* polymorphism
* abstraction
* encapsulation
* single responsibility
* open-closed
* loose coupling
* composition over inheritance
* program to an interface, not an implementation
* encapsulat what varies
 
And these principles really give you a set of guidelines that will help you to avoid bad object-oriented design
* too rigid
* inflexible
* too fragile
* too hard to understand

Principles are general guidelines while patterns are specific design solutions often aimed at solving common object-oriented problems.


Principles tell us to strive for a particular quality in our design, and this is often where patterns come in. Design patterns often demonstrate different ways of fulfilling the principle. 

An important principle: **encapsulate what varies**: Identify the aspects of your application code that vary and separate them from what stays the same. 

> e.g. separating what varies in our design ->
the strategy pattern, which shows us how to separate out an object's behavior. It's algorithm, if you will, in a flexible and extensible way. This also won't be the last you see of the encapsulate what varies principle. This one principle forms the basis for almost every design pattern. Almost all patterns provide a way to let some part of the system vary independently from the other parts. And as you'll see, different patterns do this in different ways depending on the problems they're solving.


## The Strategy Pattern
### Revisiting inheritance

Inheritance is one of the core concepts of object-oriented design. Through inheritance, you can express class relationships that allow you to reuse and extend the behavior and properties of other classes. Typically you think of one class inheriting from another if they share an IS-A relationship.

main benefit of inheritance: **code reuse**


Inheritance is a powerful technique, and there are many designs where inheritance is exactly the right choice. <-> While inheritance is a core concept in object-oriented programming, it's also easy to overdo inheritance and make it the basis of all your object-oriented design.

**if all your class relationships are IS-A relationships, take a closer look at your design.**

**overuse inheritance**: inflexible and difficult to change