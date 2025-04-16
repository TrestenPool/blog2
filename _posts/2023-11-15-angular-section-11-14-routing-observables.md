---
layout: post
title: Angular Section 11..14 Routing, Observables
date: 2023-11-15 10:41 -0600
categories: [Angular, Udemy]
image: 
  path: /2023-11-15-angular-section-11-14-routing-observables/profile.png
---

- [What is routing?](#what-is-routing)
- [Setting up Routes](#setting-up-routes)
  - [Why we can just use href="routename" for redirection](#why-we-can-just-use-hrefroutename-for-redirection)
  - [Using routerLinkActive](#using-routerlinkactive)
  - [Navigate programmatically](#navigate-programmatically)
  - [Path Parameters to route](#path-parameters-to-route)
  - [Angular not updating component when navigating to it twice](#angular-not-updating-component-when-navigating-to-it-twice)
  - [ActivatedRoute.snapshot or without??](#activatedroutesnapshot-or-without)
  - [Query parameters \& fragement](#query-parameters--fragement)
- [Nesting Routes](#nesting-routes)
- [Route Guards](#route-guards)
  - [canActivate example](#canactivate-example)
  - [canDeactivate example](#candeactivate-example)
- [Passing data to a route](#passing-data-to-a-route)
  - [Passing Static data to a route](#passing-static-data-to-a-route)
  - [Passing Dynamic data to route](#passing-dynamic-data-to-route)
- [Location Strategy](#location-strategy)
  - [Hash Stategy](#hash-stategy)
- [Observables](#observables)
  - [Installation](#installation)
  - [Observer data methods](#observer-data-methods)
  - [Creating our own observable](#creating-our-own-observable)
  - [Operators](#operators)
  - [Subjects](#subjects)


# What is routing?
  - In Angular, routing is used to navigate between different views or components in a single-page application (SPA). 

# Setting up Routes
  - **Configure the routes** in app.module.ts as an array of json objects representing the different routes for our app
  - import **RouterModule** in app.module.ts and pass our array to the **.forRoot()** method
  - place **router-outlet** html element in the app.component.html where we want the content to load for each of the routes

Configuring app routes
```typescript
const appRoutes: Routes = [
  // localhost/home
  {path: 'home', component: HomeComponent},
  // localhost/users
  {path: 'users', component: UsersComponent},
  // localhost/servers
  {path: 'servers', component: ServersComponent},
  // wildcard route
  { path: '**', redirectTo: '/home', pathMatch: 'full' },
];
```
{: file='app.module.ts'}

Importing RouterModule
```typescript
  imports: [
    BrowserModule,
    FormsModule,
    RouterModule.forRoot(appRoutes) // make sure to import and place the array variable within the ()
  ],
```
{: file='app.module.ts'}


Placing the router-outlet html element
```html
  <div class="row">
    <div class="col-xs-12 col-sm-10 col-md-8 col-sm-offset-1 col-md-offset-2">
      <router-outlet></router-outlet>
    </div>
  </div>
```
{: file='app.component.html'}

## Why we can just use href="routename" for redirection
  - when we use href for an anchor tag, the browser will redirect you to that page instead of dynamically loading that spa

## Using routerLinkActive
  - use routerLinkActive when you want to apply some classes to a certain element only if it is on the route specified
  - you can specify any class you want

Below example
  - we are specifying 3 routes [home, servers, users]
  - we want to apply the active class when it is on the respective route
  - example if we are on the /servers route
    - it will get dyanmically class="active"

```html
<ul class="nav nav-tabs">
  <li role="presentation" routerLinkActive="active" routerLink="home"><a>Home</a></li>
  <li role="presentation" routerLinkActive="active" routerLink="servers"><a>Servers</a></li>
  <li role="presentation" routerLinkActive="active" routerLink="users"><a>Users</a></li>
</ul>
```

## Navigate programmatically
  - steps
    - inject Router into your code
    - use .navigate() to navigate to the url

Inject the Router into your code by constructor injection
```typescript
constructor(private router: Router) { 

}
```

Navigate to different url
```typescript
  onLoadServers(){
    // complex calculation ...

    // navigate to /servers
    this.router.navigate(['/servers'])
  }
```

## Path Parameters to route
  - Steps
    - Setup in the route configuration
    - Inject **ActivatedRoute** into the constructor of the component
    - **ActivatedRoute.snapshop.params['paramName']** to access the parameter name you are looking for
  
Setup in route configuration with :id
```typescript
const appRoutes: Routes = [
  // .. other routes
  // ..
  {path: 'users/:id', component: UserComponent}
]
```
{: file='app.module.ts'}

Inject ActivatedRoute and access the path parameter
```typescript
export class UserComponent implements OnInit {
  // our user 
  user: {id: number};

  // injecting the ActivatedRoute
  constructor(
    private route: ActivatedRoute
  ){}

  // NgOnInit
  ngOnInit() {
    // accessing the path parameters
    this.user = {
      id: this.route.snapshot.params['id']
    }
    console.log(this.user);
  }

}
```
{: file='user.component.ts'}

## Angular not updating component when navigating to it twice
  - in the previous example we created a route that looked like localhost/users/id
  - if we were to have a button on the user html file that navigated to localhost/users/differentID
  - if would navigate to that route but not update the content of that component
    - why is this??
    - this is because angular is smart enough to know that we are already on the component so no need to refresh if we are just going back to it even though it won't update any of the data on it

## ActivatedRoute.snapshot or without??
  - what is the difference between `this.route.snapshot.params['id']` and this `this.route.params.subscribe(()=> {})`
  - without snapshot is just an **observable**
    - meaning we can subscribe so that way when a change is detected we can run some code to update our user

Now once a change is detected to the route parameters the code in the subscribe code block will be executed
```typescript
ngOnInit() {
  // initial set
  this.user = {
    id: this.route.snapshot.params['id']
  }

  // subscribing
  this.route.params
    .subscribe(
      (params: Params) => {
        this.user.id = params['id']
      }
    )
}
```

## Query parameters & fragement
  - Setting in HTML template code
    - `[queryParams]="{paramName: '1'}"`
      - setting query parameters in html template
    - `fragment="fragmentName"`
      - setting the fragment name
  
  - Settting up in Typescript component code
    - `this.router.navigate(['/servers', id, 'edit'], {queryParams: {allowEdit: '1'}, fragment: 'loading' })`
      - this will route to /servers/id/edit with query parameter and fragement in url
    
  - Retrieving Query parameters
    - ``

Using Query parameters in the html temlpate code
```html
  <!-- list of servers -->
  <div class="col-xs-12 col-sm-4">
    <div class="list-group">
      <a
        [routerLink]="[server.id, 'edit']"
        [queryParams]="{allowEdit: '1'}"
        fragment="something"
        class="list-group-item"
        *ngFor="let server of servers">
        {{ server.name }}
      </a>
    </div>
  </div>
```

Using Typescript code to go to route with path parameters, query parameters and fragment
```typescript
let id = 10;
this.router.navigate(['/servers', id, 'edit'], {queryParams: {allowEdit: '1'}, fragment: 'loading' })
```

Retrieving Query parameters in ts code
```typescript
ngOnInit() {
  // gets the server
  this.server = this.serversService.getServer(this.route.snapshot.params['id']);

  // get the id of the server
  this.paramsSubscription = this.route.params.subscribe(
    (params) => this.currentId = params.id
  );
}
```

# Nesting Routes
  - Steps
    - Place the child routes in **children** array
    - Place router-outlet html element tag in the parent component template where you want the children component to be loaded

Our typescript routes configruation goes from this to 
```typescript
const appRoutes: Routes = [
  {path: 'home', component: HomeComponent},

  {path: 'users', component: UsersComponent},

  {path: 'users/:id', component: UserComponent},

  {path: 'servers', component: ServersComponent},

  {path: 'servers/:id/edit', component: EditServerComponent},

  {path: 'servers/:id', component: ServerComponent},

  { path: '**', redirectTo: '/home', pathMatch: 'full' },
];
```
{: file='app.module.ts'}

goes to this with nested routes
```typescript
const appRoutes: Routes = [
  // localhost/home
  {path: 'home', component: HomeComponent},

  // localhost/users
  {path: 'users', component: UsersComponent, children: [
    {path: ':id', component: UserComponent},
  ]},

  // localhost/servers
  {path: 'servers', component: ServersComponent, children: [
    {path: ':id', component: ServerComponent},
    {path: ':id/edit', component: EditServerComponent},
  ]},

  // wildcard route
  { path: '**', redirectTo: '/home', pathMatch: 'full' },
];
```
{: file='app.module.ts'}

```html
<div class="col-xs-12 col-sm-4">
  <router-outlet></router-outlet>
</div>
```
{: file='servers.component.html'}



# Route Guards
  - Are a way of protecting routes in angular
  - there are multiple route guard types

| Route Guard      | Description                                         |
| :--------------- | :-------------------------------------------------- |
| canActivate      | Protects route and all of its child routes          |
| canActivateChild | Protects all the child routes                       |
| canDeactivate    | Controll if the user can navigate away from a route |


## canActivate example
  - Angular route guards are interfaces provided by Angular which, when implemented, allow us to control the accessibility of a route based on conditions provided in class implementation of that interface.
  - [depreciated class based guards](https://blog.herodevs.com/functional-router-guards-in-angular-15-open-the-door-to-happier-code-4a53bb60f78a)

  - Steps
    - Have a function that checks some logic
    - export a function from a file that will inject the service dependency and check if the current user passes the logic checks
    - next place the exported function in the app-routing.module.ts canActivate array for the routes you want it applied to


We are creating the function that holds our logic **GuardCheck()**
```typescript
import { Injectable } from '@angular/core';
import { of } from 'rxjs';
import { tap } from 'rxjs/operators';

@Injectable({
  providedIn: 'root'
})
export class UserService {
  isAllowed: boolean = false;

  GuardCheck(){
    this.isAllowed = false;
    return of(this.isAllowed).pipe(tap( (v) => console.log(v)));
  }
}
```
{: file='user.service.ts'}
    

We are exporting our guard function that takes in **ActivatedRouteSnapshot**
```typescript
import { inject } from "@angular/core";
import { ActivatedRouteSnapshot, createUrlTreeFromSnapshot } from "@angular/router";
import { UserService } from "./user.service";
import { map } from "rxjs/operators";

export const authGuard = (next: ActivatedRouteSnapshot) => {
  return inject(UserService)
    .GuardCheck()
    .pipe(
      map( (isAllowed) => 
        isAllowed ? true : createUrlTreeFromSnapshot(next, ['/', 'notFound'])
      )
    )
}
```
{: file='auth-gurard.ts'}


We are adding the exported function created above and putting it in our **canActivate array**
```typescript
const appRoutes: Routes = [
  // localhost/home
  {path: 'home', component: HomeComponent, canActivate: [authGuard]},

  // ... other routes defined here
]
```
{: file='app-routing.module.ts'}

## canDeactivate example
  - used when you want execute some action or logic when a user leaves a route
  - the example we are going to do is check if a user has saved changes before leaving a route
  - There was a pretty major change where angular went from class based to function based route guards

```typescript
@Component({
  // ..
})
export class EditServerComponent implements OnInit{
  // ..
  public changesSaved: boolean = false;

  // constructor
  constructor(
    private serversService: ServersService,
    private route: ActivatedRoute,
    private router: Router
  ) { }

  ngOnInit() {
    // ..
  }

  canDeactivate(){
    if(this.changesSaved === false){
      return confirm('Are you sure you want to exit without saving changes');
    }
  }

}
```
{: file='edit-server.component.ts'}

```typescript
  // localhost/servers
  {path: 'servers', component: ServersComponent, children: [
    {path: ':id', component: ServerComponent},
    {path: ':id/edit', component: EditServerComponent, canDeactivate: [ (component) => component.canDeactivate() ]},
  ]},
```
{: file='app-routing.module.ts'}

# Passing data to a route

## Passing Static data to a route
  - Steps
    - setup route configuration with the data property assigned with a json object
    - read the contents of the data by injecting **ActivatedRoute** into the component and using `route.snapshot.data['key']` or using `route.data.subscribe( (data: Data) => {this.message = data['key']})`

```typescript
{path: 'notFound', component: ErrorPageComponent, data: {message: 'Page not found!'}},
```
{: file='app-routing.module.ts'}

```typescript
export class ErrorPageComponent implements OnInit{
  message: string;

  constructor(private route: ActivatedRoute){
  }

  ngOnInit(): void {
    // option 1
    this.message = this.route.snapshot.data['message'];

    // option 2 
    this.route.data.subscribe(
      (data: Data) => this.message = data['message']
    )
  }

}
```
{: file='error-page.component.ts'}

## Passing Dynamic data to route
  - [depreciated Resolve to ResolveFn](https://blog.bitsrc.io/how-ive-replaced-deprecated-resolvers-in-angular-16-59811f79cd5b)
  - the only way to achieve this before angular 15 was to use a **Resolver**
  - Class-based resolvers have been already deprecated in the Angular v15 release, but now with version 16, when the functional approach is even more common
  - Steps
    - Create the **ResolverFn** function the thing that is is going to be returning should be passed as the generic type in diamond brackets

Resolver function created here and exported
```typescript
export const ServerResolver: ResolveFn<Server> = 
  (route: ActivatedRouteSnapshot, state: RouterStateSnapshot) => {
  return inject(ServersService).getServer(+route.params['id']);
}
```

The **resolve** key is used here
  - it takes a js object as the value
  - key in the js object can be whatever you want
  - the value is the name of the resolver function

```typescript
{path: ':id', component: ServerComponent, resolve: {server: ServerResolver} },
```

Now in this case of the **ServerComponent** now before ngOnInit is called it will have the data passed by the step above in the route.data object
```typescript
  constructor(
    private serversService: ServersService,
    private route: ActivatedRoute
    ) { }  

    ngOnInit() {
    // gets the server to render from the data that is published by the server resolver
    this.route.data.subscribe(
      (data: Data) => {
        this.server = data['server'];
      }
    );
  }
```

# Location Strategy
  - There are two main types of location stragety for angular
  - what is location strategy
    - how a url is parsed
  - 1. Path Location stragety (default)
    - normal default localhost/user/1
  - 2. hash location strategy
    - localhost/#/user/1
    - anything before the # is the host
    - anything after the # is the endpoint for the host

## Hash Stategy
  - easy to implement
  - **useHash** in app.module.ts

```typescript
@NgModule({
  imports: [
    RouterModule.forRoot(appRoutes, {useHash: true})
  ],
  // ..
})
export class AppRoutingModule {
}
```

# Observables
  - ![alt-text](/2023-11-15-angular-section-11-14-routing-observables/observable.png)
  - can be thought of as a data source
  - follows the observable timeline
    - observer & observable
  - timeline
    - mulitple events emitted by the observable
    - the observer does something when that happens. (subscribe function)
  - 3 types of data you can receive
    - handle data
    - handle errors
    - handle completion
  - angular observables are unsubscribed and handled by angular
  - observalbe will stop when an error is pushed or it is complete

## Installation
  - `npm install --save rxjs@6`
  - `npm install --save rxjs-compat`

## Observer data methods

| method name | Description                           |
| :---------- | :------------------------------------ |
| .next()     | next action for the observer          |
| .error()    | send an error                         |
| .complete() | tell the observer that it is complete |

## Creating our own observable
  - use the Observable() constructor to create a new Observable

```typescript
import {Observable} from 'rxjs';

// ..

// creating the observable
const observable = new Observable(
  (observer) => {
    let count = 0;
    setInterval(() => {
      observer.next(count++);
      if(count == 10){
        // observer.error('there was a fucking error');
        observer.complete();
      }
    }, 1000)
  }
)

observable.subscribe(
  (data) => {
    console.log(`data = ${data}`);
  },

  (error) => {
    console.log(`there was an error dickwad`);
    console.log(error);
  },

  () => {
    console.log(`complete`);
  }
)
```

## Operators
  - operators sit between the observable data and the subscription maniuplating data in between
  - so that means data gets transformed before reaching the observer
  - there are many different operators

Example uses map() to transform data before the observer receives the data
```typescript
// transform data before subscribing
observable.pipe(map( (data: number) => {
  return 'Round ' + (data + 1)
}))
.subscribe(
  (data) => {
    console.log(`data = ${data}`);
  },
  (error) => {
    console.log(`there was an error`);
    console.log(error);
  },
  () => {
    console.log(`observable complete`);
  }
)
```

Example using filter and map to 
```typescript
observable.pipe(
  // filter results
  filter( (data: number) => {
    return data > 0;
  }), 
  // map or transform results
  map( (data: number) => {
  return 'Round ' + (data + 1)
  })
)
.subscribe(
  (data) => {
    console.log(`data = ${data}`);
  },
  (error) => {
    console.log(`there was an error`);
    console.log(error);
  },
  () => {
    console.log(`observable complete`);
  }
)
```

## Subjects
  - subjects are not passive like observables, meaning that they can be triggered with code in the observer
  - you use .next with a subject to emit an event or 
  - preferred way of communication
  - ![alt-text](/2023-11-15-angular-section-11-14-routing-observables/subject.png)

```typescript
@Injectable({
  providedIn: 'root'
})
export class UserService {
  activatedSubject = new Subject<boolean>()
}
```

```typescript
export class AppComponent implements OnInit, OnDestroy {
  activated = false;
  activatedSubscription: Subscription;

  constructor(private us: UserService) {}

  ngOnInit() {
    // subscribe to the subject
    this.activatedSubscription = this.us.activatedSubject
    .subscribe(
      (data) => {
        this.activated = data;
      })
  }
  
  ngOnDestroy(): void {
    this.activatedSubscription.unsubscribe();
  }

}
```

```typescript
  onActivate(){
    this.us.activatedEventEmitter.next(true);
  }
```
