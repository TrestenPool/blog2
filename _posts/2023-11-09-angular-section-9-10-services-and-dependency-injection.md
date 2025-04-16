---
layout: post
title: Angular Section 9,10 Services and Dependency Injection
date: 2023-11-09 13:21 -0600
categories: [Angular, Udemy]
image: 
  path: /2023-11-09-angular-section-9-10-services-and-dependency-injection/profile.png
---


# Angular Services
  - services are a way to encapsulate and organize code that can be shared and reused throughout different parts of an application 
  - Services provide a way to centralize common functionality, data, or business logic and make it available to components and other parts of the application
  - Services are typically used for tasks such as fetching data from a server, performing authentication, logging, and managing state.

Key Characteristics

| Characteristsic         | Description                                                                                                                                                                            |
| :---------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Singleton               | Services are singleton objects                                                                                                                                                         |
| Dependency Injection    | Angular's dependency injection system is used to inject services into components, directives, and other services                                                                       |
| Reusability             | Services can be reused across different components and modules, providing a way to encapsulate functionality                                                                           |
| Separation of Concerns  | By moving certain functionalities into services, you can achieve a separation of concerns                                                                                              |
| Asynchronous Operations | Services are often used to handle asynchronous operations, such as making HTTP requests to a server.                                                                                   |
| State management        | Services can be used to manage the state of an application. For more complex state management, developers might use services in conjunction with state management libraries like NgRx. |
| Business logic          | Services can encapsulate business logic, allowing components to remain focused on the presentation layer while the service handles the underlying logic.                               |


# Creating our own service
  - Services are denoted with the Annotation **@Injectable()**

Steps
1. Create the instructor with `ng g s logging`

You will get the following scaffolded code
```typescript
import { Injectable } from '@angular/core';

@Injectable({
  providedIn: 'root'
})
export class LoggingService {

  // custom method we added
  logStatusChange(name: string, status: string) {
    console.log(`Account ===${name}=== changing status to ==> ${status}`);
  }

  constructor() { }
}
```

2. inject using DI into the target using constructor injection `constructor(private loggingService: LoggingService) {}`
3. Provide the service (tell angular how to provide the dependency)

```typescript
@Component({
  selector: 'app-new-account',
  // ...
  providers: [LoggingService]
})
```

# Dependency Injection
  - In dependency injection there is a **dependency provider** & **dependency consumer**
  - Angular facilitates the interaction between dependency consumers and dependency providers using an abstraction called Injector. When a dependency is requested, the injector checks its registry to see if there is an instance already available there. If not, a new instance is created and stored in the registry.
  - Angular creates an application-wide injector (also known as **"root" injector**) during the application bootstrap process

## Providing a Dependency
  - ![alt-text](/2023-11-09-angular-section-9-10-services-and-dependency-injection/injecting_services.png)
  - The first step is to add the @Injectable decorator to show that the class can be injected.

```typscript
@Injectable({
  providedIn: 'root'
})
export class LoggingService {
}
```

  - The next step is to make it available in the DI by providing it. A dependency can be provided in multiple places:
  - At the Component level, using the providers field of the @Component decorator. In this case the HeroService becomes available to all instances of this component and other components and directives used in the template. For example:


## Hierchical Injection
  - Angular uses hierarchys for dependency injection
  - that means if you inject a service into a component all of the components children will share the same object of that dependency

![alt-text](/2023-11-09-angular-section-9-10-services-and-dependency-injection/hierarchy_injector.png)
  
Hierarchy
  - **AppModule**
    - highest in the hierarchy
    - the singleton service is available to all **Application-wide**
  - **AppComponent**
    - same instance of service is available for **all components** (but **not for all services**)
  - **Any other component**
    - Same instance of service is available for the component and all its child components

{% include embed/youtube.html id='G8zXugcYd7o?t=540' %}
  - ![alt-text](/2023-11-09-angular-section-9-10-services-and-dependency-injection/hierarchy.png)

  Element Injector
  - ![alt-text](/2023-11-09-angular-section-9-10-services-and-dependency-injection/hierarchy2.png)

### levels
  - highest level is in the app.module.ts 

# Observables in angular
  - crucial part of the RxJS (Reactive Extensions for JavaScript) 
  - often used for working with **asynchronous data streams**
  - provide a way to **handle events**
  - such as HTTP requests, user input, or data from other sources.
  - **Subscribe and Unsubscribe**: You can subscribe to an observable to receive notifications when new values are emitted
    - When you're done with an observable, it's essential to **unsubscribe** to prevent **memory leaks**.

# Subscribing to EventEmitters
  - you can subscribe to events emitted by an event emitter by using .subscribe()
  - 

