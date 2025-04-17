---
title: .NET Core Client Side Validation
author: Tresten Pool
layout: post
date: 2025-04-15 20:10 -0500
categories: [dotnet]
tags: [dotnet, validation]
image:
  path: /Dotnet-Core-Client-Side-Validation/profile.png
---


## Adding Client Side Validation
--- 

Steps to add client side validation 

1\. Add `Required` annotation to the property

```cs
public class MyModel {
  [Required]
  public DataType PropertyName {get; set;}
}
```
{: file='mymodel.cs'}

2\. Add the `asp-for` attribute

- the `data-val` and `data-required` are **auto-generated**

```html
<input asp-for="PropertyName" data-val="true" data-required="ErrorMessage">
```
{: file='myview.cshtml'}

3\. Adding `asp-validation-for` to show the error message
  - underneath the input tag we have this span tag that will show the error message.
  - the error message is what is defined in the model class

```html
<span asp-validation-for="PersonName" style="color:red"></span>
```
{: file='myview.cshtml'}

```cs
[Required(ErrorMessage = "Person Name can't be blank")]
public string? PersonName { get; set; }
```
{: file='mymodel.cshtml'}




4\. Import JQuery Validation scripts
  - must be loaded in order
    - <https://cdnjs.com/libraries/jquery>
    - <https://cdnjs.com/libraries/jquery-validate>
    - <https://cdnjs.com/libraries/jquery-validation-unobtrusive>

---
<br><br>



## Showing all of the Error messages with `asp-validation-summary="All"`
--- 

You can show all of the error messages with ...

```html
<div asp-validation-summary="All"></span>
```
{: file='myview.cshtml'}

- This is typically at the bottom of the form to show all of the fields that have failed client side validation.

---
<br><br>
