---
title: .NET Core Routing
author: Tresten Pool
layout: post
date: 2025-04-17 01:10 -0500
categories: [dotnet]
tags: [dotnet, routing]
image:
  path: /Dotnet-Core-Routing/profile.png
---

<!-- Table of contents -->
- [Conventional vs Attribute routing](#conventional-vs-attribute-routing)
- [Conventional](#conventional)
  - [app.MapControllerRoute()](#appmapcontrollerroute)
- [Attribute Routing](#attribute-routing)


## Conventional vs Attribute routing

| Topic          | Conventional                              |                                 Attribute |
| :------------- | :---------------------------------------- | ----------------------------------------: |
| Where its used | typically used in mvc                     |                   typically used for apis |
| Why its called | it establishes a convention for url paths | uses attributes above classes and methods |

## Conventional
---

Full Example

```cs
  var builder = WebApplication.CreateBuilder(args);

  builder.Services.AddControllersWithViews();

  var app = builder.Build();

  if (!app.Environment.IsDevelopment())
  {
    app.UseExceptionHandler("/Home/Error");
    app.UseHsts();
  }

  app.UseHttpsRedirection();
  app.UseStaticFiles();
  app.UseRouting();
  app.UseAuthorization();

  app.MapControllerRoute(
      name: "default",
      pattern: "{controller=Home}/{action=Index}/{id?}");

  app.Run();
```
{: file='Program.cs'}

- `"{controller=Home}/{action=Index}/{id?}"` matches routes like
  - This defaults the controller to **Home** and the default action to **Index**
  - But will also route /Products/Index/1 or /Products/Index

- `MapControllerRoute` creates a single route
- The following are all of the available properties 

```cs
  endpoints.MapControllerRoute(
    name: string,
    pattern: string,
    defaults: object? = null,
    constraints: object? = null,
    dataTokens: object? = null
  );
```

---
<br><br>

### app.MapControllerRoute()
---

What it does?
  - a convenience method that replaces the following code
  
```cs
  app.MapControllerRoute(
    name: "default",
    pattern: "{controller=Home}/{action=Index}/{id?}");
```

The following creates a conventional route named **myroute** whenever `blog/` is accessed it will use the `Index2` action method in the `Blog` controller
```cs
app.MapControllerRoute(
  name: "myroute",
  pattern: "blog/",
  defaults: new { controller="Blog", action="Index2" }
)
```

---
<br><br>




## Attribute Routing
---


---
<br><br>
