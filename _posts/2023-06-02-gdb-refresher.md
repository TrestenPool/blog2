---
author: Tresten Pool
layout: post
date: 2023-05-30 20:10 -0500
categories: [Programming]
tags: [c, gdb, programming] 
image:
  path: /2023-06-02-gdb-refresher/1.png
---

# GDB Refresher
![image](/2023-06-02-gdb-refresher/1.png)

## Compiling a c program and running it
```bash
gcc -g program.c -o program
```
- To call run the debugger on the program now all you need to do is `gdb program`


## Focus
- You can change the focus of where the arrow keys interact with
  - Focus on the src
    - `Focus src`
  - Focus on the command line
    - `Focus cmd`

## Layouts
- show layout of the code
![image](/2023-06-02-gdb-refresher/2.png)

- You can change the focus of different parts of the gdb interface
  - show the actual code
    - `layout src`
      - ![image](/2023-06-02-gdb-refresher/layout_src.png)

  - show the registers
    - `layout reg`
      - ![image](/2023-06-02-gdb-refresher/layout_reg.png)

  - show the assembly
    - `layout asm`
      - ![image](/2023-06-02-gdb-refresher/layout_asm.png)

## Printing
- Printing the value that is stored in a variable
  - `p/my_variable`

- Printing the memory location of a variable
  - `x/1c &my_variable`
  - `x/1c my_ptr`



