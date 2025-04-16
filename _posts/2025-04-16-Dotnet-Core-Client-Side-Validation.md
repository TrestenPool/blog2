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

3\. Import JQuery Validation scripts
  - must be loaded in order
    - <https://cdnjs.com/libraries/jquery>
    - <https://cdnjs.com/libraries/jquery-validate>
    - <https://cdnjs.com/libraries/jquery-validation-unobtrusive>

---
<br><br>
