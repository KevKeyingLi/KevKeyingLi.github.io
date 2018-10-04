
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #322-325的标注 | 添加于 2018年9月19日星期三 下午9:26:34

Clarity and simplicity are of paramount importance. The user of a component should never be surprised by its behavior. Components should be as small as possible but no smaller. (As used in this book, the term component refers to any reusable software element, from an individual method to a complex framework consisting of multiple packages.) Code should be reused rather than copied. The dependencies between components should be kept to a minimum. Errors should be detected as soon as possible after they are made, ideally at compile time.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #327-328的标注 | 添加于 2018年9月19日星期三 下午9:27:06

Learning the art of programming, like most other disciplines, consists of first learning the rules and then learning when to break them.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #362-366的标注 | 添加于 2018年9月19日星期三 下午9:29:31

The language supports four kinds of types: interfaces (including annotations), classes (including enums), arrays, and primitives. The first three are known as reference types. Class instances and arrays are objects; primitive values are not. A class’s members consist of its fields, methods, member classes, and member interfaces. A method’s signature consists of its name and the types of its formal parameters; the signature does not include the method’s return type.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #367-370的标注 | 添加于 2018年9月19日星期三 下午9:30:16

Unlike The Java Language Specification, this book uses inheritance as a synonym for subclassing. Instead of using the term inheritance for interfaces, this book simply states that a class implements an interface or that one interface extends another. To describe the access level that applies when none is specified, this book uses the traditional package-private instead of the technically correct package access
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #371-375的标注 | 添加于 2018年9月19日星期三 下午9:31:01

The term exported API, or simply API, refers to the classes, interfaces, constructors, members, and serialized forms by which a programmer accesses a class, interface, or package. (The term API, which is short for application programming interface, is used in preference to the otherwise preferable term interface to avoid confusion with the language construct of that name.) A programmer who writes a program that uses an API is referred to as a user of the API. A class whose implementation
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #371-375的标注 | 添加于 2018年9月19日星期三 下午9:31:06

The term exported API, or simply API, refers to the classes, interfaces, constructors, members, and serialized forms by which a programmer accesses a class, interface, or package. (The term API, which is short for application programming interface, is used in preference to the otherwise preferable term interface to avoid confusion with the language construct of that name.) A programmer who writes a program that uses an API is referred to as a user of the API. A class whose implementation
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #371-375的标注 | 添加于 2018年9月19日星期三 下午9:31:16

The term exported API, or simply API, refers to the classes, interfaces, constructors, members, and serialized forms by which a programmer accesses a class, interface, or package. (The term API, which is short for application programming interface, is used in preference to the otherwise preferable term interface to avoid confusion with the language construct of that name.) A programmer who writes a program that uses an API is referred to as a user of the API. A class whose implementation uses an API is a client of the API.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #371-375的标注 | 添加于 2018年9月19日星期三 下午9:31:22

The term exported API, or simply API, refers to the classes, interfaces, constructors, members, and serialized forms by which a programmer accesses a class, interface, or package. (The term API, which is short for application programming interface, is used in preference to the otherwise preferable term interface to avoid confusion with the language construct of that name.) A programmer who writes a program that uses an API is referred to as a user of the API. A class whose implementation uses an API is a client of the API.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #375-380的标注 | 添加于 2018年9月19日星期三 下午9:31:58

Classes, interfaces, constructors, members, and serialized forms are collectively known as API elements. An exported API consists of the API elements that are accessible outside of the package that defines the API. These are the API elements that any client can use and the author of the API commits to support. Not coincidentally, they are also the elements for which the Javadoc utility generates documentation in its default mode of operation. Loosely speaking, the exported API of a package consists of the public and protected members and constructors of every public class or interface in the package.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #375-380的标注 | 添加于 2018年9月19日星期三 下午9:32:18

Classes, interfaces, constructors, members, and serialized forms are collectively known as API elements. An exported API consists of the API elements that are accessible outside of the package that defines the API. These are the API elements that any client can use and the author of the API commits to support. Not coincidentally, they are also the elements for which the Javadoc utility generates documentation in its default mode of operation. Loosely speaking, the exported API of a package consists of the public and protected members and constructors of every public class or interface in the package.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #380-381的标注 | 添加于 2018年9月19日星期三 下午9:32:38

module system was added to the platform. If a library makes use of the module system, its exported API is the union of the exported APIs of all the packages exported by the library’s module declaration.
==========


# Note template
## What? The problem to solve
## How? The pattern
## Compare? Other solutions and patterns, 
## Benefits
## Shortcomings
## Where to use and where not, examples
## Related Java Knowledge
## Terminologies 
## Related patterns & references