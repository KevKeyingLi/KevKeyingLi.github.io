This is reading note for https://docs.oracle.com/javase/tutorial/java/javaOO/nested.html and related articles. A lot of the content is copied from the java tutorial site, with some deletion and some annotation. 

# When to Use Nested Classes, Local Classes, Anonymous Classes, and Lambda Expressions
https://docs.oracle.com/javase/tutorial/java/javaOO/whentouse.html

As mentioned in the section Nested Classes, nested classes enable you to logically group classes that are only used in one place, increase the use of encapsulation, and create more readable and maintainable code. Local classes, anonymous classes, and lambda expressions also impart these advantages; however, they are intended to be used for more specific situations:
* Local class: Use it if you need to create more than one instance of a class, access its constructor, or introduce a new, named type (because, for example, you need to invoke additional methods later).
* Anonymous class: Use it if you need to declare fields or additional methods.
* Lambda expression:
    - Use it if you are encapsulating a single unit of behavior that you want to pass to other code. For example, you would use a lambda expression if you want a certain action performed on each element of a collection, when a process is completed, or when a process encounters an error.
    - Use it if you need a simple instance of a functional interface and none of the preceding criteria apply (for example, you do not need a constructor, a named type, fields, or additional methods).
* Nested class: Use it if your requirements are similar to those of a local class, you want to make the type more widely available, and you don't require access to local variables or method parameters.
    - Use a non-static nested class (or inner class) if you require access to an enclosing instance's non-public fields and methods. Use a static nested class if you don't require this access.

## Nested Classes
```
class OuterClass {
    ...
    class NestedClass {
        ...
    }
}
```

Terminology: Nested classes are divided into two categories: static and non-static.
* Nested classes that are declared static are called static nested classes.
* Non-static nested classes are called inner classes.

A nested class is a member of its enclosing class.
* Non-static nested classes (inner classes) have access to other members of the enclosing class, even if they are declared private.
* Static nested classes do not have access to other members of the enclosing class. 

As a member of the OuterClass, a nested class can be declared private, public, protected, or package private. (Recall that outer classes can only be declared public or package private.)

My note: Always remember the basic difference of static vs non-static.

### Why Use Nested Classes?
Compelling reasons for using nested classes include the following:
* **It is a way of logically grouping classes that are only used in one place**: If a class is useful to only one other class, then it is logical to embed it in that class and keep the two together. Nesting such "helper classes" makes their package more streamlined.
* **It increases encapsulation**: Consider two top-level classes, A and B, where B needs access to members of A that would otherwise be declared private. By hiding class B within class A, A's members can be declared private and B can access them. In addition, B itself can be hidden from the outside world.
* **It can lead to more readable and maintainable code**: Nesting small classes within top-level classes places the code closer to where it is used.

### Static Nested Classes
Static and Nested:
* As with **class** methods and variables, a static nested class is associated with its outer class.
* And like static class methods, a static nested class cannot refer directly to instance variables or methods defined in its enclosing class: **it can use them only through an object reference**.

Special note: A static nested class interacts with the instance members of its outer class (and other classes) just like any other top-level class. **In effect, a static nested class is behaviorally a top-level class that has been nested in another top-level class for packaging convenience.**

Static nested classes are accessed using the enclosing class name: `OuterClass.StaticNestedClass`. **No need to instantiate outer class**.

An example, to create an object for the static nested class, use this syntax:
```
OuterClass.StaticNestedClass nestedObject =
     new OuterClass.StaticNestedClass();
```

Thinks of `System.out.println()`, `out` is a static nested class of `System`, and `println()` is a static method of that nested class.

### Inner Classes
As with **instance** methods and variables, an inner class is associated with an instance of its enclosing class and has direct access to that object's methods and fields. Also, because an inner class is associated with an instance, **it cannot define any static members itself**.

Objects that are instances of an inner class exist within an instance of the outer class. Consider the following classes:
```
class OuterClass {
    ...
    class InnerClass {
        ...
    }
}
```
An instance of `InnerClass` can exist only within an instance of `OuterClass` and has direct access to the methods and fields of its enclosing instance.

To instantiate an inner class, you must first instantiate the outer class. Then, **create the inner object within the outer object with this syntax**:
```
OuterClass.InnerClass innerObject = outerObject.new InnerClass();
```

There are two special kinds of inner classes: *local classes* and *anonymous classes*.

### Shadowing
If a declaration of a type (such as a member variable or a parameter name) in a particular scope (such as an inner class or a method definition) has the same name as another declaration in the enclosing scope, then the declaration shadows the declaration of the enclosing scope. You cannot refer to a shadowed declaration by its name alone. 

Refer to member variables that enclose larger scopes by the class name to which they belong.

For example, OuterClass, InnerClass both have member `x`, and InnerClass's method has local variable `x`. In the InnerClass's method:
* `x` will refer to the local variable.
* `this.x` will refer to the innerClass's member `x`
* `OuterClass.this.x` will refer to the OuterClass's member `x`

### Serialization
Serialization of inner classes, including local and anonymous classes, is strongly discouraged. https://docs.oracle.com/javase/tutorial/java/javaOO/nested.html


## Local Class
https://docs.oracle.com/javase/tutorial/java/javaOO/localclasses.html
Local classes are classes that are defined in a block. You can define a local class inside any block, e.g. a method body, a for loop, or an if clause. You typically find local classes defined in the body of a method. 

### Access
* A local class has access to the members of its enclosing class.
* In addition, a local class has access to local variables. However, a local class can only access local variables that are declared final. When a local class accesses a local variable or parameter of the enclosing block, it captures that variable or parameter.
* Starting in Java SE 8, a local class can access local variables and parameters of the enclosing block that are final or effectively final. A variable or parameter whose value is never changed after it is initialized is effectively final. 
* **Shadowing and Local Classes**: Declarations of a type (such as a variable) in a local class shadow declarations in the enclosing scope that have the same name. See Shadowing for more information.
Nested class, private class

### Local Classes Are Similar To Inner Classes
Local classes are similar to inner classes because they cannot define or declare any static members. Local classes in static methods, can only refer to static members of the enclosing class. 

Local classes are non-static because they have access to instance members of the enclosing block. Consequently, they cannot contain most kinds of static declarations.

* You cannot declare an interface inside a block; interfaces are inherently static.
* You cannot declare static initializers or member interfaces in a local class. 
* A local class can have *static members provided that they are constant variables*. (A constant variable is a variable of primitive type or type String that is declared final and initialized with a compile-time constant expression. A compile-time constant expression is typically a string or an arithmetic expression that can be evaluated at compile time. See Understanding Class Members for more information.)


## Anonymous classes
https://docs.oracle.com/javase/tutorial/java/javaOO/anonymousclasses.html
Anonymous classes enable you to make your code more concise. They enable you to declare and instantiate a class at the same time. They are like local classes except that they do not have a name. Use them if you need to use a local class only once.

While local classes are class declarations, anonymous classes are expressions, which means that you define the class in another expression. 

### Example
```
HelloWorld frenchGreeting = new HelloWorld() {
    String name = "tout le monde";
    public void greet() {
        greetSomeone("tout le monde");
    }
    public void greetSomeone(String someone) {
        name = someone;
        System.out.println("Salut " + name);
    }
};
```


### Syntax
The anonymous class expression consists of the following:
* The new operator
* The name of an interface to implement or a class to extend. In this example, the anonymous class is implementing the interface HelloWorld.
* Parentheses that contain the arguments to a constructor, just like a normal class instance creation expression. Note: When you implement an interface, there is no constructor, so you use an empty pair of parentheses, as in this example.
* A body, which is a class declaration body. More specifically, in the body, method declarations are allowed but statements are not.

Because an anonymous class definition is an expression, it must be part of a statement. 

### More on variable access
[Accessing Local Variables of the Enclosing Scope, and Declaring and Accessing Members of the Anonymous Class](https://docs.oracle.com/javase/tutorial/java/javaOO/anonymousclasses.html)


## Lambda Expressions
https://docs.oracle.com/javase/tutorial/java/javaOO/lambdaexpressions.html


## Static inner class?
This is not a commonly used thing, but for completeness referencing it from StackOverflow answer https://stackoverflow.com/a/70358/5335533