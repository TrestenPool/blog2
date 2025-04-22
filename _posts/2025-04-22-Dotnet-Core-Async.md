---
title: .NET Core Asynchronous Programming
author: Tresten Pool
layout: post
date: 2025-04-22 01:10 -0500
categories: [dotnet]
tags: [dotnet, async, tasks]
image:
  path: /Dotnet-Core-Async/profile.png
---

<!-- Table of contents -->

## Task Parallel library
  - Tasks are the building block of asynchronous programming
  - A task resembles a thread or threadpool work item but at a higher level of abstraction


### Benefits
  - More efficient and scalable use of resources
  - 

### Creating and Running Tasks
  - `Parrallel.Invoke`
    - run 1..* statements **concurrently**
    - Takes an **Action** delegate(s)
    

