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

Inheritance is one of the core concepts of object-oriented design. Through inheritance, you can express class relationships that allow you to reuse and extend the behavior and properties of other classes. Typically you think of one class inheriting from another if they share an **IS-A relationship**.

main benefit of inheritance: **code reuse**

#### Don't overuse
Inheritance is a powerful technique, and there are many designs where inheritance is exactly the right choice. <-> While inheritance is a core concept in object-oriented programming, it's also easy to overdo inheritance and make it the basis of all your object-oriented design.

**if all your class relationships are IS-A relationships, take a closer look at your design.**

**overuse inheritance**: inflexible and difficult to change

### Limitations of inheritance
#### Example: design classes for duck simulator

* Duck: abstract
    - quack()
    - swim()
    - display(): abstract
* MallardDuck
    - display(): implementation
* RedheadDuck
    - display: impl

This looks fine and works fine until it doesn't
* what if we need a rubberDuck class, it doesn't quack
    - implement a quack in RuberDuck and override the super class's quack
* new feature request for Ducks to fly.
    - add `fly()` to base class Duck
    - override it in RubberDuck since it doesn't fly
* new duck type: DecoyDuck requested
    - need to override `fly()` and `quack()` again.


The problem with this design: 
* need to override inheritance for some ducks for fly and quack
* duplicated code for overriding fly and quack
hard to gain knowledge of all ducks from the abstract class
* changes to base class requires changes to other ducks
* hard to change runtime behavior

### Trying interfaces
* an interface defines the methods an object must implement in order to be a particular type. 
* An interface is an abstract type that specifies a behavior that classes must implement
* interfaces allow different classes to share similarities
* not all classes need to have the same behavior
#### Rework the duck example with interfaces
Interface Flyable
* fly()
Interface Quackable
* quack()
Class Duck
* swim()
* display()

MallardDuck extends Duck implements Flyable, Quackable

Problem with this approach:
* destroys code reuse, each duck will need to implement it's only fly and quack. 
* change to fly or quack would cause maintenance nightmare
* still not ally runtime change to behavior
    - how to simulate a duck to acquire ability to fly, or lose it during runtime.

### Get inspiration from design principles
#### 1. A review of our attempts

* inheritnace didn't work well
    - Behavior changes across subclasses and it's not appropriate for all subclasses to have all behaviors
* interfaces didn't work well
    - interfaces supply no implementation and destroy code reuse.

#### 2. revisit design principles

Encapsulate what varies: Identify the aspects of your application that vary and separate them from what stays the same.
* if some aspect of your code is changing that's a sign you should pull it out and separate it.
* by separating these parts, you can extend or alter them without affecting the rest
* this principle of what varies is fundamental

#### 3. go back to our design
* swim doesn't vary across classes
* fly and quack is changing for different ducks, so we need to extract it from the rest of the code.
* display is implemented in each duck


#### 4. another design principle
Program to an Interface, Not an implementation: clients remain unaware of the specific types of bojects they use, as long as the objects adhere to the interface that clients expect.

### Programing to an interface
new implementation after reviewing two principles

Interface FlyBehavior
* fly()

Class Quack
Class Squeak
Class Mute

Interface QuackBehavior
* Quack()

Class FlyWithWings
Class FlyNoWay

Class Duck
* FlyBehavior flyBehavior
* QuackBehavior quackBehavior
* setFlyBehavior()
* setQuackBehavior()
* performQuack()
* performFly()
* swim()
* display()

#### My Note
* Having behaviors as a member not a interface, transforms **Is-A** relationship to **Has-A** relationship. 
* somewhat composition over inheritance

### Applying the principles
A java implementation of this design.

### exploring the strategy pattern
Pulling out fly and quack behaviors from inheritance, and instead compose these behaviors with duck. 
* more flexible 
* more resillient to change. 

The class diagram of strategy pattern:

We have an inheritance hierarchy that defines the type of the objects that need a behavior and we have a HAS-A relationship between those objects and their behaviors. These behaviors can be anything. Any algorithm that an object might need to perform. 
By moving these algorithms out from the main inheritance hierarchy, we get the benefit of being able to choose which algorithm each object gets. We can change these algorithms at runtime and if multiple objects need to use the same algorithm, we get the benefit of code reuse too

The official definition of **the strategy pattern**:
The strategy pattern defines a family of algorithms, encapsulates each one and makes them interchangeable. Strategy lets the algorithm vary independently from clients that use it. 

**a family of algorithms** can be considered a strategy.

### Why HAS-A is better than IS-A
IS-A: inheritance
HAS-A: composition

when you put two classes together, with composition, instead of inheriting behavior, an object can then instead delegate that behavior, to the composed object.

#### Principle
Favor composition over inheritance: classes should achieve code reuse using composition rather than inheritance from a superclass.

composition generally leads to a more flexible design, and is often used as a design technique in a lot of design patterns.