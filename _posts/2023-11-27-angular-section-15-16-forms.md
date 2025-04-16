---
layout: post
title: Angular Section 15,16 Forms
date: 2023-11-27 16:26 -0600
categories: [Angular, Udemy]
image: 
  path: /2023-11-27-angular-section-15-16-forms/profile.png
---

- [Forms](#forms)
- [Approaches](#approaches)
  - [Template Driven](#template-driven)
    - [Submitting the form 1](#submitting-the-form-1)
    - [Submitting form 2](#submitting-form-2)
    - [Validation](#validation)
    - [Grouping Controls](#grouping-controls)
    - [Setting and updating values in your form](#setting-and-updating-values-in-your-form)
    - [Resetting Forms](#resetting-forms)
  - [Reactive Forms](#reactive-forms)
    - [Validation](#validation-1)
    - [Grouping Controls](#grouping-controls-1)
    - [Reactive arrays of form controls](#reactive-arrays-of-form-controls)
    - [Custom Validator](#custom-validator)
    - [Asynchronous Validators](#asynchronous-validators)
    - [Reacting to status or value changes](#reacting-to-status-or-value-changes)


# Forms
  - we we need a module for forms
  - when we submit a form it doesn't get sent to the server because it is a SPA remember.

# Approaches
  - There are 2 approaches when it comes to forms in angular

| Approach        | Description                                                    |
| :-------------- | :------------------------------------------------------------- |
| Template-Driven | Angular infers the Form Object of the DOM                      |
| Reactive        | Form is created programmatically and synchronized with the DOM |

Reactive
  - Provide direct, explicit access to the underlying form's object model. Compared to template-driven forms, they are more robust: they're more scalable, reusable, and testable. If forms are a key part of your application, or you're 

Template Driven 
  - Rely on directives in the template to create and manipulate the underlying object model. They are useful for adding a simple form to an app, such as an email list signup form. They're straightforward to add to an app, but they don't scale as well as reactive forms. If you have very basic form requirements and logic that can be managed solely in the template, template-driven forms could be a good fit.

## Template Driven
  - Make sure **FormsModule** is in the imports in app module
  - angular will automatically detect any forms element in your html files and place its javascript in there
  - angular will **not** however detect your inputs

### Submitting the form 1
  - use **ngModel** to tell angular to recognize as input
  - use **(ngSubmit)="onSubmit(form)"** to tell angular what method you want executed when the form is submitted
  - **#form="ngform"** tells angular to treat the form as an angular object to get passed to ngsubmit method

```html
<form
  (ngSubmit)="onSubmit(form)"
  #form="ngForm">
  <!-- gets access to the form angular creates for us -->

  <div id="user-data">

    <!-- username -->
    <div class="form-group">
      <label for="username">Username</label>
      <input 
      type="text" 
      id="username" 
      class="form-control"
      ngModel
      name="username"
      #username
      >
    </div>

    <!-- username -->
    <button 
      class="btn btn-default" 
      type="button"
      (click)="suggestUserName()"
      >Suggest an Username</button>

    <!-- email -->
    <div class="form-group">
      <label for="email">Mail</label>
      <input 
        type="email" 
        id="email" 
        class="form-control"
        ngModel
        name="email">
    </div>

  </div>

  <div class="form-group">
    <!-- secret questions -->
    <label for="secret">Secret Questions</label>

    <!-- options -->
    <select 
      id="secret" 
      class="form-control"
      ngModel
      name="secret">
      <option value="pet">Your first Pet?</option>
      <option value="teacher">Your first teacher?</option>
    </select>
  </div>

  <!-- submit button -->
  <button class="btn btn-primary" type="submit">Submit</button>
</form>
```

```typescript
@Component({
  // ..
})
export class AppComponent {
  @ViewChild('username') username: ElementRef;

  suggestUserName() {
    const suggestedName = 'Superuser';
    this.username.nativeElement.value = suggestedName;
  }

  onSubmit(form: NgForm){
    console.log(`submitted`);
    console.log(form);
  }

}
```

### Submitting form 2
  - there is another way to submit a form and look at the contents before it even gets submitted


> Notice how we are no longer passing form to the onSubmit() method
{: .prompt-tip }

```html
<form
  (ngSubmit)="onSubmit()"
  #form="ngForm">

  <div id="user-data">

    <!-- username -->
    <div class="form-group">
      <label for="username">Username</label>
      <input 
      type="text" 
      id="username" 
      class="form-control"
      ngModel
      name="username"
      #username
      >
    </div>

    <!-- username -->
    <button 
      class="btn btn-default" 
      type="button"
      (click)="suggestUserName()"
      >Suggest an Username</button>

    <!-- email -->
    <div class="form-group">
      <label for="email">Mail</label>
      <input 
        type="email" 
        id="email" 
        class="form-control"
        ngModel
        name="email">
    </div>

  </div>

  <div class="form-group">
    <!-- secret questions -->
    <label for="secret">Secret Questions</label>

    <!-- options -->
    <select 
      id="secret" 
      class="form-control"
      ngModel
      name="secret">
      <option value="pet">Your first Pet?</option>
      <option value="teacher">Your first teacher?</option>
    </select>
  </div>

  <!-- submit button -->
  <button class="btn btn-primary" type="submit">Submit</button>
</form>
```

```typescript
@Component({
  // ..
})
export class AppComponent {
  @ViewChild('username') username: ElementRef;

  // gets access to the form by local reference name
  @ViewChild('form')
  signupform: NgForm;

  suggestUserName() {
    const suggestedName = 'Superuser';
    this.username.nativeElement.value = suggestedName;
  }

  // onSubmit(form: NgForm){
  //   console.log(`submitted`);
  //   console.log(form);
  // }

  // here we can see the contents of the ngform
  onSubmit(){
    console.log(this.signupform);
  }

}
```

### Validation
  - To add validation to a template-driven form, you add the same validation attributes as you would with native HTML form validation. Angular uses directives to match these attributes with validator functions in the framework.
  - Every time the value of a form control changes, Angular runs validation and generates either a list of validation errors that results in an INVALID status, or null, which results in a VALID status.
  - angular will dynamically add classes to an input of it is valid or not depending on the validators you have put on it 

Built in validators in angular
  - [build in validators](https://angular.io/api/forms/Validators)

Directives for the built in validators, just search for validators on the page
  - [directives](https://angular.io/api?type=directive)


> `#username="ngModel"` will tell angular connect this local reference to the ngModel created by angular so you can use it in the typescript code
> `*ngIf=!username.valid` will only show the message if the username is not valid
{: .prompt-tip }

```html
<div class="form-group">
  <label for="username">Username</label>
  <input 
  type="text" 
  id="username" 
  class="form-control"
  ngModel
  name="username"
  #username="ngModel"
  required
  >
  <span 
    *ngIf="!username.valid"
    class="help-block"
    >Please enter a valid username</span>
</div>
```

```typescript
export class AppComponent {
  @ViewChild('username') 
  username: NgModel;

  // our form
  @ViewChild('form')
  signupform: NgForm;

  onSubmit(){
    console.log(this.signupform);
  }
```

### Grouping Controls
  - we want to group the username, email fields in a form
  - we can do that with ngModelGroup

> `ngModelGroup="userData"` tells angular to group the following form group together
> anything can go where **userData** is, that is just a name to reference to in the typescript code for the component
{: .prompt-tip }

```html
<div 
  #ngModel="ngModelGroup"
  id="user-data" 
  ngModelGroup="userData">

  <!-- username -->
  <div class="form-group">
    <label for="username">Username</label>
    <input 
    type="text" 
    id="username" 
    class="form-control"
    ngModel
    name="username"
    #username="ngModel"
    required
    >
    <span 
      *ngIf="!username.valid"
      class="help-block"
      >Please enter a valid username</span>
  </div>

  <!-- username generate button -->
  <button 
    class="btn btn-default" 
    type="button"
    (click)="suggestUserName()"
    >Suggest an Username</button>

  <!-- email -->
  <div class="form-group">
    <label for="email">Mail</label>
    <input 
      type="email" 
      id="email" 
      class="form-control"
      ngModel
      name="email"
      required
      email
      #email="ngModel">
    <span 
      *ngIf="!email.valid"
      class="help-block"
      >Please enter a valid email</span>
  </div>
</div>
```
  - ![alt-text](/2023-11-27-angular-section-15-16-forms/userdata.png)


### Setting and updating values in your form
  Use setValue() when setting the value for a form
  use patchValue() when updating a control for a form


```typescript
  onSetDefaults(){
    this.signupform.form.setValue({
      userData:{
        username: 'sudo',
        email: "sudo@gmail.com"
      },
      secret: 'pet',
      gender: 'male',
      questionAnswer: 'Bingo'
    })
  }

  suggestUserName() {
    const suggestedUsername = 'Sudo';
    this.signupform.form.patchValue({
      userData: {
        username: suggestedUsername
      }
    })
  }

```

### Resetting Forms
  - say we have submitted the form and not want to reset the form we can do it like the following
  - there is a .reset() method on the NgForm property

```html
<form
  (ngSubmit)="submit()"
  #form="ngForm">
  <!-- form controls ... -->
</form>
```

```typescript
export class AppComponent {
  // form
  @ViewChild('form') 
  signupform: NgForm;

  submit(){
    // do stuff ..
    // reset form
    this.signupform.reset();
  }
}


```

## Reactive Forms
  - Form is created programmatically and synchronized with the DOM

The **ReactiveFormsModule** is required not the **FormsModule** for Reactive forms
```typescript
@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule,
    ReactiveFormsModule
    // FormsModule,
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```
{: file='app.module.ts'}

```typescript
@Component({
  // ..
})
export class AppComponent implements OnInit{
  genders = ['male', 'female'];
  signupForm: FormGroup;

  ngOnInit(): void {
    this.signupForm = new FormGroup({
      'username': new FormControl(null),
      'email': new FormControl('user@gmail.com'),
      'gender': new FormControl('male')
    });
  }

  onSubmit(){
    console.log(this.signupForm);
  }
}
```
{: file='app.component.ts'}


> use **formControlName=variableNameInComponent** to connect to the variable in the component
{: .prompt-tip }

```html
<!-- FORM -->
<form
  [formGroup]="signupForm"
  (ngSubmit)="onSubmit()"
  >

  <!-- username -->
  <div class="form-group">
    <label for="username">Username</label>
    <input
      formControlName="username"
      type="text"
      id="username"
      class="form-control">
  </div>

  <!-- email -->
  <div class="form-group">
    <label for="email">email</label>
    <input
      formControlName="email"
      type="text"
      id="email"
      class="form-control">
  </div>

  <!-- genders -->
  <div class="radio" *ngFor="let gender of genders">
    <label>
      <input
        formControlName="gender"
        type="radio"
        [value]="gender">{{ gender }}
    </label>
  </div>

  <!-- submit button -->
  <button 
    class="btn btn-primary" 
    type="submit"
    >Submit</button>
</form>
```
{: file='app.component.html'}

### Validation
Steps
  - add Validation to the FormControl object

```typescript
this.signupForm = new FormGroup({
  // adding a single Validators method
  'username': new FormControl(null, Validators.required),
  // adding an array of Validator methods to be checked
  'email': new FormControl('user@gmail.com', [Validators.required, Validators.email]),
  'gender': new FormControl('male')
});
```
{: file='app.component.ts'}

```html
<!-- email -->
<div class="form-group">
  <label for="email">email</label>
  <input
    formControlName="email"
    type="text"
    id="email"
    class="form-control"
    [ngClass]="{invalid: signupForm.get('email').touched && signupForm.get('email').errors}"
    >
  <span
    *ngIf="signupForm.get('email').touched && signupForm.get('email').errors"
    class="help-block">Please enter a valid email address
  </span>
</div>
```
{: file='app.component.html'}

Or just do this in the css file.
Since angular applies classes dynamically this will apply the border automatically without having to do anything special in the html
```css
input.ng-invalid.ng-touched{
  border: 2px solid red;
}
```

### Grouping Controls
  - we may want to group our controls like
    - userinput
      - username
      - password
  - and to access we would use something like userinput.username or userinput.password
  - to group controls all you have to do is nest a FormGroup inside another FormGroup and give it it's own formcontrols

```typescript
ngOnInit(): void {
  // initialize the form
  this.signupForm = new FormGroup({

    // nested form group
    'userData': new FormGroup({
      'username': new FormControl(null, Validators.required),
      'email': new FormControl('user@gmail.com', [Validators.required, Validators.email]),
    }),

    'gender': new FormControl('male')
  });
}
```

> **formGroupName="nestedFormGroupName"** is placed in an outer div with the username & email formcontrol placed inside of it
{: .prompt-tip }

> **formControlName** is used for the name inside the nested formgroup
{: .prompt-tip }

> **signupForm.get('userData.username')** dot notation is used to get access to the nested formgroup controls like this 
{: .prompt-tip }

```html
<!-- nested form group controls -->
<div 
  class="form-group"
  formGroupName="userData"
  >

  <!-- username -->
  <div class="form-group">
    <label for="username">Username</label>
    <input
      formControlName="username"
      type="text"
      id="username"
      class="form-control"
    >

    <span
      *ngIf="signupForm.get('userData.username').touched && signupForm.get('userData.username').errors"
      class="help-block">Please enter in a username
    </span>
  </div>

  <!-- email -->
  <div class="form-group">
    <label for="email">email</label>
    <input
      formControlName="email"
      type="text"
      id="email"
      class="form-control"
      [ngClass]="{invalid: signupForm.get('userData.email').touched && signupForm.get('userData.email').errors}"
      >
      <span
        *ngIf="signupForm.get('userData.email').touched && signupForm.get('userData.email').errors"
        class="help-block">Please enter a valid email address
      </span>
  </div>
</div>
```

### Reactive arrays of form controls
  - using an array in a form

Here is our form
> note: **'hobbies': new FormArray([])** we are just setting to an empty array startup
{: .prompt-tip }

```typescript
ngOnInit(): void {
  // initialize the form
  this.signupForm = new FormGroup({

    // nested form group
    'userData': new FormGroup({
      'username': new FormControl(null, Validators.required),
      'email': new FormControl('user@gmail.com', [Validators.required, Validators.email]),
    }),
    'gender': new FormControl('male'),
    'hobbies': new FormArray([])
  });
}

onAddHobby(){
  // add a new hobby input
  const newControl = new FormControl(null, Validators.required);
  (<FormArray>this.signupForm.get('hobbies')).push(newControl);
}

getControls(){
  // return the controls for the hobbies formArray
  return (<FormArray>this.signupForm.get('hobbies')).controls;
}
```

![alt-text](/2023-11-27-angular-section-15-16-forms/hobbies.png)
  - here we have a button that when you click on it, it will add another form control which is just a text box

```html
<!-- hobbies -->
<div
  formArrayName="hobbies"
  >
  <h4>Your Hobbies</h4>
  <button 
    class="btn btn-default"
    type="button" 
    (click)="onAddHobby()">Add Hobby</button>
  <div 
    class="form-group"
    *ngFor="let control of getControls(); let i = index">
    <input 
      type="text" 
      class="form-control" 
      [formControlName]="i">
  </div>
</div>
<!-- hobbies -->
```

Heres what it looks like when we add a couple of inputs and submit the form
  - ![alt-text](/2023-11-27-angular-section-15-16-forms/hobbies1.png)


### Custom Validator
  - we want to create a custom validator that prevents the user from using some usernames
  - we don't want the user to enter in the names **Chris** or **Anna**

> we have to use **this.forbiddenNames.bind(this)** because otherwise **this** will refer to another object and not the current class we are calling it from
{: .prompt-tip }

```typescript
export class AppComponent implements OnInit{

  genders = ['male', 'female'];
  signupForm: FormGroup;
  forbiddenUsernames = ['Chris', 'Anna']

  ngOnInit(): void {
    // initialize the form
    this.signupForm = new FormGroup({
      // nested form group
      'userData': new FormGroup({
        'username': new FormControl(null, [Validators.required, this.forbiddenNames.bind(this)]),
        'email': new FormControl('user@gmail.com', [Validators.required, Validators.email]),
      }),
      'gender': new FormControl('male'),
      'hobbies': new FormArray([])
    });
  }

  // ...
  
  forbiddenNames(control: FormControl): {[s: string]: boolean}{
    // checks if the control value is in the list of forbidden names
    if(this.forbiddenUsernames.indexOf(control.value) !== -1) {
      return {'nameIsForbidden': true}
    }
    // returning null means success, there was no error found
    return null;
  }
```


> Note: we use .getError('errorname') to check if that error is present and show the error
{: .prompt-tip }

```html
<!-- username -->
<div class="form-group">
  <label for="username">Username</label>
  <input
    formControlName="username"
    type="text"
    id="username"
    class="form-control"
  >

  <!-- required -->
  <span
    *ngIf="signupForm.get('userData.username').touched && signupForm.get('userData.username').getError('required')"
    class="help-block">Please enter in a username
  </span>

  <!-- forbidden name -->
  <span
    *ngIf="signupForm.get('userData.username').getError('nameIsForbidden')"
    class="help-block">That is a invalid username
  </span>
</div>
```

### Asynchronous Validators
  - there are plenty of scenarios where we want our validators to be asynchronous

> Notice that **this.forbiddenEmails** is placed as the 3rd argument to FormControl(), this is where the asynchronous validators are palced
{: .prompt-tip }

> forbiddenEmails() is returning a promise that resolves after 1.5 seconds
{: .prompt-tip }

```typescript
export class AppComponent implements OnInit{
  genders = ['male', 'female'];
  signupForm: FormGroup;
  forbiddenUsernames = ['Chris', 'Anna']

  ngOnInit(): void {
    // initialize the form
    this.signupForm = new FormGroup({
      // nested form group
      'userData': new FormGroup({
        'username': new FormControl(null, [Validators.required, this.forbiddenNames.bind(this)]),
        'email': new FormControl('user@gmail.com', [Validators.required, Validators.email], this.forbiddenEmails),
      }),
      'gender': new FormControl('male'),
      'hobbies': new FormArray([])
    });
  }
  forbiddenEmails(control: FormControl): Promise<any> {
    // promise that resolves after 1.5 seconds
    const promise = new Promise<any>(
      (resolve, reject) => {
        setTimeout(() => {
          if(control.value === 'test@test.com'){
            resolve({'emailIsForbidden': true})
          }
          else{
            resolve(null);
          }
        }, 1500);
      }
    )

    return promise;
  }

}
```

It is handled the same way in the html code as before


### Reacting to status or value changes
  - There are 2 observables we can interact with on the entire form or a specific form control
    - .valueChanges() & .stateChanges()

```typescript
this.signupForm.valueChanges.subscribe(
(value) => {
  console.log(`value = `, value);
}
);

// or

this.signupForm.statusChanges.subscribe(
(status) => {
  console.log(`status = `, status);
}
)
```

Here is the output for valueChanges
  - ![alt-text](/2023-11-27-angular-section-15-16-forms/valueChange.png)

Here is the output for stateChanges
  - ![alt-text](/2023-11-27-angular-section-15-16-forms/stateChange.png)
  - you get pending if there is an asynchrous change waiting for approval