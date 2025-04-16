---
layout: post
title: 'Udemy Spring boot course: Section 6 Spring MVC'
date: 2023-10-05 15:25 -0500
categories: [Udemy, Java, Springboot, Spring MVC ]
tags: [Java, Programming, Udemy, Spring] 
image: 
  path: /2023-10-05-udemy-spring-boot-course-section-6-spring-mvc/profile.png
---
- [Git](#git)
- [Thymeleaf](#thymeleaf)
  - [Project structure](#project-structure)
  - [Thymeleaf template (boilerplate)](#thymeleaf-template-boilerplate)
  - [Demo App](#demo-app)
  - [CSS and Thymeleaf](#css-and-thymeleaf)
- [MVC Architecture](#mvc-architecture)
- [Sending/Receiving form with query parameters example](#sendingreceiving-form-with-query-parameters-example)
- [Adding Data to the model](#adding-data-to-the-model)
  - [Binding request parameters with @RequestParam](#binding-request-parameters-with-requestparam)
- [A little more about @RequestMapping(), @GetMapping, @PostMapping](#a-little-more-about-requestmapping-getmapping-postmapping)
  - [How spring sends data depending on what method is sent](#how-spring-sends-data-depending-on-what-method-is-sent)
- [Binding Java object to View](#binding-java-object-to-view)
- [Select with thymeleaf](#select-with-thymeleaf)
- [Injecting properties file @Value into controller and using that in the student form](#injecting-properties-file-value-into-controller-and-using-that-in-the-student-form)
- [Radio buttons](#radio-buttons)
- [Validation](#validation)
  - [Valiation Annotations](#valiation-annotations)
  - [Basic Form Validation example](#basic-form-validation-example)
  - [@InitBinder removes whitespace](#initbinder-removes-whitespace)
  - [Failed to convert property value of type java.lang.String to required type int for property freePasses; For input string: ""](#failed-to-convert-property-value-of-type-javalangstring-to-required-type-int-for-property-freepasses-for-input-string-)
  - [Custom Error messages](#custom-error-messages)
    - [How to get custom error codes](#how-to-get-custom-error-codes)
  - [Creating Custom validation rule](#creating-custom-validation-rule)

# Git
  - [Git repo](https://github.com/TrestenPool/SpringTutorial/tree/main/Section6)

# Thymeleaf
  - java templating engine
  - need to add thymeleaf to the pom.xml
  - Looping and conditionals
  - CSS and js integration
  - template layouts and fragments

## Project structure
  - Thymeleaf template files go in
    - **src/main/resources/templates**
  - for web apps, have .html extension

## Thymeleaf template (boilerplate)
  - thymeleaf expression is between the <p>
  - ![alt-text](/2023-10-05-udemy-spring-boot-course-section-6-spring-mvc/steps.png)
    - theDate is passed from the controller by the model

```text
<!DOCTYPE HTML>
<html xmlns:th="http://www.thymeleaf.org>
  <head> ... </head>

  <body>
    <p th:text="'Time on the server is ' + ${theDate}" />
  </body>

</html>
```

## Demo App

```java
// has to be @Controller and not @RestController !!!
@Controller
public class DemoController {

    @GetMapping("/hello")
    public String hello(Model model){

        // add an attribute that can be referenced in the view
        model.addAttribute(
                "theDate",
                new java.util.Date()
        );

        // looks for src/main/resources/templates/helloworld.html
        return "helloworld";
    }
}
```
{: file='DemoController.java'}

```text
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>Thymeleaf Demo</title>
</head>

<body>
    <p th:text="'Time on the server is ' + ${theDate}" />
</body>

</html>
```
{: file='helloworld.html'}

## CSS and Thymeleaf
  - spring boot will look for static resources in the directory
    - **src/main/resources/static**
  - we can have any folder/file name under static 
  - CSS is referenced in the html with

```html
<link rel="stylesheet" th:href="@{/css/demo.css}" />
```
  - Spring boot will search the following directories for static resources
    - /src/main/resources
    - /META-INF/resources
    - /resources
    - /static
    - /public


# MVC Architecture
  - [mvc docs](https://www.tutorialspoint.com/spring/spring_web_mvc_framework.htm)
  - ![alt-text](/2023-10-05-udemy-spring-boot-course-section-6-spring-mvc/mvc_fonrt_controller.png)
  - ![alt-text](/2023-10-05-udemy-spring-boot-course-section-6-spring-mvc/dispatcher_servlet.png)

# Sending/Receiving form with query parameters example

Controller class
```java
@Controller
public class HelloWorldController {

    // show the form
    @RequestMapping(value = "/show", method = RequestMethod.GET)
    public String showForm(){
        return "helloworld-form";
    }

    // process the form
    @RequestMapping("/processForm")
    public String processForm(){
        return "helloworld";
    }

}
```

/show form
```html
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>Hello World - Input Form</title>
</head>

<body>

    <form th:action="@{/processForm}" method="GET" >
        <input type="text" name="studentName"
               placeholder="What's your name?" />

        <input type="submit"/>
    </form>

</body>

</html>
```

/processForm 
```html
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>Thymeleaf Demo</title>
</head>

<body>
    Student with name: 
    <p th:text="${param.studentName}"></p>
</body>

</html>
```


# Adding Data to the model
  - Simple demo showing controller method taking the query parameter and constructing a message to append to the model before it is passed to the view

```java
@RequestMapping("/processFormTwo")
public String processFormTwo(HttpServletRequest request, Model model){
    // get thename from the  query parameters
    String name = request.getParameter("studentName");

    // convert name to upper case
    name = name.toUpperCase();

    // construct the message
    String message = String.format("HELLO %s, IT IS VERY NICE TO MEET YOU!!!", name);

    // add the attribute to the model
    model.addAttribute("message", message);

    // return the form
    return "processForm-2";
}
```

```html
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>Thymeleaf Demo</title>
</head>

<body>
    <p th:text="${message}"></p>
</body>

</html>
```

## Binding request parameters with @RequestParam
  - We can instead us @RequestParam instead of the above `request.getParameter("param_name")`
  - This will do the exact same as above except it is binded by spring and less effort on our side
    - `public String processFormThree(@RequestParam("studentName"), String name, Model model)`

```java
@RequestMapping("/processFormThree")
public String processFormThree(@RequestParam("studentName") String name, Model model){
    name = name.toUpperCase();
    String message = String.format("HELLO %s, IT IS NICE TO FINALLY MEET YOU", name);
    model.addAttribute("message", message);
    return "processForm-2";
}
```

# A little more about @RequestMapping(), @GetMapping, @PostMapping
  - when you use `@RequestMapping("/path")` above a method it will accept any http method by default
    - if you wanted to make it so only Get requests are allowed you could do this
    - `@RequestMapping(value = "/path", method = RequestMethod.GET)`
  - or you can just use `@GetMapping("/path")` instead of having to supply the second parameter
  - same goest for @PostMapping, @PutMapping etc...

## How spring sends data depending on what method is sent
  - We have the following code in the form

```html
<form th:action="@{/processFormThree}" method="GET" >

    <input type="text" name="studentName"
            placeholder="What's your name?" />

    <input type="submit"/>

</form>
```

here is our method signature for the endpoint
```java
@GetMapping("/processFormThree")
public String processFormThree(@RequestParam("studentName") String name, Model model){
```

If we hit /show then type in Briana and hit Submit, we will do a GET request to `http://localhost:3000/processFormThree?studentName=Briana`
  - The form data will be sent as Query parameters

however if we change the form to send as POST
```html
<form th:action="@{/processFormThree}" method="POST" >
```
 and change @GetMapping to @PostMapping, we will send a POST request to `http://localhost:3000/processFormThree` with no query parameters and the form data being sent as **Request Body**

# Binding Java object to View
  - In the spring controller
    - you must add the model attribute before showing the form
    - this is a bean that will hold form data for the data binding

  - ![alt-text](/2023-10-05-udemy-spring-boot-course-section-6-spring-mvc/object_binding.png)
    - the name must match in the controller and in the view
    - `*{...} is shortcut syntax for ${student.firstName}`
    - when the form is loaded, spring mvc will read student from the model then call the getter methods()


Controller method code
```java
@GetMapping("/studentForm")
public String studentForm(Model model){
    // create student object
    Student student = new Student();

    // set the properties student ojbect
    student.setFirstName("Tresten");
    student.setLastName("Pool");

    // add the student to the attributes
    model.addAttribute("student", student);

    // render the form
    return "Student/student-form";
}

@PostMapping("/processStudentForm")
public String processStudentForm(@ModelAttribute("student") Student student){
    // log the output
    System.out.printf("Student\nfirstName: %s\nlastName: %s\n", student.getFirstName(), student.getLastName());

    // return the view
    return "Student/student-results";
}
```

Field valus are binding with **th:field="*{fieldName}"**
```html
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>Hello World - Input Form</title>
</head>

<body>
    <h3>Student Registration Form</h3>
    <form th:action="@{/processStudentForm}" method="POST" th:object="${student}">
        First name: <input type="text" th:field="*{firstName}" />
        Last name: <input type="text" th:field="*{lastName}" />

        <br><br>
        <input type="submit" value="Submit">
    </form>
</body>

</html>
```

just displaying the results
```html
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>Student processing page</title>
</head>

<body>
<h3>Student Processing page</h3>
<h4>Student</h4>
First name:  <span th:text="${student.firstName}"></span>
<br>
Last name:  <span th:text="${student.lastName}"></span>

</body>

```

th:field
  - calls the getter methods when displaying the object
  - calls the setter methods if used in form to send a post request, it will use the setter methods to change the values of what is in the text field

@ModelAttibute()
  - used to get the object from the  form

# Select with thymeleaf
  - ![alt-text](/2023-10-05-udemy-spring-boot-course-section-6-spring-mvc/select_thy.png)

```html
<form th:action="@{/processStudentForm}" method="POST" th:object="${student}">
    First name: <input type="text" th:field="*{firstName}" />
    Last name: <input type="text" th:field="*{lastName}" />
    <br>
    <select th:field="*{country}">
        <option th:value="Brazil">Brazil</option>
        <option th:value="France">France</option>
        <option th:value="India">India</option>
        <option th:value="Germany">Germany</option>
    </select>

    <br><br>
    <input type="submit" value="Submit">
</form>
```

# Injecting properties file @Value into controller and using that in the student form
  - Example below injecting the countries property into the controller then using that in the html file looping over all of the countries

```properties
countries=Brazil,France,United States,India,Romania
```

```java
@Controller
public class StudentController {
    @Value("${countries}")
    private List<String> countries;

@GetMapping("/studentForm")
public String studentForm(Model model){
    // create student object
    Student student = new Student();

    // add the student to the attributes
    model.addAttribute("student", student);

    // ADD THE COUNTRIES TO THE MODEL
    model.addAttribute("countries", countries);

    // render the form
    return "Student/student-form";
}
```

Loops through all of the country with **th:field** and **th:each**
```html
<body>
    <h3>Student Registration Form</h3>
    <form th:action="@{/processStudentForm}" method="POST" th:object="${student}">
        First name: <input type="text" th:field="*{firstName}" />
        Last name: <input type="text" th:field="*{lastName}" />
        <br>

        <select th:field="*{country}">
            <option th:each="tempCountry : ${countries}" th:value="${tempCountry}" th:text="${tempCountry}"></option>
        </select>

        <br><br>
        <input type="submit" value="Submit">
    </form>
</body>

```

# Radio buttons

```html
<input type="radio"
        th:each="language : ${languages}"
        th:value="${language}"
        th:text="${language}"
        th:field="*{favoriteLanguage}"
        th:checked="${language} == *{favoriteLanguage}">
```

```java
@Controller
public class StudentController {
    @Value("${countries}")
    private List<String> countries;

    @Value("${languages}")
    private List<String> languages;

    @GetMapping("/studentForm")
    public String studentForm(Model model){
        // create student object
        Student student = new Student();

        // set the properties student ojbect
        student.setFirstName("Tresten");
        student.setLastName("Pool");
        student.setFavoriteLanguage("Zig");

        // add the student to the attributes
        model.addAttribute("student", student);

        // add the countries to the model
        model.addAttribute("countries", countries);

        // add the languages to the model
        model.addAttribute("languages", languages);

        // render the form
        return "Student/student-form";
    }
```

# Validation
  - Java has a standard Bean Validation API
  - [validation example](https://spring.io/guides/gs/validating-form-input/)
  - [alt-text](http://www.beanvalidaton.org)


## Valiation Annotations
  - below is a table of some of the most common validation annotations

| Annotation      | Contact                                   |
| :-------------- | :---------------------------------------- |
| @NotNull        | Value cannot be null                      |
| @Min            | Must be num >= value                      |
| @Max            | Must be num <= value                      |
| @Size           | Size must match given size                |
| @Pattern        | Must match a regular expression pattern   |
| @Future / @Past | Date must be in future or past given date |

## Basic Form Validation example
  - ![alt-text](/2023-10-05-udemy-spring-boot-course-section-6-spring-mvc/validation_diagram.png)

Customer class
  - here we use some annotations that will be used for validations later
```java
public class Customer {
    @NotNull(message = "is required")
    @NotBlank(message = "cannot be blank")
    private String firstName;

    @NotNull(message = "is required")
    @NotBlank(message = "cannot be blank")
    private String lastName;

    // constructors

    // getters and setters
}
```

Customer controller methods
  - showForm method()
    - Adds a new customer object to the model and passes it to the view
  - processForm method()
    - uses **@Valid** to validate the request body that came in to make sure it passes all of the validation annotations we set in the Customer class
    - **BindingResult** holds the results of the validations
    - checks if .hasErrors() is true then passes goes back to the show form page
    - else it will let it pass to the processed page
```java
    @GetMapping("/")
    public String showForm(Model model){
        // create the customer and give to the model to render on the view
        model.addAttribute("customer", new Customer());

        // render the form
        return "customer/form";
    }

    @PostMapping("/processForm")
    public String processForm(
            // tells Spring MVC to perform validation
            @Valid @ModelAttribute("customer") Customer customer,
            // holds the results of the validation
            BindingResult bindingResult
    ){

        // return back to form
        if(bindingResult.hasErrors()){
            return "customer/form";
        }
        // go to the processed form
        else{
            return "customer/processed";
        }

    }
```

Show form
  - th:action="@{/processedForm}"
    - where the form will go to 
  - th:object="@{customer}"
    - the variable of the object that the model passed in
  - **th:if="${#fields.hasErrors('lastName')}**
    - checks if the fields object has an errors for lastname
    - fields is an object that is created by the Validator in springboot automatically
  - **th:error="*{lastName}"**
    - prints out the errors that the validator has for lastName

```html
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>Customer Form</title>
    <style>
        .error{
            color: red;
        }
    </style>
</head>

<body>
    <i>Fill out the form. Asterisk (*) means required.</i>
    <br><br>

    <form th:action="@{/processForm}" th:object="${customer}" method="POST">
        First name: <input type="text" th:field="*{firstName}">

        <br><br>

        Last name (*): <input type="text" th:field="*{lastName}">

        <!-- Add Error message if present -->
        <span th:if="${#fields.hasErrors('lastName')}"
              th:errors="*{lastName}"
              class="error">
        </span>

        <br><br>

        <input type="submit" value="Submit">

    </form>

</body>

</html>
```

## @InitBinder removes whitespace
  - works as a **pre-processor**
  - pre-processes each web request to the controller
  
@InitBinder method in the controller
  - **WebDataBinder** as an argument
  - .**registerCustomEditor**(String.class, stringTrimmerEditor) to maniupulate all Strings coming in from requests
```java
    @InitBinder
    public void initBinder(WebDataBinder webDataBinder){
        System.out.println("in initbinder");

        // creating the string trimmer
        StringTrimmerEditor stringTrimmerEditor = new StringTrimmerEditor(true);

        // saying that for all Strings that come in, register the stringtrimmereditor to be ran on it
        webDataBinder.registerCustomEditor(String.class, stringTrimmerEditor);
    }
```


## Failed to convert property value of type java.lang.String to required type int for property freePasses; For input string: ""
  - Trying to make an integer required
  - We are getting this because it is trying to convert an int to a string to trim all of the whitespace that we had configured in the @InitBinder
  - To fix we can make it an Integer instead of an int and that will be able to be converted to a String with the .toString()
  
I have the following code in the model where I define an integer with the following annotations

```java
    @Range(min = 0, max = 10, message = "Must be between 0 and 10")
    @NotNull(message = "free passes is required")
    private int freePasses;
```

  - I am getting the following error after trying to submit
  - it is trying to convert a String --> int
  - ![alt-text](/2023-10-05-udemy-spring-boot-course-section-6-spring-mvc/error.png)

Fix
  - This can be fixxed by using the **Integer** class instead of primitive **int**

## Custom Error messages
  - filename and location has to be ---> **src/main/resources/messages.properties**

```properties
# format explained below vvv
# error type . spring model attribute name . field name . our custom error message
typeMismatch.customer.freePasses=Invalid number
```

HTML file
  - in the html file you can just reference errors like normal

```html
<!-- Free passes errors -->
<span th:if="${#fields.hasErrors('freePasses')}"
      th:errors="*{freePasses}"
      class="error">
</span>
```


### How to get custom error codes
  - How do I know what the error code is like in the previous example **typeMismatch.customer.freePasses=Invalid number**
  - We can get it by printing the BindingResult to the console then using that in the messages.properties file
  - Once we get the error message we can put it in our messages.properties file for the custom error message
  - `System.out.println("Binding result: " + bindingResult.toString());`
  - ![alt-text](/2023-10-05-udemy-spring-boot-course-section-6-spring-mvc/custom_error_message.png)

## Creating Custom validation rule
  - ![alt-text](/2023-10-05-udemy-spring-boot-course-section-6-spring-mvc/custom_validation.png)
    - we want a custom validation to make sure the course code starts with LUV 
  
Steps 1. Create the custom annotation
  - comments in the code below describe what each peice is used for

```java
// tells the annotation what class that is going to validate this annotation
@Constraint(validatedBy = CourseCodeConstraintValidator.class)
// tells the jvm what the annotation can be used for
@Target({ElementType.FIELD, ElementType.METHOD})
// The retention policy determines how long the annotated annotation should be retained or available in the compiled class files and at runtime.
@Retention(RetentionPolicy.RUNTIME)
// it indicates that this annotation should be included in the generated Javadoc and other documentation tools.
@Documented()
public @interface CourseCode {
    // default course code
    String value() default "LUV";

    // default error message
    String message() default "must start with LUV";

    // define default groups
    Class<?>[alt-text] groups() default {} ;

    // define default payloads
    // payloads provide custom details about the validation failure(security level, error code, etc..)
    Class<? extends Payload>[alt-text] payload() default {};
}
```

Step 2: Create the Validator Class
  - must implement ConstraintValidator
    - <Annotation, Type that we will check against>
  
  - Has 2 methods we need to override
    - initialize()
      - initializes at runtime
    - isValid()
      - checks to see if the code passed in is the same as our prefix that was set


```java
// <Annotation class, variable that we will use in the isValid method()
public class CourseCodeConstraintValidator implements ConstraintValidator<CourseCode, String> {
    // assign this when the annotation is initialized
    private String coursePrefix;

    @Override
    public void initialize(CourseCode courseCode) {
        coursePrefix = courseCode.value();
    }

    @Override
    public boolean isValid(String codeToCheck, ConstraintValidatorContext constraintValidatorContext) {
        // return true if no value was supplied
        if(codeToCheck == null){
            return true;
        }

        // return true if the code supplied starts with the course prefix, false otherwise
        return codeToCheck.startsWith(coursePrefix);
    }

}
```

Example:

Student class
```java
    @CourseCode(value = "UTSA", message = "must start with UTSA")
    private String courseCode;
```

  - ![alt-text](/2023-10-05-udemy-spring-boot-course-section-6-spring-mvc/utsa_example.png)
