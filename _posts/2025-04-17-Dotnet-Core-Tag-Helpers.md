---
title: .NET Core Tag Helpers
author: Tresten Pool
layout: post
date: 2025-04-17 01:10 -0500
categories: [dotnet]
tags: [dotnet, tagHelpers]
image:
  path: /Dotnet-Core-Tag-Helpers/profile.png
---


## asp-fallback-test & asp-fallback-src
--- 

What is it?
  - `asp-fallback-test` a test to see if it passed
    - `asp-fallback-test="<javascript-code that runs, should return true or false>"`
  - `asp-fallback-src` a src that will fallback to if the test failed
    - `asp-fallback-src="~/file.js"`

Example:

```html
  <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.7.1/jquery.min.js" asp-fallback-test="window.jQuery" asp-fallback-src="~/jquery.min.js" integrity="sha512- ...." crossorigin="anonymous" referrerpolicy="no-referrer"></script>
```
{: file='myview.cshtml'}

- `~/` in `asp-fallback-src="~/jquery.min.js"` refers to the `wwwroot` folder in your dotnet project

---
<br><br>


## asp-append-version

### Usage
  - `<img src="~Filepath" asp-append-version>`
  - gets translated to this ...
  - `<img src="/Filepath?v=HashOfImageFile">`

  - generates SHA512 hash of the image file as query string parameter appended to the file path. 
  - Regenerates a new hash every time when the file is changed on the server
  - If the same file is requested multiple times, the file hash will not be regenerated

### Why is this useful
  - By appending a unique version hash to the URL, you effectively tell the browser that this is a new version of the file. If the content of the static file changes on the server, ASP.NET Core will generate a different hash

---
<br><br>
