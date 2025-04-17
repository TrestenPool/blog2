---
title: C# Generics
author: Tresten Pool
layout: post
date: 2025-04-15 20:10 -0500
categories: [C#]
tags: [c#, generics]
image:
  path: /Csharp-Generics/profile.png
---

## Generic Constraints
---

| Company             | Contact                              |
| :------------------ | :----------------------------------- |
| where T: base-class | Base class constraint                |
| where T: interface  | Interface constraint                 |
| where T: class      | Class constraint                     |
| where T: class?     | Nullable Class constraint            |
| where T: unmanaged  | Unmanaged constraint                 |
| where T: new()      | Parameterless constructor constraint |
| where T: T          | Naked type constraint                |
| where T: notnull    | Not Nullable value type constraint   |

Example:

```cs
public class Program {
  public static void Main(string[] args) {
    Dog dog = new();
    DoSomething(dog);
  }

  public static void DoSomething<T>(T animal) where T : Animal{
    animal.Attack();
    animal.Defend();
  }

}

public interface Animal {
  // ...
}

class Dog : Animal{
  // ...
}
```
{: file='Program.cs'}


---
<br><br>

