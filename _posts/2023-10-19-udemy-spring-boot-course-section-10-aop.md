---
layout: post
title: 'Udemy Spring boot course: Section 10 AOP'
date: 2023-10-19 10:39 -0500
categories: [Springboot, Spring]
image: 
  path: /2023-10-19-udemy-spring-boot-course-section-10-aop/profile.png
---

- [Git Repo for this sesion](#git-repo-for-this-sesion)
- [Resources](#resources)
- [Brief intro example](#brief-intro-example)
- [Aspect oriented programming](#aspect-oriented-programming)
  - [Weaving](#weaving)
  - [Pointcut Expressions](#pointcut-expressions)
  - [Pointcut Declarations](#pointcut-declarations)
    - [Combining Pointcut Declarations](#combining-pointcut-declarations)
    - [Controlling Aspect order with @Order](#controlling-aspect-order-with-order)
    - [How to access method signature and method parameters in the advice](#how-to-access-method-signature-and-method-parameters-in-the-advice)
    - [Accessing the return value for a @AfterReturning advice](#accessing-the-return-value-for-a-afterreturning-advice)
    - [@AfterThrowing](#afterthrowing)
    - [@Around](#around)


# Git Repo for this sesion
  - put here

# Resources
  - {% include embed/youtube.html id='Ft29HgsePfQ' %}
  - [baelung docs on aop](https://www.baeldung.com/spring-aop-vs-aspectj)
  - [pointcut explained](https://jstobigdata.com/spring/pointcut-expressions-in-spring-aop/)
  - [static methods Spring aop](https://stackoverflow.com/questions/55964758/how-to-advise-static-methods-using-spring-aop)

# Brief intro example 
  - we have the following architecture
    - ![alt-text](/2023-10-19-udemy-spring-boot-course-section-10-aop/app_arch.png)
  - we have the following code for our dao
```java
public void addAccount(Account account, String userId) {
  entityManager.persist(account);
}
```
  - lets say manager asks us to implement logging with the following requirements
    - modular - can be used for other methods
    - happens before and/or after the method we call
  -lets say manager asks us to do the same thing but to implement security

We could do the following but we would have to reuse the code in other places, just copying and pasting (NOT GOOD PRACTICE)
```java
public void addAccount(Account account, String userId) {
  // logging +4 lines
  // security +5 lines
  entityManager.persist(account);
}
```

This introduces Two big Problems
  - **Code Tangling**
    - logging and security code tangled together along with business logic
  - **Code Scattering**
    - If we need to update the logging or security codes, we have to do so in numerous places


Other Quick Possible solutions that could work
  - **Inheritence**
    - create a abstract class of Logging & Security and just have the classes inherit from it
    - This could work but but every class would need to inherit from these classes
    - Plus java doesn't support multile inheritence so it could inherit from Logging or Security but **not both**
  
  - **Delegation**
    - classes delegate logging and security calls
    - we would still need to uppdate all those classes that want to implement logging/security and put the call to those methods in there
  
Next section below talks about the BEST SOLUTION (AOP)

# Aspect oriented programming
  - Programming paradigm based on this concept of a **Aspect**
  - AOP is an extension of OOP
  - **Aspect**
    - encapsulates **cross-cutting concerns**
    - Where cross-cutting concerns are just logic like security, logic that is the same for multiple methods
  - ![alt-text](/2023-10-19-udemy-spring-boot-course-section-10-aop/cross-cutting.png)

AOP Terminology

| Term      | Description                                                                                                                                                                                                                                        |
| :-------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Aspect    | a standard code/feature that is scattered across multiple places in the application and is typically different than the actual Business Logic (for example, Transaction management). Each aspect focuses on a specific cross-cutting functionality |
| Advice    | the action taken by the aspect in a specific joinpoint                                                                                                                                                                                             |
| Joinpoint | it’s a particular point during execution of programs like method execution, constructor call, or field assignment                                                                                                                                  |
| Pointcut  | a regular expression that matches a joinpoint. Each time any join point matches a pointcut, a specified advice associated with that pointcut is executed                                                                                           |
| Weaving   | the process of linking aspects with targeted objects to create an advised object                                                                                                                                                                   |

Advice Types

| Advice          | Description                                                                               |
| :-------------- | :---------------------------------------------------------------------------------------- |
| Before          | Run advice before the method execution.                                                   |
| After           | Run advice after the method execution, regardless of its outcome.                         |
| After-returning | Run advice after the method execution, only if the method completes successfully.         |
| After-throwing  | Run advice after the method execution, only if the method exits by throwing an exception. |
| Around          | Run advice before and after the advised method is invoked.                                |


Point Cut expressions

| Expression | Description                             |
| :--------- | :-------------------------------------- |
| Before     | Run advice before the method execution. |

Pros / Cons

| Pros                                     | Cons                                                               |
| :--------------------------------------- | :----------------------------------------------------------------- |
| Reusable modules                         | Too many Aspects                                                   |
| Resolve code tangling                    | App flow can be hard to follow                                     |
| Resolve code scatter                     | Minor performance cost for aspect execution  (**runtime weaving**) |
| Apply selectively based on configuration |                                                                    |


## Weaving
  - Two leading AOP frameworks for Java
    - Spring AOP
    - AspectJ

Spring AOP
  - support out of the box
  - run-time weaving utilizing proxy-based

Proxy-based
  - ![alt-text](/2023-10-19-udemy-spring-boot-course-section-10-aop/proxy.png)

Runtime weaving
  - Runtime weaving, in the context of Aspect-Oriented Programming (AOP), refers to the process of applying aspects (cross-cutting concerns) to a running program or application. 

AspectJ
  - Original AOP framework
  - provides **complete support** for AOP
  - released in 2001

Runtime weaving vs Compile-time weaving
  - Runtime weaving involves integrating aspect code with the running application at runtime, typically during the execution of the program.
  - This is in contrast to compile-time weaving, where aspect code is integrated with the application during the compilation phase.
  - Runtime weaving allows you to add, modify, or remove aspects without recompiling the entire application, making it more flexible and adaptable.

Spring AOP pros/cons

| Pros                                                 | Cons                                                                  |
| :--------------------------------------------------- | :-------------------------------------------------------------------- |
| Simplier to use than AspectJ                         | only supports **method level** join points                            |
| Uses Proxy pattern                                   | Can **only** apply aspects to beans created by **Spring app context** |
| Can migrate to AspectJ when using @Aspect annotation | Minor performance costs for using **run-time weaving**                |


AspectJ pros/cons

| Pros                                                 | Cons                                                     |
| :--------------------------------------------------- | :------------------------------------------------------- |
| Support **all** Join points                          | Compile-time weaving required **extra compilation step** |
| works with any POJO, not just beans from app context | AspectJ **pointcut** **syntax** can become **complex**   |
| **Faster** performance compared to Spring AOP        |                                                          |
| **Complete** AOP support                             |                                                          |

Parameter Pattern Wildcards

| Symbol              | Description                                                                                     |
| :------------------ | :---------------------------------------------------------------------------------------------- |
| ()                  | matches a method with **No** arguments                                                          |
| (*)                 | matches a method 1 argument of any type                                                         |
| (..)                | matches a method with **0 or more arguments** of any type                                       |
| (int,..)            | matches a method with 1 argument of type int, or multiple arguments with the first being an int |
| (com.tpool.Account) | 1 argument of type Account object with full class path                                          |


Should you use Spring AOP or AspectJ
  - Spring AOP is a lightweight version of AspectJ
  - it solves common enterprise problems
  - start off with Spring AOP and if you have complex business needs go ahead and use AspectJ

## Pointcut Expressions
  - Spring AOP uses AspectJ pointcut expressions
  - Spring AOP has no support for static methods
  - 
  - Pointcut
    - It is a predicate expression that determines the Join points, hence allowing us to control the advice execution
    - In simple words, a pointcut expression is like a Regular Expression which determines the classes and methods where the Advice will be executed
  - Declaring a pointcut is simple, all you need is annotate the method with `@Pointcut(POINTCUT_EXPRESSION)`
  - ![alt-text](/2023-10-19-udemy-spring-boot-course-section-10-aop/pointcut-1.png)
    - matches on specific class method name
  - ![alt-text](/2023-10-19-udemy-spring-boot-course-section-10-aop/pointcut-2.png)
    - just matches on any class that has the method name
  - ![alt-text](/2023-10-19-udemy-spring-boot-course-section-10-aop/pointcut-3.png)
    - matches on any method name starting with **add** like addStudent(), addLog(), addAnything()
  - ![alt-text](/2023-10-19-udemy-spring-boot-course-section-10-aop/pointcut-4.png)
    - matches on any return type
    - matches on any method that starts with processCreditCard*
  - `@Before("execution(* com.tpool.aopdemo.dao.*.*(..))")`
    - this matches for all methods in a given package
    - com.tpool.aopdemo.dao - tells spring this is the base package
    - .* - tells spring any class
    - .* - tells spring any method name
    - (..) - tels spring any number of arguments of any type

## Pointcut Declarations
  - way of **reusing** our **pointcut expressions** to multiple advices
  - Declaring pointcut-declarations
    - ![alt-text](/2023-10-19-udemy-spring-boot-course-section-10-aop/pointcut-declaration.png)
  - Applying pointcut declaration to advice
    - ![alt-text](/2023-10-19-udemy-spring-boot-course-section-10-aop/apply-pointcut-declaration.png)

### Combining Pointcut Declarations
  - we can apply multiple pointcut declarations using **logic operators**
  - The example we want to do is apply pointcut declarations to "All methods in a package EXCEPT getter/setter methods"

```java
// just a collection of related advices
@Aspect
@Component
public class MyDemoLoggingAspect {

    // all methods that are in the dao package
    @Pointcut("execution(* com.tpool.aopdemo.dao.*.*(..))")
    private void forDaoPackage(){};

    @Pointcut("execution(* com.tpool.aopdemo.dao.*.get*(..))")
    private void DaoGetters(){};

    @Pointcut("execution(* com.tpool.aopdemo.dao.*.set*(..))")
    private void DaoSetters(){};

    // all in the dao package but no getters or setters
    @Pointcut("forDaoPackage() && !(DaoGetters() || DaoSetters())")
    private void forDaoPackageNoGetterSetter(){}

    @Before("forDaoPackageNoGetterSetter()")
    public void logging(){
        System.out.println("logging here ...");
    }
}
```

### Controlling Aspect order with @Order
  - We want the advices to run in a certain order
  - Lower numbers have higher precedence
  - negative numbers are allowed
  - numbers do not have to be consecutive 
    - ex. 1, 5, 10, 12
  - ![alt-text](/2023-10-19-udemy-spring-boot-course-section-10-aop/breaking_up_aspects.png)
    - we have to break up the single aspect into multiple to get that fine grain control of the order
  - ![alt-text](/2023-10-19-udemy-spring-boot-course-section-10-aop/order.png)
    - the order in which the aspects will run in
  - ![alt-text](/2023-10-19-udemy-spring-boot-course-section-10-aop/annotations.png)
  - What if two aspects have the same order number?
    - it is considered undefined, so expect wacky results

```java
@Aspect
public class AopExpressions {
    // all methods that are in the dao package
    @Pointcut("execution(* com.tpool.aopdemo.dao.*.*(..))")
    public void forDaoPackage(){};

    // getter methods
    @Pointcut("execution(* com.tpool.aopdemo.dao.*.get*(..))")
    public void DaoGetters(){};

    // setter methods
    @Pointcut("execution(* com.tpool.aopdemo.dao.*.set*(..))")
    public void DaoSetters(){};

    // all in the dao package but no getters or setters
    @Pointcut("forDaoPackage() && !(DaoGetters() || DaoSetters())")
    public void forDaoPackageNoGetterSetter(){}
}
```
{: file='AopExpressions.java'}

```java
@Aspect
@Component
@Order(1)
public class LoggingAspect {
    @Before("com.tpool.aopdemo.aspect.AopExpressions.forDaoPackageNoGetterSetter()")
    public void CloudLog(){
        System.out.println("=======> Cloud log");
    }
}
```
{: file='LoggingAspect.java'}

```java
@Aspect
@Component
@Order(2)
public class ApiAspect {
    @Before("com.tpool.aopdemo.aspect.AopExpressions.forDaoPackageNoGetterSetter()")
    public void apiLog(){
        System.out.println("=======> API log");
    }
}
```
{: file='ApiAspect.java'}
    
```java
@Aspect
@Component
@Order(3)
public class SecurityAspect {
    @Before("com.tpool.aopdemo.aspect.AopExpressions.forDaoPackageNoGetterSetter()")
    public void security(){
        System.out.println("=======> security check");
    }
}
```
{: file='SecurityAspect.java'}
  

### How to access method signature and method parameters in the advice
  - we want to use the method signature and parameters in the advice for things like logging the method that was called
  - We want to access the return value for a method 
  - ![alt-text](/2023-10-19-udemy-spring-boot-course-section-10-aop/return_value.png)

```java
@Aspect
@Component
@Order(3)
public class SecurityAspect {
    @Before("com.tpool.aopdemo.aspect.AopExpressions.forDaoPackageNoGetterSetter()")
    public void security(JoinPoint joinPoint){
        System.out.println("=======> security check");

        // method signature
        MethodSignature methodSignature = (MethodSignature) joinPoint.getSignature();
        System.out.println("Method: " + methodSignature);


        // go through all of the arguments
        System.out.println("args");
        Object[] args = joinPoint.getArgs();
        for(var arg: args) {
            System.out.println(arg);
        }
        System.out.println("=== end of args ===");

    }
}
```

### Accessing the return value for a @AfterReturning advice
  - We want to access the return value for a method 
  - ![alt-text](/2023-10-19-udemy-spring-boot-course-section-10-aop/return_value.png)

```java
@AfterReturning(
        pointcut = "execution(* RetrieveMemberships(..))",
        returning = "result"
)
public void afterReturningResult(List<String> result) {
    // remove all of the elements in the list
    result.clear();
    result.addAll(Arrays.asList("You", "are", "awesome", "!"));
}
```

### @AfterThrowing
  - advice is executed after an exception is thrown from the method being called
  - ![alt-text](/2023-10-19-udemy-spring-boot-course-section-10-aop/sequence_diagram.png)
  - What its great for
    - log exceptions
    - perform auding on the exception
    - notify devops team via email or sms

How to access exception object
  - use the `throwing="theException"`
  - the throwing=**theException** has to match what is in the parameters for Throwable **theException**

```java
@AfterThrowing(
        pointcut = "execution(* com.tpool.aopdemo.dao.MembershipDAOImpl.simulateException(..) )",
        throwing = "throwingException"
)
public void afterThrowing(Throwable throwingException){
    System.out.println("you threw an exception buddy");
    
    // print out the exception message
    System.out.println(throwingException.getMessage());
}
```

### @Around
  - Runs before and after method execution
  - Most common use cases
    - logging
    - auditing
    - security
    - pre-processing & post-processing
  - Ability to manage exeptions
    - swallow, handle, stop exceptions
  - When using @Around advice you get a reference to the **ProceedingJoinPoint**
    - this is a handle to the target method
    - your code can use this to execute the target method

Example below
  - ProceedingJointPoint
  - notice `proceedingJointPoint.proceed()` gets the method to be executed

```java
@Around("execution(* com.tpool.aopdemo.dao.MembershipDAOImpl.getAccount(..) )")
public Object aroundDemo(ProceedingJoinPoint proceedingJoinPoint) throws Throwable{
    // start time
    long begin = System.currentTimeMillis();

    // calls getAccount()
    Object result = proceedingJoinPoint.proceed();

    // end time
    long end = System.currentTimeMillis();

    long duration = end - begin;
    System.out.println("\n======> DURATION " + duration + " milliseconds");

    return result;
}
```

Exception Handling
  - for an exception thrown from proceeding join point we can
    - you can handle / swallow / stop the exception
    - or you can simply re-throw the exception
  - ![alt-text](/2023-10-19-udemy-spring-boot-course-section-10-aop/exception_sequence_diagram.png)

```java
@Around("execution(* com.tpool.aopdemo.dao.MembershipDAOImpl.getAccount(..) )")
public Object handleException(ProceedingJoinPoint proceedingJoinPoint) throws Throwable {
    System.out.println("beginning of handleException()");

    Object result;
    try {
        result = proceedingJoinPoint.proceed();
    }
    catch (Exception e) {
        result = "exception occured, but we don't really care";
    }

    System.out.println("end of handleException()");
    return result;
}
```

If we wanted to rethrow the exception we'd simply use throw again in the catch block like this
````java
catch (Exception e) {
    throw e;
}
```




## Enabling Spring AOP
  - Add to the pom.xml
    - it will be automatically enabled after that
    - in the old days you would have to use the @EnableAspectJAutoProxy annotation

# Example using @Before

Development process
  - Create target object: AccountDao
  - Create main app
  - Create an Aspect with **@Before** advice

Create target object: AccountDao
```java
public interface AccountDAO {
  void add Account();
```
```java
@Component
public class AccountDAOImpl implements AccountDAO {
  void add Account() {
    System.out.println("ADDING ACCOUNT");
  }
```

Create main app
```java
@SpringBootApplication
public class AppdemoApplication {

	public static void main(String[] args) {
		SpringApplication.run(AppdemoApplication.class, args);
	}

	@Bean
	public CommandLineRunner commandLineRunner(AccountDAO accountDAO) {
		return runner -> {
			demoTheBeforeAdvice(accountDAO);
		};
	}

	private void demoTheBeforeAdvice(AccountDAO accountDAO) {
		accountDAO.addAccount();
	}

}
```

Create an Aspect with **@Before** advice

```java
@Aspect
@Component
public class MyDemoLoggingAspect {
    // pointcut expression goes between the parens of @Before
    @Before("execution(public void addAccount())")
    public void loggingAdvice() {
        System.out.println("===============================");
        System.out.println("===> Logging stuff here... <===");
        System.out.println("===============================");
    }
}
```

When we run our code we get the following
```text
===============================
===> Logging stuff here... <===
===============================
class com.tpool.aopdemo.dao.AccountDAOImpl: DOING MY DB: WORK ADDING AN ACCOUNT
```


