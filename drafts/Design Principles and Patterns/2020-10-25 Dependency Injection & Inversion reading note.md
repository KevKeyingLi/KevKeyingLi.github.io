[Dependency Injection & Inversion](https://khalilstemmler.com/articles/tutorials/dependency-injection-inversion-explained/)

Benefit of modular design:
* assign tasks to others
* reduce anxiety 
* improve modularity of designs

After modularity, how to hook things up, how to manage dependency? 
> good software design is all about composition of components

## Bad: directly referencing other components as dependency
* closely dependent/coupled
* hard to isolate and test, when testing one thing, all it's dependency need to be available. 

## Dependency injection: good.
Instead of hard dependency, allow the dependency to be injected during runtime. For example, pass in as an param of constructor vs create one inside of current component.
```
  constructor () {
    this.userRepo = new UserRepo(); // Also bad, read on for why
  }
//vs
  constructor (userRepo: UserRepo) { // Better, inject via constructor
    this.userRepo = userRepo; 
  }
```


* still not good enough, the dependency on the other component detail is still there.
* can't mock and test in isolation

## Dependency Inversion: better
Instead of a concrete class, injecting a interface is enough, the caller only need to know the shape. 

```
  constructor (userRepo: IUserRepo) { // and here
    this.userRepo = userRepo;
  }
```

This way the dependency graph changed. Instead of A -> B, it became A -> Interface <- B. 
* The dependency is inverted, a architectural boundary is created. Now modularity really are isolated.
* Isolated testing with mocked data is easy now.

> Design principle: Program against interfaces, not implementations.

## In summary, here is what dependency inversion/decoupling did
* testability: complex components can be substituted with mock component
* Substitutability: If we **program against an interface**, we enable a plugin architecture adhering to the Liskov Substitution Principle, which makes it incredibly easy for us to swap out valid plugins, and program against code that doesn't yet exist. 
* Flexibility: Adhering to the Open Closed Principle, a system should be open for extension but closed for modification. If we want to extend the system, we need only create a new plugin to extend the current behavior.
* Delegation: Inversion of Control is the phenomenon we observe when we delegate behavior to be implemented by someone else, but provide the **hooks/plugins/callbacks** to do so. We design the current component to invert control to another one. Lots of web frameworks are built on this principle.(React lifecycle hooks)

## Ways to manage inversion of control
* Manually inject instances of dependency at runtime. not scalable
* A solid style guide
* IoC containers: They work by requiring you to:
    - Create a container (that will hold all of your app dependencies)
    - Make that dependency known to the container (specify that it is injectable)
    - Resolve the depdendencies that you need by asking the container to inject them

> IoC also gets explained by: "Hollywood Design Principle": Don't call us, we'll call you.



























