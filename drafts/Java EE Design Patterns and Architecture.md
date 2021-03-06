Java EE: Design Patterns and Architecture Cource on LNKD learning

# 1. Design Patterns in Software Development
## Classic GOF software design patterns
* solutions to common problems
* about object creation and interactions for micro scale problems
* Enterprise patterns for macro scale problems

23 design patterns into  3 categories:
* creational: object creation, initialization, and class selection
    - Abstract Factory
    - Builder
    - Factory Method
    - Prototype
    - Singleton*
* structural: interactions between objects
    - Adapter
    - Bridge
    - Composite
    - Decorator*
    - Facade*
    - Flyweight
    - Proxy
* behavioral: relationships and combining
    - Command
    - Visitor
    - Interpreter
    - Observer*
    - Iterator
    - Strategy
    - Mediator
    - State
    - Memento
    - Chain of Responsibility
    - Template Method

provides a Common dictionary

## Enterprise Patterns
* to solve enterprise problems
* follows the flow of a message, from one system to another system via path, redirection and transformations
* classified by application layer
* e.g
    - MVC in presentation layer
    - session facade in business layer
    - data access object in persistence layer

Two seminal works
* Core J2EE patterns
    - e.g. in modern enterprise: session facade is implemented with a single annotation, MVC is partially baked into JSF API, leaving view and model for dev to implememt. 

* Patterns of Enterprise Application Structure/Achitecture 
Longevity of design pattern, relevant to remainder of your career. 



# 2. classic software design patterns in java EE
## classic soterware design patterns revisited
* Some of the GOF patterns are built in OOB in java. e.g. observer pattern in Java SE. `java.util.Observable; java.util.Observer;`
* Some of the GOF patterns are used to build some of java's APIs: e.g. 
    - Singleton: `system.console()`, `Runtime.getRuntime()`
    - Strategy: `java.util.Comparator`
* Java EE built in support for GOF patterns
    - Enable patterns with annotations
    - relies on Java EE's super set of features: CDI(Contexts and Dependency Injection), interceptors, and EJB(enterprise javabeans).
* Containers does the work for you, adding services and functionalitiy to pattern implementations. 
* e.g. simply use annotation and you get what you want. 
    - @Singleton
    - @Decorator

## The singleton design pattern
* single object in the jvm
* Global point of access, once created is not destroyed until the application is terminated.
* reason to use: Contruct heavy weight object
* Create once, always available. 

implementation of singleton is non-trivial in java SE
* double check locking
* private constructors
* nested synchronization
* still not thread safe

Java EE provides all essential features, all you need to do is annotation.:
* Shared instance in JVM, and multi-threads
* Convention over configuration -> Reduce the amount of boilerplate code requried to construct a singleton
* Container-managed concurrency -> no need for messy synchronization and ugly code construct. 

**First code exersize**:  The first coding exercise will be to create and use a lazily instantiated singleton bean. In fact, the one we saw in the previous slide. A lazily instantiated singleton bean is a bean that is created the first time that it is used. Let's go to the IDE.

what is a bean?
## Implement a Singleton pool manager

`PoolManger.java`
```
@Singleton //this now becomes a lazily instantiated Singleton Bean.
public class PoolManager {
    
    private Queue<Object> pooledObjects = new LinkedBlockingQueue<>(1_000);
    
    public PoolManager(){
        for(int i = 0; i < 1000; i++) {
            pooledObjects.offer(new Object());
        }
    }
    
    public void returnObject(Object object) {
        pooledObjects.offer(object);
    }
    
    public void borrowObject() {
        pooledObjects.poll();
    }
}
```
So, the way this works is that the creation of the Singleton Class is done by the constructor. And, the container knows to create only one instance because the class is annotated with the Singleton Stereotype Annotation. And, it is lazily instantiated because it is not created until the first client makes a request to use it. Now, thanks to convention of a configuration this object is read locked by default. Access to it is serialized, so you don't have to worry about threat safety, at all. This means if two threats attempt to access the instance, they will be forced into serialized access. Now, the next question is how do I use the Singleton Bean? 

`UsePoolManager.java`

```
public class UsePoolManager {

    @Inject //container automatically creates an instance of the Pool Manager class when it is first used. This happens when it is injected, and the method is called by the client class.
    private PoolManager poolManager;
    
    public void usePooledObject() {
        Object object = poolManager.borrowObject();
        poolManager.returnObject(object);
    }
}
```

What is a container?

## Advanced Singleton Pattern
This lesson includes a few advanced features of JavaEE @Singleton support
* `@Startup`: make the singleton initialzed at start-up, instead of created on first use(lazy initiation). 
    - This could be used when we want to do some heavy initialization, or to do some extra startup tasks.
    - more control over instantiation
    - Eagerly instantiated singleton
* `@PostConstruct` move expensive construction after initial construction. 
* `@DependOn("NameOfSomeOtherSingleton")` make a singleton depenent on other class, so it will instantiation will occur after the depended class.

## Singleton Pattern Concurrency

Two concurrency management of JavaEE:
* Container-managed concurrency: this is default
* Bean-managed concurrency: custom concurrency control

### Bean-managed concurrency:
We do this by adding the `@ConcurrencyManagement(ConcurrentManagementType.BEAN)` annotation to the singleton class, and specifying the type of concurrency management by passing it as meta data to the annotation: `BEAN` or `CONTAINER`.
* Add ConcurrentManagement annotation
* Add appropriate concurrency management code to the methods. The methods operate in a concurrent environment, and therefore their access must be controlled in order for it to be safe. 
    - Traditionally, we would use the synchronize keyword and such constructs to make this happen
    -  in Java EE, we have been provided with a lock annotation that does this job for us. This annotation takes a lock type of either write or read
    -  `@lock(LockType.WRITE)` or `@lock(LockType.READ)`
    -  READ lock will wait for WRITE lock to finish, this wait could be indefinite, so we need another annotation: `@AccessTimeout(value = 30, unit = TimeUnit.SECONDS)` 
    -  Worth noting that the access timeout can be set at either the class level or the method level. 

## The Facade design pattern

* The facade pattern provides a **unified interface** to a set of interfaces in a subsystem. While hiding the complexity of that subsystem, the full power of the subsystem is therefore available by a simple and easy to use facade. 
* This pattern is commonly implemented to provide simple and unified access to a **legacy back-end system**. 
* To offer **course-grained access** to a range of available services, 
* These services are combined to provide higher level service and to **reduce remote network calls**. One remote call is made to the facade which then makes several calls to the subsystem.


## Implement the Facade pattern
Exercise Files > 02_07_start

Because the banking system is a Java EE application, the subsystem services are a special type of bean called an Enterprise JavaBean. An EJB is a POJO that is annotated either @Stateless, @Stateful, or @Singleton.

* use `@EJB` to inject a service(the sub services from the example). 
```
    @EJB
    private CreditRatingService creditRatingService
    ...
```

## Advanced Facade services

* Java EE similar implementation of the Façade pattern in a simple Java SE application. 
* The Façade is annotated `@Stateless`. This innocuous appearing annotation is actually rather powerful because it identifies this class as an **enterprise JavaBean**. This is a special kind of Bean in the Java EE application. It is given a range of very useful services automatically. Just by virtue of the @Stateless annotation, or a stateful annotation if you want your Bean to maintain a state.
* five services added by default for EJB
* another seven services that can be added by the use of annotations.

### An overview of the services
Default services: 
* **pooling** 
    * The containment creates a pool of EJB instances, that are shared among all clients. Upon a client request, an instance is retrieved from the pool and made available to the client via proxy. When the client has finished with the object, it is returned to the pool and readied for reuse.
    * The object is only created once when the pool is initialized, and only marked for garbage collection when the pool is destroyed. These events happen automatically on application startup and shutdown. 
    * The size of the pool is configured to allow fine-grain control over throttling. 
    * When the pool is exhausted and all objects are in use, further requests are queued until instances become available. Thus ensuring that the system remains stable even when a flood of requests come in. 
* **Thread Safety** All EJB components are thread safe by default. 
    - developer can focus on business logic rather than getting tangled with threading issues. 
    - Thread safety is achieved thanks to the way EJB pools provide access to its EJB instances. Each client gets exclusive access to once instance of the EJB hit requested. While the instance is serving the client, no other thread can access it. Therefore providing guaranteed thread safety. 
* **transactional** All of your EJB components are transactional by default.Which means that all interactions with a database and the Java messaging service are provided within a transaction.
    - This convenience means that you don't have to write plumbing code to manage transactional logic of your EJBs. 
    - Nevertheless, configuration and fine-tuning of transactional behavior is provided by specialized annotations. 
* **Memory management** 
    * The container manages it's memory by selecting stateful components to save to hard disk. 
    * Less frequently used components are temporarily taken out of action and only brought back to life when memory is freed, or when the request is made for that component. This cycle is called passivation and activation, and frees up memory for more actively used components.
* **State Management** The EJB container takes care of your stateful component's state, 
    * so you are free from writing tricky and repetitive state management code.
    * All of the intricacies of session and state maintenance are managed transparently. 
 
optional services, which you add to the EJB with annotations are. 
* **security** Probably one of the most important services provided by the container is that of security. This service is provided through the simple configuration of a few specially designed annotations and some exema attributes.
* **Interceptors** Aspect orientated programming is used to implement cross cutting concerns, such as logging and is brought to EJBs via interceptors. 
* **Scheduling** The scheduling service lets you evoke EJB methods based on a clone like expression. They can be used anytime a regular and repeatable action is required. 
* **Remoting** The container makes it easy to provide remote access to your EJB's functionality and to interact with the remote service. No additional code is required other than a few annotations to turn your local EJB into remote EJB.
A great benefit of this service is to allow remote EJBs to be managed as if they were local EJBs and therefore to be injected as CDI Beans. 
* **Asynchronous processing** By default, all EJBs methods are evoked synchronously. However, you can configure an EJB to have asynchronous methods, and for it's methods to be evoked asynchronously. 
* **Messaging** An EJB can adopt messaging capabilities and participate in the message dialogue without having to handle the complexities of messaging mechanics. The Java messaging service provides the functionality of the service and is configurable via a collection of special annotations. 
* **Web service** And finally, but most definitely not least, is the transformative power to make an EJB into a web service. Such as making it into a safe or restful endpoint. The container provides dedicated annotations that take care of all the aspects of a web service configuration. 


* just by using one annotation, either stateless or stateful, you can get a range of services for free.
* by adding various other annotations, you can extend those services even further.


Q What are services in Java EE?

## The Observer design pattern
An Overview:
* Observer pattern is widely used in many developers' apis
* Java EE provides both Asynchronous and Synchorous observer
* **Inform of state change**: The idea behind the observer pattern is that an object that changes its state can inform other objects that a change in state has occurred. 

### Key components:
* Subject: the object that changes its state
* Observers: objects that receives notification of the change of state. 
* 1 to many: subject may have many observers
* Pass message in a decoupled way: subject knows nothing about the observers. In java EE **subject and observers are truely decoupled**. 

Java SE has a built in Observer pattern in the java.util package. Extend `java.util.Observer` and `java.util.Observable` will do the work. open .

### Java EE implementation
* annotation driven: use `@Observes` to mark observers.`javax.enterprise.event.Observes`
* The subject uses the event class to create and fire events that the observers listen for. `javax.enterprise.event.Event`

Basically the subject sends an object to all observers, by firing event.

Simple example:
```
    public void createCustomer(@Observes Customer customer) {
        // add new customer
    }
```
```
    @Inject
    private Event<Customer> customerAddEvent;

    public void newCustomer(Customer customer) {
        customerAddEvent.fire(customer);
    }
```
##Implement Observer Pattern: Exercise **02_10**
Requirements:
* a REST endpoint that is called to create a new customer.
* fires a new customer event
* three observers are listening to the new customer event
    - The CustomerService, that creates a new customer, 
    - the AuthenticationService, that creates the authentication credentials for the new customer, 
    - and the EmailService that sends a welcome email.

> about rest, refer to course *RESTful Service with JAX-RS 2.0.*

The essence of the observer pattern, to decouple the change in the object state from those that react to its change.

## Observer priority and qualifiers
### Priority
* observer exception breaks chain: if an observer throws an exception the uncalled observers are not invoked
* Alleviated with `@Priority` setting: use this to specify order of observers to be invoked. **New in java8**
* The lowest value priorities are called first
* if no priority is specified, then the default middle value is assumed: the application constant from the priority class `javax.interceptor.Interceptor.Priority.APPLICATION` +500
* observers with the same priority are invoked in an **unpredictable order**.

**02_11** Code changes: +priority
e.g.`(@Observes @Priority(1000) Customer customer)`

### Qualifiers
A qualifier allows the container to disambiguate between instances injected into the class, and thus with the use of qualifiers, I could inject two different event instances of type customer.

Create a custom qualifier annotation using annotations. See details in exercise files. 

A qualifier is basically a distinguisher for events. Subject and Observers use the same qualifier annotation to specify who listens to whom. 


## Asynchronous observer
Exercise **02_12**
* By default events are synchronous. However, in CDI 2.0 they introduced asynchronous processing of events
* New method: `fireAsync` and annotation `@ObservesAsync`
* The events are observed asynchronously and in separate threads so **no priority can logically be set**. **no `@Priority` for Async**
* Asynchronous and synchronous observers operate independently from each other. So an asynchronous firing of an event cannot be observed by a parameter annotated observers and vice versa. 
* Notification options can be set on the asynchronous firing event. There's allowed a specification of a thread pool for that observer. 
* The fireAsync method returns an instance of `CompletionStage`. So if an exception is thrown by one of the observers, the `CompletionStage` will complete with completion exceptions. This instance holds a reference to all the suppressed exceptions throw during observer invocation and can be handled in the same way that you would handle a completion state instance

CompletionStage is a Java EE exception, google for more info.


## The decorator design Pattern
### the concepts overview
* Structrual Patterns
* It's purpose is to wrap a target object, theoretically unlimited layers of wrapping. 
* To dynamically add behavior at runtime, or when it is not possible, or advisable, to use sub classing
* e.g. data streams like java.io.BufferedInputStream
* runtime behavior is more flexible than inheritance, but adds complexity of sub classing, making it hard to determine type and behaviors prior to execution.
* In JavaEE, `@Decorator` `@Delegate`
    - The @Decorator annotation marks a decorator class
    - @Delegate annotation marks delegate injection point where the class to be decorated is injected.

### Simple scienario
Logger scienario, the logger is a third party API. To change the format, we need a decorator wrapping over the logger.

The third party LogMessage interface looks like this:
```
public interface LogMessage {
    void printMessage();
    String getMessage();
    void setMessage(String message);
}
```

The decorator is created by implementing the same `LogMessage` interface, and add the decorator annotation `@Decorator`. Example: `02_14_start`

```
@Decorator // identify as an decorator
@Priority(10) //The order of decorators to be applied. 
public abstract class LogMessageFormatter implements LogMessage { 
//if I want to decorate the logMessage, I need to implement the interface
//abstract so that I don't have to implement all the interface methods.

    @ //Any because I want to inject every instance of the logMessage.
    @Inject //add that injection point, with the type I want to inject
    @Delegate //in order to identify this as the delegate.
    private LogMessage logMessage;

    @Override
    public void printMessage() {
        //To use the API
        String message = logMessage.getMessage();
        message = LocalDate.now().toString().concat(message);
        logMessage.setMessage(message);
    }

}
```

This is a simple example, and things far more complex could be achieved. e.g. in `LogMessageJSONFormatter.java
```
@Decorator
@Priority(20)
public abstract class LogMessageJSONFormatter implements LogMessage {

    @Any
    @Inject
    @Delegate
    @ComplexMessage //annotate the logMessage injection point in the decorator so that only instances of logMessage annotated ComplexMessage are actually injected
    private LogMessage logMessage;

    @Override
    public void printMessage() {
        String message = logMessage.getMessage();
        String jsonMessage = JsonbBuilder.create().toJson(message);
        logMessage.setMessage(jsonMessage);
    }

}
```
To filter which message should be decorated, we can create a qualifier as in ComplexMessage.java:
1. create qualifier annotation
```
@Qualifier
@Retention(RetentionPolicy.RUNTIME)
@Target({ElementType.TYPE, ElementType.PARAMETER, ElementType.FIELD})
public @interface ComplexMessage {}
```
2. use the qualifier on a system message concrete class:
```
@ComplexMessage //To identify this is the message to be formatted.
public class SystemMessage implements LogMessage {

    private String message;

    @Override
    public String getMessage() {
        return message;
    }

    @Override
    public void setMessage(String message) {
        this.message = message;
    }

    @Override
    public void printMessage() {
        System.out.print(message);
    }
}
```
3. annotate the logMessage injection point in the decorator so that only instances of logMessage annotated ComplexMessage are actually injected

And now only those instances of logMessage annotated with ComplexMessage are decorated and all other instances remain in their original form.

# 3. Architectural Software Patterns in Java EE
## What are enterprise software patterns
* Enterprise software patterns are solution to problems commonly found in Enterprise systems. 
* unique problems for enterprise software -> their own set of solutions
* Example: MVC
    - not exclusively enterprise , certainly solves the common Enterprise problems of **separating the presentation logic from the business logic**
    - Web apps
    - views separated from model ensures the **visual display** and the **processing** of the app's data separate.
* Other patterns in the Enterprise Software world:
    - software pattern
    - integration pattern:  Enterprise systems integration problems. These patterns tend to be **structural** in nature, and solve problems such as file transfer, shared databases, remote procedure calls, and messaging.
    - architecture patterns: the structure of the Enterprise application. They're concerned with the **organization and separation** of concerns
        + might put the database at the center of the application. The classic three-tiered architecture does this,
        + might describe the database as an implementation detail and relegate it to the outer parts of the application design or putting the domain model at the heart of the application. Domain-centric architecture does this.

## The Dependency Injection Pattern
* Well-known but not GOF, to promote loose coupling
* The dependency injection pattern is based on the idea of inverting control. Instead of creating hard dependencies and creating new objects, either with a new keyword or look-ups, you inject the needed resources into the destination object.
* The client does not need to be aware of the different implementations of the injected resources, 
    - making **design changes** much easier
    - **unit testing** using mock objects is much easier to implement
    - **configuration can externalized**, thereby reducing the impact of changes
    - and finally, a loosely coupled architecture allows **pluckable structures**.
* The basic idea: *change the place where objects are created and use an injector to inject the specific implementation into the destination object at the right moment.*
* More than object creation(factory pattern)
* Objects are instantiated by the container and injected into qualifying injection points.
* Injection points are identified by the annotation `@inject` -> field, constructor, or a method. 
* Objects are instantiated based on their conformity to the specifications of a managed bean 
    - [as described in the specification documentation "Contexts and Dependency Injection for Java 2.0" JSR 365]
    - the injectable object(also called: managed CDI bean) must conform to the requirements in section 3.1: For an object to be discovered and instantiated as a managed CDI bean, it must meet all of these conditions
        + It is not an inner class
        + it is not a non-abstract class or an annotated `@Decorator`
        + it does not implement a service provider interface(SPI extension)
        + it is not annotated `@Vetoed` or in a package annotated `@Vetoed`
        + it has an appropriate constructor, 
            * which can be either a constructor with no parameters 
            * or it declares a constructor annotated inject.
    - Compliant POJOs are instantiated as managed CDI beans -> no special decoration or configuration is required.
* The container matches the type at the injection point with the object type, and injects an instance of the object if there is a match at the injeciton point. `03_02_start`: injecting an instance of the subject class into the target class. 
    - instance can be injected based on a class/interface type match
    - Using interface might give rise to Ambiguous dependency, due to posibility of multiple implementation classes. `@Qualifiers`
* **Qualifiers** are custom annotations that can be used to identify the implementation you want to be injected. example at `03_02_start`
```
//Favorites.java
@Qualifier
@Retention(RetentionPolicy.RUNTIME)
@Target({ElementType.TYPE, ElementType.PARAMETER, ElementType.FIELD, ElementType.CONSTRUCTOR})
public @interface Favourites {}

```

```
//Target.java
public class Target {

    @Inject
    @Favourites
    Subject subject;

}
```

## The filter design pattern

## AOP: The interceptor pattern

## AOP: Implement the interceptor pattern

## The MVC and Front Controller pattern

# 4. Introduction to Enterprise Architecture

## What is software arch

## why do we need arch

# 5. Database Centric Architecture

## What is 

## Classic Three Tier arch

## advantages and disadvantages

# 6. Domain-Centric Architecture

## What is domain-centric architecture?

## Modern four-layer architecture

## Types of domain architecture

## Advantages and disadvantages

# 7. Screaming Architecture

## What is screaming architecture?

## Functional vs. categorical

## Advantages and disadvantages

# 8. CQRS Architectures

## What is CQRS architecture?

## The three variants

## Advantages and disadvantages

# 9. Monolith and Microservice Architectures

## What is a monolith?

## What is a microservice?

## Advantages and disadvantages of microservices

# Conclusion

## Next steps









