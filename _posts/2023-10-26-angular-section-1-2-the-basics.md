---
layout: post
title: Angular Section 1,2. The Basics
date: 2023-10-26 08:35 -0500
categories: [Angular, Udemy]
image: 
  path: /2023-10-26-angular-section-1-2-the-basics/profile.png 
---

- [References](#references)
- [What is Angular](#what-is-angular)
  - [What is a SPA](#what-is-a-spa)
- [Angular Versions Explained](#angular-versions-explained)
- [Angular Pre-requisites \& Install](#angular-pre-requisites--install)
- [Angular CLI](#angular-cli)
  - [Create new project](#create-new-project)
  - [Run your application](#run-your-application)
- [Angular project structure](#angular-project-structure)
- [Course Structure](#course-structure)
- [Ts-node](#ts-node)
- [How angular works](#how-angular-works)
  - [How the does the index.html file know to load angular](#how-the-does-the-indexhtml-file-know-to-load-angular)
  - [Where is the main method that gets triggered in angular project](#where-is-the-main-method-that-gets-triggered-in-angular-project)
  - [Where is this AppModule that gets bootstrapped and starts the angular app](#where-is-this-appmodule-that-gets-bootstrapped-and-starts-the-angular-app)
- [Installling bootstrap css for the project](#installling-bootstrap-css-for-the-project)
- [Angular Components](#angular-components)
  - [Creating our own Component (**Manually**)](#creating-our-own-component-manually)
  - [Creating our own component via (**CLI**)](#creating-our-own-component-via-cli)
  - [Inline template \& Css](#inline-template--css)
- [Component Selector](#component-selector)
- [Databinding](#databinding)
  - [String interpolation](#string-interpolation)
  - [Property Binding](#property-binding)
  - [Event Binding](#event-binding)
  - [Passing $event to an Event binding](#passing-event-to-an-event-binding)
  - [Two-Way Binding](#two-way-binding)
- [Directives](#directives)
- [NgIf](#ngif)
  - [else for NgIf](#else-for-ngif)
    - [ng-template](#ng-template)
  - [Local References](#local-references)
- [ngStyle](#ngstyle)
- [ngClass](#ngclass)
- [\*ngFor](#ngfor)
  - [Getting the index for \*ngFor](#getting-the-index-for-ngfor)


# References
  - How an angular project is started
  - {% include embed/youtube.html id='ua2NONiy-7A' %}

# What is Angular
  - Angular is a js framework for (SPA's) **Single page applications**

## What is a SPA
  - Single page application
  - Single html file is loaded at the start, but as you navigate around the site it is still the same html file, It is only rendering different views on the page with javascript loading it in the background

Why is this good?
  - good for performance
  - the client no longer has to go out and talk to the server with every request like it used to. Instead it only reaches out to the server in the background when it needs some additional info from the server making it very responsive

# Angular Versions Explained
  - ![alt-text](/2023-10-26-angular-section-1-2-the-basics/angular_versions.png)
  - started with AngularJS (Angular 1)
    - totally different than what angular is today
    - not future proof because of fundamental structure
    - Called "Angular JS"

  - Angular 2 was a complely re-write
    - released in 2016
    - Called just "Angular"
  - Angular 4 
    - Angular 3 was not released for internal things
  - Angular 10, 11, 12, ...
    - new major version is released every 6 months
    - small, incremental, backwards-compatiable changes

# Angular Pre-requisites & Install
  - Node is required 
  - I am using nvm for my node version management
  - `nvm use 16.14`
  - `npm install -g @angular/cli`
  - `ng version`

```text
tpool@tpool-thinkpad-l480:~/Playground/Udemy/Angular/Section1/my-first-app$ ng version

     _                      _                 ____ _     ___
    / \   _ __   __ _ _   _| | __ _ _ __     / ___| |   |_ _|
   / △ \ | '_ \ / _` | | | | |/ _` | '__|   | |   | |    | |
  / ___ \| | | | (_| | |_| | | (_| | |      | |___| |___ | |
 /_/   \_\_| |_|\__, |\__,_|_|\__,_|_|       \____|_____|___|
                |___/
    

Angular CLI: 16.2.8
Node: 16.14.1
Package Manager: npm 8.5.0
OS: linux x64

Angular: 16.2.11
... animations, common, compiler, compiler-cli, core, forms
... platform-browser, platform-browser-dynamic, router

Package                         Version
---------------------------------------------------------
@angular-devkit/architect       0.1602.8
@angular-devkit/build-angular   16.2.8
@angular-devkit/core            16.2.8
@angular-devkit/schematics      16.2.8
@angular/cli                    16.2.8
@schematics/angular             16.2.8
rxjs                            7.8.1
typescript                      5.1.6
zone.js                         0.13.3
    
[1]+  Done                    code .
```
  
# Angular CLI
  - [github-repo](https://github.com/angular/angular-cli)
  - [angular docs workflow](https://angular.io/cli)

## Create new project
  - `ng new <project-name> --no-strict`
    - `--no-strict` 
      - Strict mode improves maintainability, helps you catch bugs ahead of time, and turns runtime errors into compile-time errors.
    - common convention to use lowercase letters for the project name
    - then it will ask you the following
      - add angular routing?
      - which stylesheet format you would like to use

  You will then see the following of angular bootstrapping your application
  - ![alt-text](/2023-10-26-angular-section-1-2-the-basics/terminal_creating_project.png)

## Run your application
  - `ng serve`
  - it will run on port 4200 by default

You will see this if you navigate to localhost:4200
  - ![alt-text](/2023-10-26-angular-section-1-2-the-basics/default_page.png)
  

# Angular project structure

```text
your-angular-app/
│
├── e2e/                  # End-to-End test files
│
├── node_modules/          # Node.js modules (third-party packages)
│
├── src/                   # Source code of your Angular app
│   │
│   ├── app/               # Main application code
│   │
│   ├── assets/            # Static assets (images, fonts, etc.)
│   │
│   ├── environments/      # Environment-specific configuration
│   │
│   ├── index.html         # The main HTML file
│   │
│   ├── main.ts            # Entry point for the application
│   │
│   ├── styles.css         # Global CSS styles
│   │
│   └── ...
│
├── .angular.json           # Angular CLI configuration
│
├── package.json            # Project dependencies and scripts
│
├── tsconfig.json           # TypeScript configuration
│
├── tslint.json             # TSLint configuration (if used)
│
└── ...
```

# Course Structure
  - ![alt-text](/2023-10-26-angular-section-1-2-the-basics/course_structure.png)

# Ts-node
  - I am using ts-node for typescript REPL for practice and experimenting
  - just type `ts-node` in the terminal after installing it via npm and you will get a REPL environment for ts

# How angular works 
  - The typescript we write gets compiled to javascript so that way when the code is deployed, the client can do all the processing on their side

## How the does the index.html file know to load angular
  - The script imports at the end of the html file are what the cli imports automatically. This triggers angular

## Where is the main method that gets triggered in angular project
  -  src/main.ts

```typescript
import { platformBrowserDynamic } from '@angular/platform-browser-dynamic';

import { AppModule } from './app/app.module';

// bootstrap the AppModule and start the application
platformBrowserDynamic().bootstrapModule(AppModule)
  .catch(err => console.error(err));
```

## Where is this AppModule that gets bootstrapped and starts the angular app
  - src/app
  - this folder has all the parts for the AppModule where app.module.ts has the outer layer

app.module.ts
```typescript
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';

import { AppComponent } from './app.component';

@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```


app.component.ts creates the component
```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})


export class AppComponent {
  title = 'my-new-project';
}
```

And app.component.html contains the html code for the AppComponent



# Installling bootstrap css for the project
  - `npm install --save bootstrap@3`
  - we will be using bootstrap 3 for this course
  
Now update angular.json to include the bootstrap files
  - you can copy the relative path to the boostrap css file you would like to use and copy to the angular.json file

```json
"styles": [
  "src/styles.css",
  "node_modules/bootstrap/dist/css/bootstap.min.css"
],
```

# Angular Components
  - The entire application is built upon **Components**
  - each component has it's own html, css, and it's own business logic
  - Allows you to **split up** your complex application into **re-usable parts**
  - Best practice says to place components inside their own folder inside the app directory

## Creating our own Component (**Manually**)
  - we want to create a server component
  - server component code will go in src/app/server

We create our component as follows

```typescript
import { Component } from "@angular/core";

@Component({
  selector: 'app-server',
  templateUrl: './server.component.html'
})

export class ServerComponent {
}
```
{: file='src/app/server/server.component.ts'}



We have simple html code for our component like this

```html
<h2>server component</h2>
```
{: file='src/app/server/server.component.html'}


We have to tell the main AppModule to load our component
```typescript
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { AppComponent } from './app.component';

// our new server component
import { ServerComponent } from './server/server.component';

@NgModule({
  declarations: [
    AppComponent,
    ServerComponent // register our server component in the app module
  ],
  imports: [
    BrowserModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```
{: file='src/app/app.module.ts'}

Now finally we can render our new component in the app-root

```html
<h3>I'm in the app component</h3>

<br>

<app-server></app-server>
```
{: file='src/app/app.component.html'}

## Creating our own component via (**CLI**)
  - `ng generate component servers` or for short `ng g c servers`
  - This will generate the same code and will even update the **app.module.ts** to add the component to be used
  - THIS IS AWESOME!!!


## Inline template & Css
  - you can have your html templates inline with the typescript code instead of in a separate file
  - you have to use **template** instead of templateUrl
  - you can also use css in the ts file with **styles**

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-servers',

  // use a html file
  // templateUrl: './servers.component.html',

  // use html inline
  template: '<app-server></app-server><app-server></app-server>',

  // use a css file
  // styleUrls: ['./servers.component.css']

  // use css inline
  styles: [`
  h3 {
    color: dodgerblue;
  }
  `]
})
export class ServersComponent implements OnInit {

  ngOnInit(): void {
    console.log('')
  }

}
```
{: file='src/app/servers/servers.component.ts'}


# Component Selector
  - we can tell angular to have our component be an html element, an id or an attribute
  - selecting by id won't work
  - pseudo selectors like :hover will not work
  - typically use for html elements


Below is an example of a html element

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
  // <app-servers> </app-servers>
  selector: 'app-servers',

  templateUrl: './servers.component.html',

  styleUrls: ['./servers.component.css']
})
export class ServersComponent implements OnInit {

  ngOnInit(): void {
    console.log('')
  }

}
```
{: file='src/app/servers/servers.component.ts'}


```html
<app-servers></app-servers>
```
{: file='src/app/app.component.html'}


If we wanted our component to be an html attribute

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
  // <div app-servers>
  selector: '[app-servers]',

  templateUrl: './servers.component.html',

  styleUrls: ['./servers.component.css']
})
export class ServersComponent implements OnInit {

  ngOnInit(): void {
    console.log('')
  }

}
```
{: file='src/app/servers/servers.component.ts'}

```html
<div app-servers="">
</div>
```
{: file='src/app/app.component.html'}

If we wanted our component to be an class

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
  // <div class="app-servers">
  selector: '[app-servers]',

  templateUrl: './servers.component.html',

  styleUrls: ['./servers.component.css']
})
export class ServersComponent implements OnInit {

  ngOnInit(): void {
    console.log('')
  }

}
```
{: file='src/app/servers/servers.component.ts'}

```html
<div class="app-servers">
</div>
```
{: file='src/app/app.component.html'}


# Databinding
  - Communication between typescript business logic and html template code
  - ![alt-text](/2023-10-26-angular-section-1-2-the-basics/databinding.png)
  - 4 types of Databinding
    - String interpolation
      - `{{ data }}`
      - just display the data

    - Property Binding
      - `[property] = "data"`
      - have the the property be tied to an element

    - Event Binding
      - `(event) = "expression"`
      - have an even trigger an expression

    - Two-Way-Binding
      - `[(ngModel)] = "data"`
  
  
## String interpolation
  - expression placed between the {{ expressionHere }}
  - As long as the expression resolves to a string it will work without issue
  - You also cannot write multi-line expression between the curly braces

```typescript
import { Component } from "@angular/core";

@Component({
  selector: 'app-server',
  templateUrl: './server.component.html'
})

export class ServerComponent {
  // our two variables
  server_id: number = 1000;
  status: string = 'Down';
}
```
{: file='src/app/server/server.component.ts'}

```html
<p>Server with ID: {{ server_id }} is {{ status }} </p>
```
{: file='src/app/server/server.component.html'}


## Property Binding
  - bind a property like **disabled** for a button to a variable
  - `[disabled]="allowNewServer"`
  - This will bind the !allowNewServer variable to the disabled property 
  - so when the allowNewServer is true, the button will be disabled
  - and when allowNewServer is false, the button will not be disabled


```typescript
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-servers',
  templateUrl: './servers.component.html',
})
export class ServersComponent {
  allowNewServer:boolean = false;
  
  // after two seconds allowNewServerWillBeSetToTrue
  constructor() {
    setTimeout(() => {
      this.allowNewServer = true;
    }, 2000);
  }

}
```
{: file='src/app/server/server.component.ts'}


```html
<button class="btn btn-primary" [disabled]="!allowNewServer" >Add server</button>

<app-server></app-server>
<app-server></app-server>
```
{: file='src/app/server/server.component.html'}

## Event Binding
  - we want a button to trigger a function in our code
  - `(click)="onCreateServer()"`

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-servers',
  templateUrl: './servers.component.html',
})
export class ServersComponent {
  // variables
  allowNewServer:boolean = false;
  serverCreationStatus = "No server was created!"
  
  // after the button is created, it will wait for two seconds then disable it
  constructor() {
    setTimeout(() => {
      this.allowNewServer = true;
    }, 2000);
  }

  onCreateServer():void {
    this.serverCreationStatus = "Server was created!";
  }

}
```
{: file='src/app/server/server.component.ts'}


```html
<button class="btn btn-primary" (click)="onCreateServer()" >Add server</button>

<p>{{serverCreationStatus}}</p>

<app-server></app-server>
<app-server></app-server>

```
{: file='src/app/server/server.component.html'}

## Passing $event to an Event binding
  - we can pass **$event** to our event functions to pass the event that has happend during the event binding
  - we can manipulate $event in our ts code

```typescript
@Component({
  //
})
export class ServersComponent {
  // variables
  allowNewServer:boolean = false;
  serverCreationStatus = "No server was created!"
  serverName = '';
  
  onCreateServer():void {
    this.serverCreationStatus = "Server was created!";
  }

  // $event gets passed here
  onUpdateServerName(event: Event) {
    // the stuff in parens are just to make tyepscript happy
    this.serverName = (<HTMLInputElement>event.target).value;
  }

}
```
{: file='src/app/server/server.component.ts'}j


```html
<input 
  type="text"
  class="form-control"
  (input)="onUpdateServerName($event)" 
>

<p>{{serverName}}</p>
```
{: file='src/app/server/server.component.html'}

## Two-Way Binding
  - to enable two-way binding you must add the FormsModule to the imports array in the AppModule
  - This is done below

```typescript
// ..
import { FormsModule } from '@angular/forms';

@NgModule({
  declarations: [
    // ..
  ],
  imports: [
    BrowserModule,
    FormsModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```
{: file='src/app/app.module.ts'}

Here we are binding to the variable **serverName**

```html
<!-- Binded to the variable -->
<input 
  type="text"
  class="form-control"
  [(ngModel)]="serverName"
>

<!-- Not binded to the model
  meaning if it were to change somewhere else, the change would not be reflected here
 -->
<input 
  type="text"
  class="form-control"
  (input)="onUpdateServerName($event)"
>

<p>{{serverName}}</p>
```


# Directives
  - directives are instructions in the DOM
  - They are built-in directives into angular
  - You can also create your own like we have been doing like below
  - example below
  - `<p appTurnGreen>Receives a green background!</p>`

```typescript
@Directive({
  selector: '[appTurnGreen]'
})
export class TurnGreenDirective {
  // ...
}
```

# NgIf
  - `<p *ngIf="serverCreated">Server was created, server name is {{serverName}}</p>`
  - the ***** at the beginning of *ngIf indicates that this is a **STRUCTURAL DIRECTIVE**
    - used to change the structure of the view by manipulating the DOM
  - note that p element will not be there if serverCreated is false
  - if serverCreated is true angular will place the p element on the page

## else for NgIf
  - we can add an else condition to an *ngIf by looking at the following example
  - `*ngIf="serverCreated; else noServer "`
    - **noServer** is referring to the local reference in the code below

  - `<ng-template #noServer>`
    - the #noServer specifies a local reference that is referred to in the ***ngIf** above

```html
<!-- Server created -->
<p 
  *ngIf="serverCreated; else noServer ">Server was created, server name is {{serverName}}</p>

<!-- no server created -->
<ng-template #noServer>
  <p>No server was created!</p>
</ng-template>
```

### ng-template
  - The `ng-template` directive itself doesn't produce any visible output in the DOM; instead, it acts as a placeholder for content that can be used in conjunction with other directives to control the rendering of that content. 
  - It is often used with other structural directives like *ngIf, *ngFor, and *ngSwitch, allowing you to define template fragments 

## Local References
  - local references, also known as template reference variables
  - are used to capture references to elements or directives in the template and make them accessible within the component's TypeScript code. 
  - Local references are prefixed with a hash (#) in the template

```html
<!-- Using a local reference with an input element -->
<input #myInput type="text">

<!-- Using a local reference with an Angular directive (ngIf) -->
<div *ngIf="showElement" #conditionalDiv>This element is conditionally displayed.</div>
```

  - In the examples above, #myInput and #conditionalDiv are local references to the input element and the ngIf-controlled div element, respectively.
  - You can then access these local references in your component's TypeScript code by using @ViewChild or @ViewChildren decorators. For example:

```typescript
import { Component, ViewChild } from '@angular/core';

@Component({
  selector: 'app-example',
  template: `
    <input #myInput type="text">
    <button (click)="showValue()">Show Input Value</button>
  `,
})
export class ExampleComponent {
  @ViewChild('myInput') myInput: ElementRef;

  showValue() {
    console.log(this.myInput.nativeElement.value);
  }
}
```

# ngStyle
  - an **attribute directive**
  - dynamically assign a style
  - attribute directives **don't add or remove elements**, they only **change** the elementes they were placed on 

```html
<p [ngStyle]="{backgroundColor: getColor()}">Server with ID: {{ server_id }} is {{ status }} </p>
```

```typescript
@Component({
  // ...
})

export class ServerComponent {
  // our two variables
  server_id: number = 1000;
  status: string = '';

  constructor() {
    this.status = Math.random() > 0.5 ? 'online' : 'offline';
  }

  getServerStatus() {
    return this.status;
  }

  getColor() {
    if (this.status === 'online') {
      return 'green';
    }
    else {
      return 'red';
    }
  }
}
```

# ngClass
  - apply classes to an element dynamically based on a condition
  - `[ngClass]="{'online': status === 'online'}"`
  - here we are using property binding by surrounding the ngClass directive with **[]**
  - we are saying apply the **online** class to the **p** element if **status === 'online'**

```html
<p 
  [ngStyle]="{backgroundColor: getColor()}"
  [ngClass]="{'online': status === 'online'}">Server with ID: {{ server_id }} is {{ status }} </p>
```

```typescript
@Component({
  // ...
  styles: [`
    .online {
      color: white;
    }
  `]
})

export class ServerComponent {
  // ...
}
```

# *ngFor
  - **structure directive**
  - adds 0 to many elements based on the loop presented to **ngFor**
  `<app-server *ngFor="let server of servers"></app-server>`
    - this will loop through array of **servers** and create as many as there is in servers

## Getting the index for *ngFor
  - we want to get the index for an element during the loop using ngFor
