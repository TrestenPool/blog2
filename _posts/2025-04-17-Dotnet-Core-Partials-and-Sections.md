---
title: .NET Core Partials and Sections and Layouts
author: Tresten Pool
layout: post
date: 2025-04-17 01:10 -0500
categories: [dotnet]
tags: [dotnet, partials, sections, layouts]
image:
  path: /Dotnet-Core-Partials-and-Sections/profile.png
---


## Differences betwen Layouts, Partials, Sections
--- 

Differences
  - Layout
    - **Define overall structure of the page**
    - applied to one or more views
    - provides a consistent look across the application [header, footer, navbar]
    - The following will reder the content in the layout 
      - `@RenderBody()` is used to render the contents in layout view
    - Full views have a primary model
    - used once per page

  - Partial
    - **Render reusable UI components within a view.**
    - Encapsulate UI elements [forms, lists, widgets]
    - the following will load the partial in the view
      - `@await Html.PartialAsync("_PartialName", Model)` 
      - or
      - `<partial name="_PartialName" model="Model">`
    - can accept and use specific models passed to them 
    - can be used multiple times in a single view

  - Section
    - **Inject view-specific content into predefined areas of a layout**
    - Allow specific parts of a content view to be placed in designed areas of the layout like [css, javascript]
    - the following will load the section in the layout
      - `@RenderSection("SectionName", required: false)`
    - the following will load the section in the content view
      - `@section SectionName{ ... }`
    - Reused accross views that share the same layout, but the content is view-specific
  
Analogy
  - Layout
    - The blueprint for the house
  - Partials
    - Pre-fabricated components like windows, lights, doors, etc ..
  - Sections
    - Designated areas within the house blueprint (layout) where the occupants of each room (view) can decide what ot put there, like choosing specific curtains for a window or a specific rug for the floor

---
<br><br>

## Sections

Take the following _Layout code below
```html
  <!-- ViewData -->
  @{
    string title = (string?)ViewData["title"] ?? "Default title";
  }
  <!DOCTYPE html>
  <html lang="en">
  <head>
    ...
    <title>@(title)</title>
  </head>
  <body>

    <div class="container">

      @* Navbar *@
      @await Html.PartialAsync("_Navbar")

      @* Page Content *@
      <div class="page-content">
        @RenderBody()
      </div>

    </div>

    @* Load any javascript files that the user specifies in the views *@
    @RenderSection("Scripts", required: false)
  </body>

  </html>
```
{: file='_Layout.cshtml'}

- The `RenderSection("Scripts", required: false)` tells dotnet for the views that use this layout, if the user defines a section in the view because it is optional, load it here in the layout

- The following code shows a view inputing some scripts into the section
```html
  ...
  @section Scripts {
    <script href="..."></script>
    <script href="..."></script>
  }
```
{: file='_sass/jekyll-theme-chirpy.scss'}
