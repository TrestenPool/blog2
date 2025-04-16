---
layout: post
title: Angular Section 5,6,7,8. Components, Databinding, Advanced Directives
date: 2023-10-30 12:25 -0500
categories: [Angular, Udemy]
image: 
  path: /2023-10-30-angular-section-5-6-7-8-components-databinding-advanced-directives/profile.png
---

- [Passing data between different components](#passing-data-between-different-components)
- [@Input Decorator](#input-decorator)
- [Emitting events with @Output](#emitting-events-with-output)
- [View encapsulation](#view-encapsulation)
- [Using local references in templates](#using-local-references-in-templates)
- [Accessing Local references through the DOM with @ViewChild](#accessing-local-references-through-the-dom-with-viewchild)
- [Projecting content into component with ng-content](#projecting-content-into-component-with-ng-content)
- [Component lifecycle](#component-lifecycle)
- [@ContentChild()](#contentchild)
- [Directives](#directives)
  - [Attribute Directives](#attribute-directives)
    - [NgClass](#ngclass)
    - [NgStyle](#ngstyle)
  - [Structural Directives](#structural-directives)
    - [Why do we need the \* in structural directives?](#why-do-we-need-the--in-structural-directives)
    - [Creating our own Structural Directive](#creating-our-own-structural-directive)
    - [NgSwitch](#ngswitch)
  - [Creating our own Atribute Directives](#creating-our-own-atribute-directives)
    - [@HostListener](#hostlistener)
    - [@HostBinding](#hostbinding)
    - [Bind property to a directive](#bind-property-to-a-directive)
    - [Special case for passing down string data](#special-case-for-passing-down-string-data)


# Passing data between different components
  - we want to pass data between different components but don't know how to do up to this point

# @Input Decorator 
  - @Input is a decorator in Angular used to declare an input property in a component. Input properties allow data to be passed into a component from its parent component. This is a fundamental concept in Angular, and it enables parent-child communication within your application.
  - we can use property and event binding on html elements and their native properties and events
  - we can use property binding on **directives** 
  - we can also property binding on our custom components properties and events

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent {
  serverElements = [ {type: 'server', name: 'testsever', content: 'just a test'} ];
}
```
{: file='app.component.ts'}

```html
<app-server-element 
  *ngFor="let serverElement of serverElements"
  [element]="serverElement"> <!-- this is setting the element variable for app-server-element -->
  </app-server-element>
```
{: file='app.component.html'}

```typescript
import { Component, Input, OnInit } from '@angular/core';

@Component({
  selector: 'app-server-element',
  templateUrl: './server-element.component.html'
})
export class ServerElementComponent implements OnInit {
  // this annotation is to tell angular that this property can be used to property bind as an input
  @Input()
  element: {type: string, name: string, content: string};

  constructor() { }

  ngOnInit(): void {
  }

}

```
{: file='server-element.component.ts'}

```html
<div 
  class="panel panel-default">
  <div class="panel-heading">{{ element.name }}</div>
  <div class="panel-body">
    <p>
      <strong *ngIf="element.type === 'server'" style="color: red">{{ element.content }}</strong>
      <em *ngIf="element.type === 'blueprint'">{{ element.content }}</em>
    </p>
  </div>
</div>

```
{: file='server-element.component.html'}

If you wanted to bind to the same property but reference it by a different name you would just have to pass that as a string to **@Input('varName')**

```typescript
@Input('myPropertyName')
```

```html
[element]="serverElement"> 
```


# Emitting events with @Output
  - with @Input it allows the parent to bind to a variable in the child component
  - but what if we want our child component notifiy our parent component when a change is made

Here in the app root we are binding to the **serverCreated & blueprintCreated event** 
  - these events are declared in the cockpit typescript file 
  - We bind these to the methods onServerAdded() & onBlueprintAdded() that we have declared in the app root type script file 

```typescript
  <app-cockpit 
    (serverCreated)="onServerAdded($event)"
    (blueprintCreated)="onBlueprintAdded($event)">
    </app-cockpit>
```
{: file='app.component.html'}

Take note of the @Outut annotation  
  - this means that a parent component can bind to it

Take note of **.emit()**
  - We are saying when the button is pressed, it will emmit an event where anyone who is listening for that event will trigger an event to occur

```typescript
@Component({
  // ...
})
export class CockpitComponent {
  @Output()
  serverCreated     = new EventEmitter<{serverName: string, serverContent: string}>();
  @Output()
  blueprintCreated  = new EventEmitter<{serverName: string, serverContent: string}>();

  onAddServer() {
    this.serverCreated.emit({
      serverName: this.newServerName,
      serverContent: this.newServerContent
    });
  }
  
  onAddBlueprint() {
    this.blueprintCreated.emit({
      serverName: this.newServerName,
      serverContent: this.newServerContent
    });
  }
}
```
{: file='cockpit.component.ts'}

# View encapsulation
  - when you have a .css file for a component it will be only applied for that component
  - for example if you set all paragraphs elements be blue it will only assign blue to paragraphs in that specific component only
    - it does this by assigning each html element a unique html attribute and css will reference that html attribute in the css file. 
    - you don't have to nothing to achieve this behavior as it is default
  - this emulates shadow dom

You can change the **view encapsulation** by using the **encapsulation** key in the **@Component** settings
  - you change change to the following options
    - Emulated - default
    - None
    - ShadowDom

```typescript
@Component({
  // ...
  // Three options
  encapsulation: ViewEncapsulation.Emulated
  encapsulation: ViewEncapsulation.None
  encapsulation: ViewEncapsulation.ShadowDom
})
export class ServerElementComponent implements OnInit {
  // ...
}
```

# Using local references in templates
  - you can use local references in templates to pass data to a function instead of using two-way databinding
  - local references are denoted with **#**

Example
  - we are using two local references **#serverNameInput & #contentInput**
  - we can use this local reference in the **template only**
  - we are passing both local references to the functions called by button input

```html
<input 
  type="text" 
  class="form-control" 
  #serverNameInput
  >

<input 
  type="text" 
  class="form-control"
  #contentInput
  >

<br>

<!-- buttons -->
<button class="btn btn-primary" (click)="onAddServer(serverNameInput, contentInput)">Add Server</button>
<button class="btn btn-primary" (click)="onAddBlueprint(contentInput, contentInput)">Add Server Blueprint</button>
```

typescript code
  - in the typescript code we are passing the local references to it by **HtmlInputElements**
  - below is an example of one of the functions taking advantage of passing the local references as arguments

```typescript
  onAddServer(nameInput: HTMLInputElement, contentInput: HTMLInputElement) {
    console.log(nameInput.value);
    this.serverCreated.emit({
      serverName: nameInput.value,
      serverContent: contentInput.value
    });
  }
```

# Accessing Local references through the DOM with @ViewChild
  - in the previous example we see how we can pass the local reference to a function that is executed in the typescript
  - but what if we don't want to pass the variable as an argument just to get the local reference and instead just want to access it directly
  - we can do exactly this with **@ViewChild**

Example html file
  - we have a simple text input with the local reference #contentInput

```html
<input 
  type="text" 
  class="form-control"
  #contentInput
  >
```

Example typescript code
  - to have access to this local reference with @ViewChild()

```typescript
@ViewChild('contentInput', {static: false})
serverContentInput: ElementRef;

myfunc(){
  // accessing the value of the input
  let x = this.serverContentInput.nativeElement.value;
}
```

# Projecting content into component with ng-content
  - if want to project content into your component then look no further than **ng-content**
  - typically used for widgets and complex operations that can be passed from another component

```html
<div 
  class="panel panel-default">
  <div class="panel-body">

    <!-- contents get projected here -->
    <ng-content></ng-content>

  </div>
</div>
```

```html
<app-server-element 
  *ngFor="let serverElement of serverElements"
  [element]="serverElement"> 

  <!-- element that is getting projected -->
  <p>
    <strong *ngIf="serverElement.type === 'server'" style="color: red">{{ serverElement.content }}</strong>
    <em *ngIf="serverElement.type === 'blueprint'">{{ serverElement.content }}</em>
  </p>
  <!-- element that is getting projected -->

  </app-server-element>
```


# Component lifecycle
  - In Angular, components go through a series of lifecycle events and hooks from creation to destruction
  - These lifecycle events allow you to interact with your components at various points during their existence.

| Hook                  | Description                                                              |
| :-------------------- | :----------------------------------------------------------------------- |
| ngOnChanges           | Called after a bound input property changes                              |
| ngOnInit              | Called once the component is initialized. Ran after the constructor      |
| ngDoCheck             | Called during every change detection run                                 |
| ngAfterContentInit    | Called after content (ng-content) has been projected into view          |
| ngAfterContentChecked | Called everytime the projected content has been checked                  |
| ngAfterViewInit       | Called after the component's view (and child views) has been initialized |
| ngAfterViewChecked    | Called every time the view (and child views) have been checked           |
| ngOnDestroy           | Called once the component is about to get destroyed                      |
| ngAfterViewChecked    | Called every time the view (and child views) have been checked           |


# @ContentChild()
  - Say we want access to a local reference that isn't in our component per say
  - meaning if we have some stuff passed through **ng-content** that we know will have a local reference lets say **#paragraphContent**
  - We can access this local reference in the child component with @ContentChild()

code below
  - static: true just means that the child components will be loaded before ngOnInit() so we can reference it in there
  - if static: false that means that the content will not get loaded until after ngOnInit() meaning you can't access the stuff until after ngOnInit is called()
  - this is for when the local reference is not in the component directly but gets projected eventually 

```typescript
@ContentChild('contentParagraph', {static: false})
paragraph: ElementRef
```

# Directives

3 Main Categories


1. Component
  - most common
  - examples
    - ngComponentOutlet
2. Attribute Directives
  - Attribute directives are used to modify the appearance or behavior of an element or component
  - examples
    - ngModel
    - ngIf
    - ngFor
    - ngStyle
    - ngClass
3. * Structural Directives
  - They have a preceding *****
  - Add or remove elements from the DOM
  - examples
    - ngIf
    - ngFor
    - ngSwitch

## Attribute Directives

### NgClass
  - when using ngClass you have to use with square brackets
  - in Angular, you need to wrap ngClass with square brackets [] when you want to bind to a property, expression, or a variable to **dynamically** determine the classes to be applied. 
  - `[ngClass]`
  - There are multiple ways to use ngClass
  - but the main implementation is to use **object expressions**
  - `[ngClass]=" 'class1': condition1, 'class2': condition2 "`

  > Make sure to wrap the classes in `'class1'`
  {: .prompt-danger }

```html
<div *ngIf="onlyOdd">
  <ul class="list-group">
    <li
      class="list-group-item"
      *ngFor="let num of oddNumbers"
      [ngClass]=" {'odd': num % 2 !== 0}"
      >{{ num }}</li>
  </ul>
</div>
```

### NgStyle
  - When you want to apply css styles to your html element dynamically
  - `[ngStyle] = " 'css-property': expression ? 'true' : 'false' "`

```html
<li
  class="list-group-item"
  *ngFor="let num of oddNumbers"
  [ngStyle]="{'background-color': num % 2 !== 0 ? 'yellow' : 'green'}"
>{{ num }}</li>
```


## Structural Directives
  - you can't have more than 1 structural directive on an element
  - only 1 is allowed

### Why do we need the * in structural directives?
  - when you use *ngStructuralDirective we are really just doing just placeing an ngStructural directive in [] and in an ng-template

```html
<p *ngIf="!flag"></p>

<!-- same thing as .. -->
<ng-template [ngIf]="!flag">
</ng-template>
```

### Creating our own Structural Directive
  - we can create our own structural directive


> The @Input() **appUnless** has to be named the **name of the selector** in order to work
{: .prompt-danger }

```typescript
@Directive({
  selector: '[appUnless]'
})
export class UnlessDirective {

  @Input()
  set appUnless(condition: boolean) {
    if(!condition) {
      // if condition is not true, then render the view 
      this.vcREf.createEmbeddedView(this.templateRef);
    }
    else {
      // if the condtiion is true, then clear the contents from the view 
      this.vcREf.clear();
    }
  }

  constructor(
    private templateRef: TemplateRef<any>,
    private vcREf: ViewContainerRef) { 
  }
}
```

```html
<div *appUnless="onlyOdd">
  <p>onlyOdd is False</p>
</div>
```

### NgSwitch
  - just like a switch statement in languages like c and java

```html
<div [ngSwitch]="value">
  <p *ngSwitchCase="5">5</p>
  <p *ngSwitchCase="10">10</p>
  <p *ngSwitchCase="15">15</p>
  <p *ngSwitchDefault>Not a valid value</p>
</div>
```



## Creating our own Atribute Directives

  - `ng generate directive --skip-test basicHighlight`

> `selector: '[appBasicHighlight]'`  tells angular to create an attribute selector, this does not mean that you have to use [] brackets to use this directive
{: .prompt-warning }

```typescript
import { Directive, ElementRef, OnInit } from "@angular/core";

@Directive({
  // camel case is standard convention
  selector: '[appBasicHighlight]'
})
export class BasicHighlightDirective implements OnInit{
  
  constructor(private elementRef: ElementRef) {
  }

  ngOnInit(): void {
    // gets access to the element and changing the background color
    this.elementRef.nativeElement.style.backgroundColor = 'green';
  }


}
```
{: file='basic-highlight.directive.ts'}

```html
<p appBasicHighlight>Style me with a basic directive</p>
```

> We have learned that it is not good to access the elements directly with `this.elementRef.nativeElement.style.backgroundColor = 'green';`
{: .prompt-warning }
  - So what are we supposed to do instead?
  - use **Render2**


```typescript
{ Directive, ElementRef, OnInit, Renderer2 } from '@angular/core';

@Directive({
  selector: '[appBetterHighlight]'
})
export class BetterHighlightDirective implements OnInit {

  constructor(
    private elRef: ElementRef, 
    private renderer: Renderer2) {
  }

  ngOnInit(): void {
    this.renderer.setStyle(this.elRef.nativeElement, 'background-color', 'blue');
    this.renderer.setStyle(this.elRef.nativeElement, 'color', 'white');
  }

}
```

### @HostListener
  - We can use @HostListener to listen for event and respond accordingly
  - we will have the background color change when a mouse enters a paragraph and returns back to original color when it leaves the paragraph


> @HostListener('**mouseenter**') takes an argument of the event it will listen to
{: .prompt-tip }

```typescript
export class BetterHighlightDirective implements OnInit {

  constructor(private elRef: ElementRef, private renderer: Renderer2) {
  }

  changeBackground(color: string){
    this.renderer.setStyle(this.elRef.nativeElement, 'background-color', color);
  }

  @HostListener('mouseenter')
  mouseOver() {
    this.changeBackground('dodgerBlue');
  }

  @HostListener('mouseleave')
  mouseLeave() {
    this.changeBackground('initial');
  }

}
```

### @HostBinding
  - Alternatively to using Renderer2 we can have an element represent the background color and we can update that value and it will be reflected on the page


> @HostBinding('style.backgroundColor') takes an argument that connects to the DOM of the element that this directive is sitting on top off
{: .prompt-info }

```typescript
@Directive({
  selector: '[appBetterHighlight]'
})
export class BetterHighlightDirective implements OnInit {

  @HostBinding('style.backgroundColor')
  backgroundColor: string;


  @HostListener('mouseenter')
  mouseOver() {
    this.backgroundColor = 'dodgerBlue';
  }

  @HostListener('mouseleave')
  mouseLeave() {
    this.backgroundColor = 'initial';
  }

}
```

### Bind property to a directive
  - If we wanted to bind a property to the we have to pass the name of the selector to one of the @Input('nameOfSelector')
  
```typescript
@Directive({
  selector: '[appBetterHighlight]'
})
export class BetterHighlightDirective implements OnInit{

  // inputs
  @Input('appBetterHighlight')
  highlightColor: string = 'blue';

  @HostBinding('style.backgroundColor')
  backgroundColor: string = this.highlightColor;

  // happens after the directives gets it's inputs
  // otherwise, default color will always be initial
  ngOnInit(): void {
    this.backgroundColor = highlightColor;
  }


  @HostListener('mouseenter')
  mouseOver() {
    this.backgroundColor = this.highlightColor;
  }

  @HostListener('mouseleave')
  mouseLeave() {
    this.backgroundColor = this.defaultColor;
  }

}
```

```html
<p [appBetterHighlight]="'yellow'">Style me with a better directive</p>
```

### Special case for passing down string data
  - normally we have to enclose the property we are trying to pass as in put in [] and wrap in single quotes like this example

```typescript
export class BetterHighlightDirective implements OnInit{

  @Input()
  something: string;

  // ...
}
```

```html
<p 
  appBetterHighlight
  [something]="'hi'"
  >Style me with a better directive</p>
```

> instead we can remove the `[]` and the `''` like this `<p appBetterHighlight something="hi"> I am a paragraph </p>`
{: .prompt-tip }