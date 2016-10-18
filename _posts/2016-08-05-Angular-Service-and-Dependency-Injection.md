Service is an important design choice in angular 2, the idea is to keep components lean. Here I will cover what I learned about using service and dependency injection. A nice and more detailed resource to look at: https://angular.io/docs/ts/latest/guide/architecture.html 

### Service
* Service is intended to provide service for component. To separate operational logic from component(so component can focus on controling the view)
* The code in `service.ts` file defines the **service class**, which acts as a prototype for service instances.
* The thing that is injected into components is **service instance**.

### Component
* responsible of defining and controling views, each view/tag can be considered as a **component instance**
* In component, the `constructor` determines/specifies which service will be used. 
* In the component constructor, we usually see *service instances*,*member variables*, ?(variable from other module? like child module?)

### Providers Array
* To use a service in a component, we need to register the service as a service provider, so the *injector* will know how to create instances. 
* Can register a service as a provider in mainly two ways:
    - register it in the provider array
    - register when bootstrap
* Provide different granuality/coverage

### Injector
* Injector is used to 
    - create/maintain service instances.
    - According to the providers
    - before the constructor of a component can be called
* Additionally you need to import the service class in the component to use it.

### To use a service in a component:
* Import the service in the component
* Include it in the component's provider array, or bootstrap the service already
* Declare a instance of the service in the constructor of the component, so each component can have a service instance.

