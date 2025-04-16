---
layout: post
title: Angular Section 3. Course Project
date: 2023-10-27 17:26 -0500
categories: [Angular, Udemy]
image: 
  path: /2023-10-27-angular-section-3-course-project/profile.png
---
- [Course project explained](#course-project-explained)
  - [Planning our app](#planning-our-app)
- [Creating The app](#creating-the-app)
- [Debugging](#debugging)
  - [Sourcemaps](#sourcemaps)
- [Creating our Dropdown directive](#creating-our-dropdown-directive)


# Course project explained
  - we will be creating a project for this course
  - it will be a recipe book & shopping list


## Planning our app
  - ![alt-image](/2023-10-27-angular-section-3-course-project/plan.png)
    - root component will hold all of our components
    - header component to navigate between the two main fetures of our app (Shopping list & Recipe Book)
    - Shopping list components
      - shopping list
      - shopping list edit
    - Recipe Book components
      - Recipe List
      - Receipe Item
      - Recipe Detail
    


# Creating The app
  - `nvm use 16.14`
    - made sure I am using a good version of node with our node version manager (nvm)
  - `ng new courseProject --no-strict --routing false --standalone false`
  - `npm install bootstrap@3`
    - install bootstrap 3 locally for the project
  - Place the styles in the angular.json file

```json
"styles": [
"src/styles.css",
"node_modules/bootstrap/dist/css/bootstrap.min.css"
]
```

# Debugging
  - chrome dev tools

## Sourcemaps
  - are files that provide a mapping between the source code of your application (typically written in TypeScript or other high-level languages) and the transpiled or minified code that the browser actually executes (JavaScript). 
  - They are essential for debugging and understanding issues in your application, especially when using build tools like Angular CLI or Webpack that transpile and bundle your code.
  - Angular CLI, for instance, automatically generates sourcemaps during the build process. 
  - You can enable or disable sourcemap generation in the angular.json configuration file. By default, they are generated for development builds and excluded from production builds to save space.


# Creating our Dropdown directive
  - We will make our dropdown directive such that it will attach the class **open** when it is clicked and remove when it is clicked again

> **@HostBinding('class.open')** bind to the class **open** on the element this directive is placed on, meaning when it is true it will be on the element and when it is falsed it will be taken off of the element
{: .prompt-info }

> **@HostListener('click')** will execute the the method when the click event is present on the element this directive is placed on 
{: .prompt-info }

```typescript
import { Directive, HostBinding, HostListener } from '@angular/core';

@Directive({
  selector: '[appDropdown]'
})
export class DropdownDirective {
  @HostBinding('class.open')
  isOpen: boolean = false;

  @HostListener('click')
  toggleOpen() {
    this.isOpen = !this.isOpen;
  }

}
```

```html
<div class="btn-group" appDropdown>
```