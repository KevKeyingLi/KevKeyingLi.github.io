Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #506-506的标注 | 添加于 2018年9月22日星期六 下午3:01:40

Traditionally, programmers have used the telescoping constructor pattern,
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #538-538的标注 | 添加于 2018年9月22日星期六 下午3:00:17

the telescoping constructor pattern works, but it is hard to write client code when there are
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #538-539的标注 | 添加于 2018年9月22日星期六 下午3:00:30

the telescoping constructor pattern works, but it is hard to write client code when there are many parameters, and harder still to read it.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #541-542的标注 | 添加于 2018年9月22日星期六 下午3:01:27

A second alternative when you’re faced with many optional parameters in a constructor is the JavaBeans
==========

Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #562-563的标注 | 添加于 2018年9月22日星期六 下午3:02:56

Because construction is split across multiple calls, a JavaBean may be in an inconsistent state partway through its construction.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #565-566的标注 | 添加于 2018年9月22日星期六 下午3:03:34

A related disadvantage is that the JavaBeans pattern precludes the possibility of making a class immutable
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #602-604的标注 | 添加于 2018年9月22日星期六 下午3:07:49

The NutritionFacts class is immutable, and all parameter default values are in one place. The builder’s setter methods return the builder itself so that invocations can be chained, resulting in a fluent API.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #607-608的标注 | 添加于 2018年9月22日星期六 下午3:08:12

The Builder pattern simulates named optional parameters as found in Python and Scala.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #613-613的标注 | 添加于 2018年9月22日星期六 下午3:12:28

The Builder pattern is well suited to class hierarchies.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #629-629的标注 | 添加于 2018年9月22日星期六 下午3:15:03

recursive type parameter
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #630-631的标注 | 添加于 2018年9月22日星期六 下午3:15:36

This workaround for the fact that Java lacks a self type is known as the simulated self-type idiom.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #658-659的标注 | 添加于 2018年9月22日星期六 下午3:41:47

This technique, wherein a subclass method is declared to return a subtype of the return type declared in the super-class, is known as covariant return typing.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #659-660的标注 | 添加于 2018年9月22日星期六 下午3:41:57

It allows clients to use these builders without the need for casting.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #670-670的标注 | 添加于 2018年9月22日星期六 下午3:47:24

A builder can fill in some fields automatically upon object creation, such as a serial number that increases
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #670-670的标注 | 添加于 2018年9月22日星期六 下午3:47:42

A builder can fill in some fields automatically upon object creation, such as a serial number that increases
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #673-673的标注 | 添加于 2018年9月22日星期六 下午3:48:10

verbose
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #672-672的标注 | 添加于 2018年9月22日星期六 下午3:48:14

performance-critical
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #675-676的标注 | 添加于 2018年9月22日星期六 下午3:48:53

the obsolete constructors or static factories will stick out like a sore thumb. Therefore, it’s often better to start with a builder in the first place.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #677-677的标注 | 添加于 2018年9月22日星期六 下午3:49:07

the Builder pattern is a good choice when designing classes whose constructors or static factories
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #677-678的标注 | 添加于 2018年9月22日星期六 下午3:49:18

the Builder pattern is a good choice when designing classes whose constructors or static factories would have more than a handful of parameters,
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #678-679的标注 | 添加于 2018年9月22日星期六 下午3:50:07

Client code is much easier to read and write with builders than with telescoping constructors, and builders are much safer than JavaBeans.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #681-684的标注 | 添加于 2018年9月24日星期一 下午9:14:39

Singletons typically represent either a stateless object such as a function (Item 24) or a system component that is intrinsically unique. Making a class a singleton can make it difficult to test its clients because it’s impossible to substitute a mock implementation for a singleton unless it implements an interface that serves as its type.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #693-694的标注 | 添加于 2018年9月24日星期一 下午9:17:04

Nothing that a client does can change this, with one caveat: a privileged client can invoke the private constructor reflectively (Item 65) with the aid of the AccessibleObject.setAccessible method.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #681 的笔记 | 添加于 2018年9月24日星期一 下午9:17:39

Background
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #681-681的标注 | 添加于 2018年9月24日星期一 下午9:17:39

singleton
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #706-707的标注 | 添加于 2018年9月24日星期一 下午9:19:05

One advantage of the static factory approach is that it gives you the flexibility to change your mind about whether the class is a singleton without changing its API.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #708-709的标注 | 添加于 2018年9月24日星期一 下午9:19:13

separate instance for each thread that invokes it. A second advantage is that you can write a generic singleton
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #708-708的标注 | 添加于 2018年9月24日星期一 下午9:19:20

separate instance for each thread that invokes it. A second
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #708-709的标注 | 添加于 2018年9月24日星期一 下午9:19:32

A second advantage is that you can write a generic singleton factory if your application requires it (Item 30).
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #708-711的标注 | 添加于 2018年9月24日星期一 下午9:20:05

A second advantage is that you can write a generic singleton factory if your application requires it (Item 30). A final advantage of using a static factory is that a method reference can be used as a supplier, for example Elvis::instance is a Supplier<Elvis>. Unless one of these advantages is relevant, the public field approach is preferable.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #712-712的标注 | 添加于 2018年9月24日星期一 下午9:20:48

serializable
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #720-721的标注 | 添加于 2018年9月24日星期一 下午9:21:37

A third way to implement a singleton is to declare a single-element enum:
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #727-727的标注 | 添加于 2018年9月24日星期一 下午9:22:39

a single-element enum type is often the best way to implement a singleton.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #727-729的标注 | 添加于 2018年9月24日星期一 下午9:22:52

Note that you can’t use this approach if your singleton must extend a superclass other than Enum (though you can declare an enum to implement interfaces).
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #732-734的标注 | 添加于 2018年9月24日星期一 下午9:24:10

They can be used to group related methods on primitive values or arrays, in the manner of java.lang.Math or java.util.Arrays. They can also be used to group static methods, including factories (Item 1), for objects that implement some interface, in the manner of java.util.Collections. (As of Java 8, you can also put such methods in the interface, assuming it’s yours to modify.)
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #732-736的标注 | 添加于 2018年9月24日星期一 下午9:24:21

They can be used to group related methods on primitive values or arrays, in the manner of java.lang.Math or java.util.Arrays. They can also be used to group static methods, including factories (Item 1), for objects that implement some interface, in the manner of java.util.Collections. (As of Java 8, you can also put such methods in the interface, assuming it’s yours to modify.) Lastly, such classes can be used to group methods on a final class, since you can’t put them in a subclass. Such utility classes
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #732-735的标注 | 添加于 2018年9月24日星期一 下午9:24:30

They can be used to group related methods on primitive values or arrays, in the manner of java.lang.Math or java.util.Arrays. They can also be used to group static methods, including factories (Item 1), for objects that implement some interface, in the manner of java.util.Collections. (As of Java 8, you can also put such methods in the interface, assuming it’s yours to modify.) Lastly, such classes can be used to group methods on a final class, since you can’t put them in a subclass.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #741-742的标注 | 添加于 2018年9月24日星期一 下午9:26:23

A default constructor is generated only if a class contains no explicit constructors, so a class can be made noninstantiable by including a private constructor:
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #751-751的标注 | 添加于 2018年9月24日星期一 下午9:28:15

As a side effect, this idiom also prevents the class from being subclassed.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #776-777的标注 | 添加于 2018年9月24日星期一 下午9:32:46

A simple pattern that satisfies this requirement is to pass the resource into the constructor when creating a new instance.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #774-774的标注 | 添加于 2018年9月24日星期一 下午9:32:51

Static utility classes and singletons are inappropriate for classes whose behavior is parameterized by an underlying resource.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #787-788的标注 | 添加于 2018年9月24日星期一 下午9:34:56

While our spell checker example had only a single resource (the dictionary), dependency injection works with an arbitrary number of resources and arbitrary dependency graphs.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #787-790的标注 | 添加于 2018年9月24日星期一 下午9:35:18

While our spell checker example had only a single resource (the dictionary), dependency injection works with an arbitrary number of resources and arbitrary dependency graphs. It preserves immutability (Item 17), so multiple clients can share dependent objects (assuming the clients desire the same underlying resources). Dependency injection is equally applicable to constructors, static factories (Item 1), and builders (Item
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #787-790的标注 | 添加于 2018年9月24日星期一 下午9:35:44

While our spell checker example had only a single resource (the dictionary), dependency injection works with an arbitrary number of resources and arbitrary dependency graphs. It preserves immutability (Item 17), so multiple clients can share dependent objects (assuming the clients desire the same underlying resources). Dependency injection is equally applicable to constructors, static factories (Item 1), and builders (Item
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #791-792的标注 | 添加于 2018年9月24日星期一 下午9:35:50

A useful variant of the pattern is to pass a resource factory to the constructor. A factory is an object that can be called repeatedly to create instances of a type.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #793-795的标注 | 添加于 2018年9月24日星期一 下午9:37:50

Methods that take a Supplier<T> on input should typically constrain the factory’s type parameter using a bounded wildcard type (Item 31) to allow the client to pass in a factory that creates any subtype of a specified type.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #799-800的标注 | 添加于 2018年9月24日星期一 下午9:40:02

This clutter can be all but eliminated by using a dependency injection framework,
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #801-802的标注 | 添加于 2018年9月24日星期一 下午9:40:49

APIs designed for manual dependency injection are trivially adapted for use by these frameworks.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #803-805的标注 | 添加于 2018年9月24日星期一 下午9:41:09

Instead, pass the resources, or factories to create them, into the constructor (or static factory or builder). This practice, known as dependency injection, will greatly enhance the flexibility, reusability, and testability of a class.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #807-808的标注 | 添加于 2018年9月24日星期一 下午9:43:47

Reuse can be both faster and more stylish. An object can always be reused if it is immutable (Item 17).
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #816-817的标注 | 添加于 2018年9月24日星期一 下午11:28:17

This version uses a single String instance, rather than creating a new one each time it is executed. Furthermore, it is guaranteed that the object will be reused by any other code running in the same
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #818-819的标注 | 添加于 2018年9月24日星期一 下午11:28:54

You can often avoid creating unnecessary objects by using static factory methods (Item 1) in preference to constructors on immutable classes that provide both.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #820-821的标注 | 添加于 2018年9月24日星期一 下午11:29:31

The constructor must create a new object each time it’s called, while the factory method is never required to do so and won’t in practice.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #821-822的标注 | 添加于 2018年9月24日星期一 下午11:29:40

In addition to reusing immutable objects, you can also reuse mutable objects if you know they won’t be modified.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #823-824的标注 | 添加于 2018年9月24日星期一 下午11:30:26

“expensive object” repeatedly, it may be advisable to cache it for reuse.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #830-831的标注 | 添加于 2018年9月24日星期一 下午11:31:00

While String.matches is the easiest way to check if a string matches a regular expression, it’s not suitable for repeated use in performance-critical situations.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #834-835的标注 | 添加于 2018年9月24日星期一 下午11:31:33

To improve the performance, explicitly compile the regular expression into a Pattern instance (which is immutable) as part of class initialization, cache it, and reuse
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #835 的笔记 | 添加于 2018年9月24日星期一 下午11:31:49

Example
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #844-844的标注 | 添加于 2018年9月24日星期一 下午11:33:05

Not only is the performance improved, but arguably, so is clarity.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #847-849的标注 | 添加于 2018年9月24日星期一 下午11:33:35

It would be possible to eliminate the initialization by lazily initializing the field (Item 83) the first time the isRomanNumeral method is invoked, but this is not recommended.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #847-850的标注 | 添加于 2018年9月24日星期一 下午11:33:52

It would be possible to eliminate the initialization by lazily initializing the field (Item 83) the first time the isRomanNumeral method is invoked, but this is not recommended. As is often the case with lazy initialization, it would complicate the implementation with no measurable performance improvement (Item 67).
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #852-852的标注 | 添加于 2018年9月24日星期一 下午11:34:42

An adapter is an object that delegates to a backing object, providing an alternative interface.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #855-856的标注 | 添加于 2018年9月24日星期一 下午11:37:42

Naively, it would seem that every call to keySet would have to create a new Set instance, but every call to keySet on a given Map object may return the same Set instance.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #860-861的标注 | 添加于 2018年9月24日星期一 下午11:38:11

Autoboxing blurs but does not erase the distinction between primitive and boxed primitive types.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #873-873的标注 | 添加于 2018年9月24日星期一 下午11:39:24

The lesson is clear: prefer primitives to boxed primitives, and watch out for unintentional autoboxing.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #875-876的标注 | 添加于 2018年9月24日星期一 下午11:40:21

Creating additional objects to enhance the clarity, simplicity, or power of a program is generally a good thing.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #877-878的标注 | 添加于 2018年9月24日星期一 下午11:40:29

Conversely, avoiding object creation by maintaining your own object pool is a bad idea unless the objects in the pool are extremely heavyweight.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #879-880的标注 | 添加于 2018年9月24日星期一 下午11:41:14

Generally speaking, however, maintaining your own object pools clutters your code, increases memory footprint, and harms performance.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #883-885的标注 | 添加于 2018年9月24日星期一 下午11:42:23

Note that the penalty for reusing an object when defensive copying is called for is far greater than the penalty for needlessly creating a duplicate object. Failing to make defensive copies where required can lead to insidious bugs and security holes; creating objects unnecessarily merely affects style and performance.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #908-909的标注 | 添加于 2018年9月27日星期四 下午7:59:41

which can silently manifest itself as reduced performance due to increased garbage collector activity or increased memory footprint.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #910-912的标注 | 添加于 2018年9月27日星期四 下午8:00:35

If a stack grows and then shrinks, the objects that were popped off the stack will not be garbage collected, even if the program using the stack has no more references to them. This is because the stack maintains obsolete references to these objects.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #914-917的标注 | 添加于 2018年9月27日星期四 下午8:02:02

Memory leaks in garbage-collected languages (more properly known as unintentional object retentions) are insidious. If an object reference is unintentionally retained, not only is that object excluded from garbage collection, but so too are any objects referenced by that object, and so on. Even if only a few object references are unintentionally retained, many, many objects may be prevented from being garbage collected, with potentially large effects on performance.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #918-918的标注 | 添加于 2018年9月27日星期四 下午8:02:10

null out references once they become obsolete.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #926-927的标注 | 添加于 2018年9月27日星期四 下午8:20:31

It is always beneficial to detect programming errors as quickly as possible.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #928-931的标注 | 添加于 2018年9月27日星期四 下午8:21:10

Nulling out object references should be the exception rather than the norm. The best way to eliminate an obsolete reference is to let the variable that contained the reference fall out of scope. This occurs naturally if you define each variable in the narrowest possible scope (Item 57).
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #932-932的标注 | 添加于 2018年9月27日星期四 下午8:22:52

Simply put, it manages its own memory.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #933-935的标注 | 添加于 2018年9月27日星期四 下午8:23:02

The elements in the active portion of the array (as defined earlier) are allocated, and those in the remainder of the array are free. The garbage collector has no way of knowing this; to the garbage collector, all of the object references in the elements array are equally valid.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #937-938的标注 | 添加于 2018年9月27日星期四 下午8:23:41

whenever a class manages its own memory, the programmer should be alert for memory leaks. Whenever an element is freed, any object references contained in the element should be nulled out.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #939-940的标注 | 添加于 2018年9月27日星期四 下午8:24:20

Another common source of memory leaks is caches. Once you put an object reference into a cache, it’s easy to forget that it’s there and leave it in the cache long after it becomes irrelevant.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #942-943的标注 | 添加于 2018年9月27日星期四 下午8:24:58

Remember that WeakHashMap is useful only if the desired lifetime of cache entries is determined by external references to the key, not the value.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #944-946的标注 | 添加于 2018年9月27日星期四 下午8:26:11

Under these circumstances, the cache should occasionally be cleansed of entries that have fallen into disuse. This can be done by a background thread (perhaps a ScheduledThreadPoolExecutor) or as a side effect of adding new entries to the cache.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #948-949的标注 | 添加于 2018年9月27日星期四 下午8:26:40

third common source of memory leaks is listeners and other callbacks. If you implement an API where clients register callbacks but don’t deregister them explicitly, they will accumulate unless you take some action.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #949-950的标注 | 添加于 2018年9月27日星期四 下午8:26:47

One way to ensure that callbacks are garbage collected promptly is to store only weak references to them, for instance, by storing them only as keys in a WeakHashMap.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #951-952的标注 | 添加于 2018年9月27日星期四 下午8:27:03

They are typically discovered only as a result of careful code inspection or with the aid of a debugging tool known as a heap profiler.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #952-953的标注 | 添加于 2018年9月27日星期四 下午8:27:19

Therefore, it is very desirable to learn to anticipate problems like this before they occur and prevent them from happening.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #954-955的标注 | 添加于 2018年10月1日星期一 下午10:09:41

Finalizers are unpredictable, often dangerous, and generally unnecessary. Their use can cause erratic behavior, poor performance, and portability problems.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #957-958的标注 | 添加于 2018年10月1日星期一 下午10:10:03

Cleaners are less dangerous than finalizers, but still unpredictable, slow, and generally unnecessary.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #961-962的标注 | 添加于 2018年10月1日星期一 下午10:13:19

Java, a try-with-resources or try-finally block is used for this purpose (Item 9).
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #963-963的标注 | 添加于 2018年10月1日星期一 下午10:13:37

One shortcoming of finalizers and cleaners is that there is no guarantee they’ll be executed promptly [JLS, 12.6].
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #964-965的标注 | 添加于 2018年10月1日星期一 下午10:13:50

This means that you should never do anything time-critical in a finalizer or cleaner.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #971-971的标注 | 添加于 2018年10月1日星期一 下午10:15:58

Tardy finalization is not just a theoretical problem. Providing a finalizer for a class can arbitrarily delay reclamation of its instances.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #978-979的标注 | 添加于 2018年10月1日星期一 下午10:17:17

prompt cleaning. Not only does the specification provide no guarantee that finalizers or cleaners will run promptly; it provides no guarantee that they’ll run at all. It is entirely possible, even likely, that a program terminates
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #978-979的标注 | 添加于 2018年10月1日星期一 下午10:17:28

prompt cleaning. Not only does the specification provide no guarantee that finalizers or cleaners will run promptly; it provides no guarantee that they’ll run at all. It is entirely possible, even likely, that a program terminates
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #978-979的标注 | 添加于 2018年10月1日星期一 下午10:17:33

Not only does the specification provide no guarantee that finalizers or cleaners will run promptly; it provides no guarantee that they’ll run at all. It is entirely possible, even likely, that a program terminates
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #978-979的标注 | 添加于 2018年10月1日星期一 下午10:17:38

Not only does the specification provide no guarantee that finalizers or cleaners will run promptly; it provides no guarantee that they’ll run at all. It
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #978-979的标注 | 添加于 2018年10月1日星期一 下午10:17:41

Not only does the specification provide no guarantee that finalizers or cleaners will run promptly; it provides no guarantee that they’ll run at all.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #980-981的标注 | 添加于 2018年10月1日星期一 下午10:18:12

As a consequence, you should never depend on a finalizer or cleaner to update persistent state.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #976-977的标注 | 添加于 2018年10月1日星期一 下午10:18:21

Cleaners are a bit better than finalizers in this regard because class authors have control over their own cleaner threads, but
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #985-986的标注 | 添加于 2018年10月1日星期一 下午10:19:23

Another problem with finalizers is that an uncaught exception thrown during finalization is ignored, and finalization of that object terminates [JLS, 12.6].
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #990-990的标注 | 添加于 2018年10月1日星期一 下午10:20:14

There is a severe performance penalty for using finalizers and cleaners.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #993-993的标注 | 添加于 2018年10月1日星期一 下午10:21:12

finalizers inhibit efficient garbage collection.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #996-996的标注 | 添加于 2018年10月1日星期一 下午10:21:32

safety net
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #996-997的标注 | 添加于 2018年10月1日星期一 下午10:22:59

Finalizers have a serious security problem: they open your class up to finalizer attacks.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #1001-1002的标注 | 添加于 2018年10月1日星期一 下午10:23:21

Throwing an exception from a constructor should be sufficient to prevent an object from coming into existence;
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #1001-1002的标注 | 添加于 2018年10月1日星期一 下午10:23:28

Throwing an exception from a constructor should be sufficient to prevent an object from coming into existence;
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #1001-1002的标注 | 添加于 2018年10月1日星期一 下午10:23:33

Throwing an exception from a constructor should be sufficient to prevent an object from coming into existence; in the presence of finalizers, it is not.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #1003-1004的标注 | 添加于 2018年10月1日星期一 下午10:23:53

To protect nonfinal classes from finalizer attacks, write a final finalize method that does nothing.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #1006-1008的标注 | 添加于 2018年10月1日星期一 下午10:24:25

Just have your class implement AutoCloseable, and require its clients to invoke the close method on each instance when it is no longer needed, typically using try-with-resources to ensure termination even in the face of exceptions (Item
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #1011-1012的标注 | 添加于 2018年10月1日星期一 下午10:25:32

They have perhaps two legitimate uses. One is to act as a safety net in case the owner of a resource neglects to call its close method.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #1015-1016的标注 | 添加于 2018年10月1日星期一 下午10:26:01

A second legitimate use of cleaners concerns objects with native peers.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #1016-1016的标注 | 添加于 2018年10月1日星期一 下午10:26:58

A native peer is a native (non-Java) object to which a normal object delegates via native methods.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #1049-1050的标注 | 添加于 2018年10月1日星期一 下午10:32:07

It is critical that a State instance does not refer to its Room instance. If it did, it would create a circularity that would prevent the Room instance from becoming eligible for garbage collection (and from being automatically cleaned).
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #1050-1052的标注 | 添加于 2018年10月1日星期一 下午10:33:14

Therefore, State must be a static nested class because nonstatic nested classes contain references to their enclosing instances (Item 24). It is similarly inadvisable to use a lambda because they can easily capture references to enclosing objects.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #1053-1053的标注 | 添加于 2018年10月1日星期一 下午10:34:29

earlier, Room’s cleaner is used only as a safety net. If clients surround
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #1053-1054的标注 | 添加于 2018年10月1日星期一 下午10:34:34

If clients surround all Room instantiations in try-with-resource blocks, automatic cleaning will never be required. This well-behaved client demonstrates that behavior:
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #1070-1071的标注 | 添加于 2018年10月1日星期一 下午10:35:46

In summary, don’t use cleaners, or in releases prior to Java 9, finalizers, except as a safety net or to terminate noncritical native resources. Even then, beware the indeterminacy and performance consequences.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #1077-1078的标注 | 添加于 2018年10月1日星期一 下午10:37:02

try-finally statement was the best way to guarantee that a resource would be closed properly, even in the face of an exception or return:
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #1076-1078的标注 | 添加于 2018年10月1日星期一 下午10:37:23

8). Historically, a try-finally statement was the best way to guarantee that a resource would be closed properly, even in the face of an exception or return:
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #1077-1078的标注 | 添加于 2018年10月1日星期一 下午10:37:27

Historically, a try-finally statement was the best way to guarantee that a resource would be closed properly, even in the face of an exception or return:
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #1101-1101的标注 | 添加于 2018年10月1日星期一 下午10:40:19

Under these circumstances, the second exception completely obliterates the first one.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #1105-1106的标注 | 添加于 2018年10月1日星期一 下午10:41:05

To be usable with this construct, a resource must implement the AutoCloseable interface, which consists of a single void-returning close method.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #1107-1108的标注 | 添加于 2018年10月1日星期一 下午10:41:23

If you write a class that represents a resource that must be closed, your class should implement AutoCloseable too.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #1123-1125的标注 | 添加于 2018年10月1日星期一 下午10:46:56

If exceptions are thrown by both the readLine call and the (invisible) close, the latter exception is suppressed in favor of the former. In fact, multiple exceptions may be suppressed in order to preserve the exception that you actually want to see.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #1127-1128的标注 | 添加于 2018年10月1日星期一 下午10:47:32

You can put catch clauses on try-with-resources statements, just as you can on regular try-finally statements.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #1136-1139的标注 | 添加于 2018年10月1日星期一 下午10:48:31

The lesson is clear: Always use try-with-resources in preference to try-finally when working with resources that must be closed. The resulting code is shorter and clearer, and the exceptions that it generates are more useful. The try-with-resources statement makes it easy to write correct code using resources that must be closed, which was practically impossible using try-finally. Chapter 3.
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #1136-1138的标注 | 添加于 2018年10月1日星期一 下午10:48:39

The lesson is clear: Always use try-with-resources in preference to try-finally when working with resources that must be closed. The resulting code is shorter and clearer, and the exceptions that it generates are more useful. The try-with-resources statement makes it easy to write correct code using resources that must be closed, which
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #1136-1138的标注 | 添加于 2018年10月1日星期一 下午10:48:42

The lesson is clear: Always use try-with-resources in preference to try-finally when working with resources that must be closed. The resulting code is shorter and clearer, and the exceptions that it generates are more useful. The try-with-resources statement makes it easy to write correct code using resources that must be closed, which
==========
Effective Java, Third Edition (Joshua Bloch)
- 您在位置 #1136-1139的标注 | 添加于 2018年10月1日星期一 下午10:48:43

The lesson is clear: Always use try-with-resources in preference to try-finally when working with resources that must be closed. The resulting code is shorter and clearer, and the exceptions that it generates are more useful. The try-with-resources statement makes it easy to write correct code using resources that must be closed, which was practically impossible using try-finally.
==========
