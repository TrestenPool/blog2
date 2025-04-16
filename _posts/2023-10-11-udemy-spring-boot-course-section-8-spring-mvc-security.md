---
layout: post
title: 'Udemy Spring boot course: Section 8 Spring MVC Security'
date: 2023-10-11 16:59 -0500
categories: [Udemy, Java, Springboot, Spring MVC, Security]
tags: [Java, Programming, Udemy, Spring] 
image: 
  path: /2023-10-11-udemy-spring-boot-course-section-8-spring-mvc-security/profile.png
---

- [Git repo](#git-repo)
- [App goal](#app-goal)
  - [Example](#example)
  - [Show the user incorrect password and/or password](#show-the-user-incorrect-password-andor-password)
  - [Logging out a user](#logging-out-a-user)
  - [Getting the username of the currently logged in user](#getting-the-username-of-the-currently-logged-in-user)
  - [Getting the roles of the currently logged in user](#getting-the-roles-of-the-currently-logged-in-user)
  - [Restricting URL's to Roles](#restricting-urls-to-roles)
- [Custom Access Denied page](#custom-access-denied-page)
- [Display based on Role](#display-based-on-role)
- [Using JDBC authentication for the username,password roles](#using-jdbc-authentication-for-the-usernamepassword-roles)
  - [ROLE\_ROLEName by default](#role_rolename-by-default)
- [Make spring security use custom tables for authentication](#make-spring-security-use-custom-tables-for-authentication)


# Git repo
  - [alt-text]()

# App goal
  - ![alt-text](/2023-10-11-udemy-spring-boot-course-section-8-spring-mvc-security/app.png)
    - Employees can access /
    - Admins can access /systems
    - Managers can access /leaders
  
  - Security design goal
  - ![alt-text](/2023-10-11-udemy-spring-boot-course-section-8-spring-mvc-security/our_diagram.png)
  
## Example

@Configuration File
  - first method is the in memory username and password storage
    - will use db for authentication in the future
  - Second method specififies the configuration for the Web MVC security
    - comments explain what each line of code does

```java
@Configuration
@EnableWebSecurity
public class SecurityConfiguration {

    // in memory configuration
    @Bean
    public UserDetailsService users() {

        UserDetails john = User.builder()
                .username("john")
                .password("{noop}test123")
                .roles("EMPLOYEE")
                .build();

        UserDetails mary = User.builder()
                .username("mary")
                .password("{noop}test123")
                .roles("EMPLOYEE", "MANAGER")
                .build();

        UserDetails susan = User.builder()
                .username("susan")
                .password("{noop}test123")
                .roles("EMPLOYEE", "MANAGER", "ADMIN")
                .build();

        return new InMemoryUserDetailsManager(john, mary, susan);
    }

    // security filter chain configuration
    @Bean
    public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {
        http
                // enable csrf with the defaults
                .csrf(Customizer.withDefaults())

                // authorize all request that are authenticate
                .authorizeHttpRequests(
                        authorize -> authorize.anyRequest().authenticated()
                )

                // uses http basic auth
                .httpBasic(Customizer.withDefaults())

                // Tells it to use the default login form page
//                .formLogin(Customizer.withDefaults());

                // uses custom login form
                .formLogin(
                        form ->
                                // login page
                                form.loginPage("/showMyLoginPage")
                                // where the login page is posted to, we don't have to worry about this,
                                // ... spring will take care and create this automagically for us in the background
                                .loginProcessingUrl("/authenticateTheUser")
                                // allow everybody to see the login page
                                .permitAll()
                );

        // return the http build for the spring security filter chain
        return http.build();
    }
}
```

HTML Custom Login Page
  - Using custom Login page but somethings like below have to have a certain structure
    - username has to be named **username**
    - password has to be named **password**
  - We get the /autenticateTheUser for free since Spring will create that automatically for us since we specified it in the @Configuration

```html
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>Login page</title>
</head>
<body>
    <h2>Login Form</h2>
    <!-- Goes to the route we specified in the SecurityConfiguration.java -->
    <form th:action="@{/authenticateTheUser}" method="POST">

        <p>
            <!-- name must be username when using spring security -->
            User name: <input type="text" name="username">
        </p>

        <p>
            <!-- name must be password when using spring security -->
            Password: <input type="text" name="password">
        </p>

        <input type="submit" value="Login">
    </form>

</body>
</html>
```

Simple Demo Controller
  - / is the home route
  - /showMyLoginPage is the login page
    - all unauthenticated requested get routed here first to get authenticated (specified in the @Configuration)

```java
@Controller
public class DemoController {
    @GetMapping("/")
    public String home(){
        return "home";
    }

    @GetMapping("/showMyLoginPage")
    public String loginPage(){
        return "security/plain-login";
    }
}
```

## Show the user incorrect password and/or password
  - if the login fails, I want to let the user know that it had failed
  - By default spring will append the query parameter ?error to the end of the url and redirect back to the login page
  - We can show the error message by just doing the following in the html form

This is all we have to do show the error message
  - **param** is a keyword to get any of the query parameters from the url
  - We are saying if there is a param.query in the url we will show this message between the div

```html
  <!-- show error if there is any -->
  <div th:if="${param.error}" class="alert alert-error">
      Invalid username and password.
  </div>
```

## Logging out a user
  - the /logout is provided by Spring for free
  - when a user is logged out the following will happen
    - invalidate user http session and remove session cookies
    - send the user back to the login page
    - append the ?logout query parameter to the login form route


## Getting the username of the currently logged in user
  - You can get the username of the user that is currently logged in with the code below

```html
Username: <span sec:authentication="principal.username"></span>
```

## Getting the roles of the currently logged in user
  - You can get the roles of the currenly logged in user with the code below

```html
Role(s): <span sec:authentication='principal.authorities'></span>
```

## Restricting URL's to Roles
  - Boilerplate code for restricting urls to certain roles
  - `requestMatchers("/").hasRole("EMPLOYEE")`
  
```java
public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {
  http
    .authorizeHttpRequests(authorize -> 
                authorize
                    // restrict urls based on roles
                    .requestMatchers("/").hasRole("EMPLOYEE")
                    .requestMatchers("/leaders/**").hasRole("MANAGER")
                    .requestMatchers("/systems/**").hasRole("ADMIN")
                    .anyRequest().authenticated()
    )

    // other stuff

  return http.build();
}
```

# Custom Access Denied page
  - We can have our own custom access denied page instead of the default


```java
public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {
  http
    // here it is 
    .exceptionHandling(configurer ->
            configurer
                    // this is the route /access-denied
                    .accessDeniedPage("/access-denied")
    )

    // other stuff

    return http.build();
}

```

# Display based on Role
  - We want to display links only if the currently logged in user has a specific role
  - `sec:authorize="hasRole('MANAGER')"`
  
```html
<!-- Add a link to point to /leaders -->
<p sec:authorize="hasRole('MANAGER')">
    <a th:href="@{/leaders}">Leaders page (for managers only)</a>
</p>
```

# Using JDBC authentication for the username,password roles
  - Spring uses these tables by default
    - users 
      - username
      - password
      - enabled
    - authorities (AKA Roles)
      - username
      - authority

## ROLE_ROLEName by default
  - By default spring uses the format ROLE_ROLEName
  - So we have to be mindful of this when we insert our roles into the authorities table
  - it should look something like this ...
  - ![alt-text](/2023-10-11-udemy-spring-boot-course-section-8-spring-mvc-security/roles_pic.png)
  
# Make spring security use custom tables for authentication
  - we will try to use jdbc authentication with our custom tables
  - here are our tables
    - members
      - user_id
      - ps
      - active
    - roles
      - user_id
      - role

Here is the code to make springboot aware of the custom tables with the custom queries
  - This code goes in your @Configuration file

```java
    // connect to the mysql db for authentication
    @Bean
    public UserDetailsManager userDetailsManager(DataSource dataSource){
        // gets the datasource created by spring by default
        JdbcUserDetailsManager jdbcUserDetailsManager = new JdbcUserDetailsManager(dataSource);

        // finds the user by the username
        jdbcUserDetailsManager
                .setUsersByUsernameQuery("SELECT user_id, pw, active FROM members WHERE user_id=?");

        // finds the roles for the user by the username
        jdbcUserDetailsManager
                .setAuthoritiesByUsernameQuery("SELECT user_id, role FROM roles WHERE user_id=?");

        return jdbcUserDetailsManager;
    }
```
