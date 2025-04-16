---
layout: post
title: 'Udemy Spring boot course: Section 2 Spring Core'
date: 2023-09-21 15:41 -0500
categories: [Udemy, Java, Spring, Core]
tags: [Java, Programming, Udemy, Spring] 
image: 
  path: /2023-09-21-udemy-spring-boot-course-section-2-spring-core/profile.png
---

- [Inversion of Control (IoC)](#inversion-of-control-ioc)
- [Dependency Injection](#dependency-injection)
  - [Types of Injection](#types-of-injection)
    - [Constructor Injection](#constructor-injection)
      - [Constructor injection example](#constructor-injection-example)
    - [Setter Injection](#setter-injection)
      - [Setter Injection example](#setter-injection-example)
    - [Field Injection](#field-injection)
  - [Spring Autowiring](#spring-autowiring)
    - [Types of Autowiring](#types-of-autowiring)
- [Spring Container](#spring-container)
  - [Configuration of the spring container](#configuration-of-the-spring-container)
- [@SpringBootApplication annotation](#springbootapplication-annotation)
  - [Component Scanning](#component-scanning)
    - [Specify explicitly](#specify-explicitly)
  - [@Qualifer](#qualifer)
  - [@Primary](#primary)
  - [Lazy Initialization @Lazy](#lazy-initialization-lazy)
    - [Global Configuration](#global-configuration)
  - [Bean Scope](#bean-scope)
    - [Specify Bean Scope @Scope](#specify-bean-scope-scope)
    - [Singleton](#singleton)
    - [Prototype](#prototype)
  - [Bean LifeCycle](#bean-lifecycle)
    - [@PostConstruct init()](#postconstruct-init)
    - [@PreDestroy destroy() method](#predestroy-destroy-method)
  - [Configure Beans with java code @Configuration \& @Bean](#configure-beans-with-java-code-configuration--bean)



# Inversion of Control (IoC)
  - the approach of outsourcing the construction and management of objects

Coding Scenario
  - ![alt-text](/2023-09-21-udemy-spring-boot-course-section-2-spring-core/coding_scenario.png)

Spring Solution
  - The app requests a coach object from spring
  - Spring will then use the **Object Factory** to return the reference to the correct object
  - Spring determines which object you need based on the **configuration** you set
  - ![alt-text](/2023-09-21-udemy-spring-boot-course-section-2-spring-core/spring_solution.png)

# Dependency Injection
  - Dependency  Inversion Principle - client delegates to another object the responsiblity of providing its dependencies

Car Factory Example
  - user says give me a car object
    - car factory assemblies the car and all its parts and components
    - once the car factory is finished it will return the user the car object
  - ![alt-text](/2023-09-21-udemy-spring-boot-course-section-2-spring-core/car_di_example.png)

Team example
  - The application requests a coach object
  - Spring object factory assemblies the correct object based on the configuration and returns the reference to the user 
  - ![alt-text](/2023-09-21-udemy-spring-boot-course-section-2-spring-core/di_example.png)

## Types of Injection
  - There are two types of injection
    - Constructor injection
    - Setter injection

### Constructor Injection
  - use this when you have **required dependencies**
  - recommended as first choice

#### Constructor injection example
  - ![alt-text](/2023-09-21-udemy-spring-boot-course-section-2-spring-core/example.png)
    - In this example we want the spring container to autowire a coach bean to our DemoController class

```java
public interface Coach{
  String getDailyWorkout();
}
```
{: file='Coach.java'}

```java
@Component
public class CricketCoach implements Coach{
  @Override
  public String getDailyWorkout() {
    return "Practice fast bowling for 15 minutes;
  }
}
```
{: file='CricketCoach.java'}


```java
@RestController
public class DemoController {
  private Coach mycoach;

  @Autowired
  public DemoController(Coach thecoach){
    this.mycoach = thecoach;
  }

  @GetMapping("/getworkout")
  public String getDailyWorkout(){
    return mycoach.getDailyWorkout();
  }
}
```
{: file='DemoController.java'}

  - **@Component** annotation marks the class as a **Spring Bean**
    - A spring bean is just a regular Java class that is **managed by Spring**
    - It also makes the class available for **Dependency Injection**
  
  - **@RestController** annoation tells spring this is a class that lists rest routes
  - **@AutoWired** annoation tells spring to infer the type and spring bean to be injected into the constructor when calling this restcontroller at creation
    - if you only have 1 constructor then @Autowired on constructor is optional


### Setter Injection
  - use this when you have **optional dependencies**
  - if dependency is not provided, your app can provide reasonable default logic

#### Setter Injection example
  - inject dependencies by calling setter methods on your POJO class
  - can have any setter method name, Spring will infer based on arguments and property being set on what bean to inject

```java
@RestController
public class Controller {
    private Coach mycoach;

    // SETTER INJECTION
    @Autowired
    public void setMycoach(Coach mycoach) {
        this.mycoach = mycoach;
    }

    @GetMapping("/")
    public String test(){
        return "Hello world";
    }

    @GetMapping("/getdailyworkout")
    public String getdailyWorkout(){
        return this.mycoach.getDailyWorkout();
    }
}

```

### Field Injection
  - There is a 3rd injection type that is not recommended
  - not popular like it used to be in the old days
  - reason why is because it makes it harder to unit test
  - inject beans into class properties even private ones
  - behind the scenes accomplishes this with java reflection.

```java
@RestController
public class Controller {
    @Autowired
    private Coach mycoach;

    // no need for constructor or setters

    @GetMapping("/")
    public String test(){
        return "Home route";
    }

    @GetMapping("/getdailyworkout")
    public String getdailyWorkout(){
        return this.mycoach.getDailyWorkout();
    }
}
```


## Spring Autowiring
  - simplifies the process of injecting dependencies into Spring beans (components or objects).
  - Dependency injection is a fundamental concept in Spring, and autowiring is one way to achieve it.
  - **Autowiring allows you to automatically inject the required dependencies into a Spring bean without explicitly specifying them in the configuration.**
  - Spring can automatically identify and inject the appropriate dependencies based on certain rules and annotations. 

### Types of Autowiring

| Type                                              |                                                                     Description                                                                      |
| :------------------------------------------------ | :--------------------------------------------------------------------------------------------------------------------------------------------------: |
| No Autowiring (Default)                           |    must explicitly specify the dependencies using <property> elements in XML configuration or @Autowired annotations in Java-based configuration.    |
| Autowire by Type (autowire="byType")              |    Spring automatically wires dependencies by matching their types. If there are multiple beans of the same type, Spring will raise an exception     |
| Autowire by Name (autowire="byName")              |                                              Spring automatically wires dependencies by matching their                                               |
| Autowire by Constructor (autowire="constructor"): |                                  Spring automatically wires dependencies by examining the constructor of the bean.                                   |
| Autowire by Qualifier (@Qualifier annotation):    | When you have multiple beans of the same type, you can use the @Qualifier annotation along with @Autowired to specify which bean should be injected. |





# Spring Container
Primary Functions
  - Create and manage objects (Inversion of control)
  - Injeft object dependencies (Dependency Injection)

## Configuration of the spring container

| Configuration Type | Relevance |
| :----------------- | :-------: |
| XML Configuration  |  Legacy   |
| Java Annotations   |  Modern   |
| Java Source Code   |  Modern   |

# @SpringBootApplication annotation
  - **@SpringBootApplication** enables the following by default
    - @EnableAutoConfiguration
    - @ComponentScan
    - @Configuration

```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class DependencyInjectionDemoApplication {
  SpringApplication.run(DependencyInjectionDemoApplication.class, args);
}
```

| Annotation               |                                    Description                                     |
| :----------------------- | :--------------------------------------------------------------------------------: |
| @EnableAutoConfiguration |                   Enables Springboots auto-configuration support                   |
| @ComponentScan           | Enables component scanning of current package. Also recursively scans sub-packages |
| @Configuration           |   Able to register extra beans with @Bean or import other configuration classes    |

  - `SpringApplication.run()`
    - Creates application context and registers all beans
    - Starts the embedded server Tomcat, etc..

## Component Scanning
  - ![alt-text](/2023-09-21-udemy-spring-boot-course-section-2-spring-core/component_scanning.png)
  - default, spring scans all sub packages from where the main method file is located
    - scans these packages recursively
  - doesn't matter the name of the packages
  
### Specify explicitly 
  - we can specify explicitly what packages to scan with `scanBasePackages= {...}`

```java
@SpringBootApplication(
		scanBasePackages= {"springboot.something","springboot.other"}
)
public class DependencyInjectionDemoApplication {
	public static void main(String[alt-text] args) {
		SpringApplication.run(DependencyInjectionDemoApplication.class, args);
	}

}

```

## @Qualifer
  - when you have multiple beans and need to specify one


By default the component name for a class will camelCase with the first letter being lowercase.
In order to override this you have to specify with **@Component("BeanName")**
```java
@Component("FootballCoach")
public class FootballCoach implements Coach{

    @Override
    public String getDailyWorkout() {
        return "10 up-downs, and hit  25 people";
    }
}
```
  
Then to specify which bean you want injected you can use the **@Qualifer("BeanName")**
```java
@RestController
public class Controller {
    private Coach mycoach;

    @Autowired
    public Controller(@Qualifier("footballCoach") Coach mycoach) {
        this.mycoach = mycoach;
    }

    @GetMapping("/")
    public String test(){
        return "Home route";
    }

    @GetMapping("/getdailyworkout")
    public String getdailyWorkout(){
        return this.mycoach.getDailyWorkout();
    }
}
```

## @Primary
  - You can use the @Primary annotation instead or instead or in conjunction with the @Qualifer annotation
  - It goes in the @Component class
  - That way if you have multiple coach types it will inject the class with the @Primary annotation as default
  - You will get an error if more than one bean has the @Primary annotation
  - If you have a @Primary bean and specify a bean in @Qualifer, the **@Qualifer has higher priority**

```java
@Component
@Primary
public class BaseballCoach implements Coach{
  // implementation
}
```

## Lazy Initialization @Lazy
  - Lazy initialization is the pattern of putting off the creation of an object or process until it is needed.
  - By default, when your app starts, all beans are initialized. Regardless if they are going to be used or not
  - We can setup lazy initialization where the beans is only created if:
    - It is needed for dependency injection
    - it is explictly requested

```java
@Component
@Lazy
public class BaseballCoach implements Coach{
    @Override
    public String getDailyWorkout() {
        return "Do 10 poles and hit 5 homeruns";
    }
}
```

| Advantages                     |                                Disadvantages                                |
| :----------------------------- | :-------------------------------------------------------------------------: |
| Only create objects as needed  | Web related components have to create the beans needed on the first request |
| Helps with faster startup time |               may not see configuration issues until too late               |


### Global Configuration
  - Using the @Lazy for every single component could get tedious
  - We could use the global configuration to make all components to load lazyily

```properties
spring.main.lazy-initialization=true
```

## Bean Scope
  - Default scope is **Singleton**
    - spring container only creates 1 instance of a bean
    - it is cached in memory
    - all dependency injections for a bean will reference the same bean

  - ![alt-text](/2023-09-21-udemy-spring-boot-course-section-2-spring-core/singleton_diagram.png)

### Specify Bean Scope @Scope
  - [Spring bean scopes documentation](https://docs.spring.io/spring-framework/docs/3.0.0.M3/reference/html/ch04s04.html)

| Scope          |                                                                                             Description                                                                                             |
| :------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
| Singleton      |                                                        Scopes a single bean definition to a single object instance per Spring IoC container.                                                        |
| Prototype      |                                                                 Scopes a single bean definition to any number of object instances.                                                                  |
| Session        |                               Scopes a single bean definition to the lifecycle of a HTTP Session. Only valid in the context of a web-aware Spring ApplicationContext.                               |
| Global Session | Scopes a single bean definition to the lifecycle of a global HTTP Session. Typically only valid when used in a portlet context. Only valid in the context of a web-aware Spring ApplicationContext. |

```java
@Component
@Scope(ConfigurableBeanFactory.SCOPE_PROTOTYPE)
public class FootballCoach implements Coach{

  public class FootBallCoach(){
    System.out.println("FootballCoach constructor()");
  }
    
    @Override
    public String getDailyWorkout() {
        return "10 up-downs, and hit  25 people";
    }
    
}
```

```java
@RestController
public class Controller {
    private Coach mycoach;
    private Coach otherCoach;

    @Autowired
    public Controller(@Qualifier("footballCoach") Coach mycoach,
                      @Qualifier("footballCoach") Coach otherCoach) {
        this.mycoach = mycoach;
        this.otherCoach = otherCoach;
    }

    @GetMapping("/check")
    public String check(){
        return "Comparing beans: myCoach == otherCoach: " + ((mycoach ==  otherCoach) ? "True": "False");
    }
```

  - if we went to /other
    - we wold see "False", because myCoach and otherCoach are two different objects since using the **prototype scope**

### Singleton
  - One bean instance per spring container

### Prototype
  - Scopes single bean to any number of object instances
  - ![alt-text](/2023-09-21-udemy-spring-boot-course-section-2-spring-core/prototype_example.png)





## Bean LifeCycle
  - ![alt-text](/2023-09-21-udemy-spring-boot-course-section-2-spring-core/Bean-Life-Cycle-Process-flow3.png)
  - if we want to execute some code on the bean instantiation and just after closing the spring container, then we can write that code inside the custom init() method and the destroy() method.
  - What is the point of the custom init/destroy methods
    - custom code during bean initialization, destroy

### @PostConstruct init()
  - The @PostCostruct is the init() method

```java
@Component
public class FootballCoach implements Coach{

    public FootballCoach() {
        System.out.println("IN CONSTRUCTOR: " + getClass().getSimpleName());
    }

    // init method
    @PostConstruct
    public void doStartupStuff(){
        System.out.println("football coach needs redbull to get started...");
    }

    @Override
    public String getDailyWorkout() {
        return "10 up-downs, and hit  25 people";
    }
}
```

```java
@RestController
public class Controller {
    private Coach mycoach;

    @Autowired
    public Controller(@Qualifer("footballCoach")Coach mycoach) {
        this.mycoach = mycoach;
    }


    @GetMapping("/getdailyworkout")
    public String getdailyWorkout(){
        return this.mycoach.getDailyWorkout();
    }

}
```

  - Output will be the following

```
IN CONSTRUCTOR: FootballCoach
football coach needs redbull to get started...
```

### @PreDestroy destroy() method
  - The @PreDestroy is the destroy() method
  - The destroy() method is **not** called on beans with **Prototype scope**

```java
@PreDestroy
public void doCleanupStuff(){
    System.out.println("Cleaning up the rest of the stuff");
}
```

## Configure Beans with java code @Configuration & @Bean
  - you can configure beans with java code instead of annotations
  - When does it make sense to use a configuration file instead of @Component on classes
    - make an existing 3rd party class available to the Spring Framework

  - Steps
    - Need to configure class with **@Configuration** annotation
    - Configure **@Bean method** that returns a bean
  - ![alt-text](/2023-09-21-udemy-spring-boot-course-section-2-spring-core/configure_bean.png)

```java
public class SwimCoach implements Coach{
    @Override
    public String getDailyWorkout() {
        return "swim 10 laps";
    }
}
```
{: file='SwimCoach.java'}

```java
@Configuration
public class SportsConfig {
  @Bean("swimmingCoach") // overriding the default bean id which would just be the method name below
  public Coach swimCoach(){ // bean id will default to the method name
      return new SwimCoach();
  }
}
```
{: file='SportsConfig.java'}

```java
@Autowired
public Controller(@Qualifier("swimmingCoach") Coach mycoach) {
    this.mycoach = mycoach;
}
```
{: file='Controller.java'}

