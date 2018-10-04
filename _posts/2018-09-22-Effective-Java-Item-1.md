# Chapter 2 Creating and Destroying Objects

## Item 1 Consider static factory methods instead of constructors:

A class can provide its clients with static factory methods instead of, or in addition to, public constructors. Providing a static factory method instead of a public constructor has both advantages and disadvantages. 

Example: 

```
    public static Boolean valueOf(boolean b) {
          return b ? Boolean.TRUE : Boolean.FALSE;
}
```

## Terminologies 
**instance controlled**
The ability of static factory methods to return the same object from repeated invocations allows classes to maintain strict control over what instances exist at any time. Classes that do this are said to be instance-controlled.

**service provider frameworks** e.g. JDBC 
A service provider frameworks is a system in which providers implement a service, and the system makes the implementations available to clients, decoupling the clients from the implementation

There are three essential components in a **service provider framework**: 
* a *service interface*, which represents an implementation; 
* a *provider registration API*, which providers use to register implementations; and 
* a *service access API*, which clients use to obtain instances of the service. The service access API may allow clients to specify criteria for choosing an implementation, return a default implementation, or let client cycle through all available implementations. This is the flexible static factory that forms the basis of the service provider framework.
* An optional fourth component of a service provider framework is *a service provider interface*, which describes a factory object that produce instances of the service interface.

There are many variants of the service provider framework pattern:
* the service access api can return a richer service interface to client than the one furnished by providers. *Birdge pattern [Gamma 95]*
* *Dependency injection framworks (Item 5)* can be viewed as powerful service providers.
* Since Java 6, the platform includes a general-purpose service provider framework, *java.util.ServiceLoader (Item 59)*, which you should generally use
* JDBC doesn't use ServiceLoader, since it's earlier.

## Benefits/reasons:
1.  Unlike constructors, **static factory methods have names**
    - a well-chosen name results in client code easier to read. 
    - Creating multiple constructors with different param types is bad. replacing multiple constructors with same signature with static factory methods with carefully chosen names highlights their differences.
2.  Unlike constructores, **static factory methods are not required to create new object each time they're called.** 
    -   This allows *immutable classes[Item 17]* to use preconstructed instances or cache and reuse constructed instances. e.g. Boolean never creates an object.
    -   This is similar technique to *Flyweight pattern*
    -   improves performance, if equivalent object is requested often and expensive to create.
    -   This ability makes the classes **instance controlled**. There are several reasons to write instance-controlled classes. 
        +   Instance control allows a class to guarantee that it is a *singleton (Item 3)* or *noninstantiable (Item 4)*. 
        +   Also, it allows an *immutable value class (Item 17)* to make the guarantee that no two equal instances exist: a.equals(b) if and only if a == b. This is the basis of the *Flyweight pattern [Gamma95]*. *Enum types(item 34)* provide this guarantee.
3.  A third advantage of static factory methods is that, unlike constructors, **they can return an object of any subtype of their return type** -> great flexibility in choosing the class of the returned object.
    -   One application of this flexibility is that an API can return objects without making their classes public. Hiding implementation classes in this fashion leads to a very compact API. This technique lends itself to *interface-based frameworks (Item 20)*, where interfaces provide natural return types for static factory methods.
> Prior to Java 8, interfaces couldn’t have static methods. By convention, static factory methods for an interface named Type were put in a *noninstantiable companion class (Item 4)* named Types.”  java.util.collections has 45 convenience implementations of its collection interface, nearly all of these implementations are exported via static factory methods in one non-instantiable class java.util.Collections, the classes of the returned objects are all non-public. examples: java.util.Collections and java.util.EnumSet(Item 36).
> The Collections Framework API is much smaller than it would have been had it exported forty-five separate public classes, one for each convenience implementation. It is not just the bulk of the API that is reduced but the conceptual weight: the number and difficulty of the concepts that programmers must master in order to use the API.
> Java 8 requires all static members of an interface to be public. Java 9 allows private static methods, but static fields and static member classes are still required to be public.
4.  A fourth advantage of static factories is that the class of the returned object can vary from call to call as a function of the input parameters. Any subtype of the declared return type is permissible. 
5.  A fifth advantage of static factories is that the class of the returned object need not exist when the class containing the method is written.

##Limitation/Shortcoming
* The main limitation of providing only static factory methods is that classes without public or protected constructors cannot be subclassed.
    - Arguably this can be a blessing in disguise because it encourages programmers to *use composition instead of inheritance (Item 18)*, and is required for *immutable types (Item 17)*
* A second shortcoming of static factory methods is that they are hard for programmers to find. They don't stand out in API docs as constructors. In the meantime, you can reduce this problem by drawing attention to static factories in class or interface documentation and by adhering to **common naming conventions**. Here are some common names for static factory methods.
    - `from` -- A type-conversion method 
    - `of` -- An aggregation method
    - `valueOf` -- A more verbose alternative to `from` and `of`
    - `instance` or `getInstance` reutnrs an instance that is described by its parameters
    - `create` or `newInstance` each call should guarantee to return a **new** instance.
    - `get[Type]` like `getInstance`, but returns instance of a different class indicated by `Type` in the name. e.g. `getFileStore`.
    - `new[Type]` like `newInstance`, but returns a new instance of a different class. e.g. `newBufferedReader()`
    - `[type]`: a concise alternative to `get[Type]` and `new[Type]` e.g. `Collections.list()` 

## Summary
Static factory and constructors both have their uses, and it pays to understand their relative merits. **Often static factories are preferable, so avoid the reflex to provide public constructors without first considering static factories.**

## Related Java Knowledge
Java 8 requires all static members of an interface to be public. Java 9 allows private static methods, but static fields and static member classes are still required to be public.

## Related patterns & references
* Flyweight pattern
* *immutable classes[Item 17]*
* *singleton (Item 3)*
* *noninstantiable (Item 4)*
* *Enum types(item 34)*
* *noninstantiable companion class (Item 4)*
* *refering to returned object by interface rather than implementation class is good practice(Item 64)*
* The enumSet class (Item 36 )
* *use composition instead of inheritance (Item 18)*
* *immutable types (Item 17)*
