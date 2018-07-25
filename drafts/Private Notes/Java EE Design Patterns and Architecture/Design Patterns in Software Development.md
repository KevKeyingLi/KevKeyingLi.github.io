# Design Patterns in Software Development
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



# 2. classic soterware design patterns in java EE
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


