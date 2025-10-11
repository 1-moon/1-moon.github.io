---
title: 'Conquer pointer'
date: 2025-09-15
permalink: /posts/2025/09/ConquerPtr/
tags:
  - Article
  - Pointer
---

## Fear 
Whenever I encounter a pointer with an asterisk(*) in a function, I always get frustrated.\
So, I'd like to conquer it - and maybe even enjoy it - unless i can avoid it altogether.\
I think working with diagrams might help me understand it better! 

## Pointers, what are you ? 
When declaring a variable, memory gets allocated for it.\
When we assign a value to a variable, the value is stored in the allocated memory.

```C++
  int p;   // memory is allocated for p, but it contains a garbage value initially
  p = 10;  // The value at p's memory address is updated to 10
```
<p align="center">
  <img src="https://github.com/user-attachments/assets/fab7fb2f-f046-47e5-9f3d-a5355a528260" width="300" />
</p>

## Pointer is a 'Variable'

A pointer is a **variable** that stores the memory address of another variable.

- All variables are stored in memory, and each byte of that memory has its own address.
- A pointer variable is usually represented as an arrow rather than a number because the actual memory address can vary depending on the system 
- Memory is made up of bytes, and each byte is assigned a unique address in sequential order.
<p align="center">
  <img src="https://github.com/user-attachments/assets/93f2c877-42f2-428d-bce4-9d727a16ec0c" width="300" />
</p>

```C++
  int  a = 100;  // Memory is allocated for a, and 100 is stored in that memory. 
  int  *p;    // Declaring a pointer that can store a memory address. 
  p = &a;
  cout << p; 
```

- The address of a variable can be extracted by **address-of operator(&)** 
  - & operator : address-of operator
  - * operator : dereference operator

### Summary for this concept 
```C++
  int a; // integer variable
  p =&a; // store address of variable into pointer 
```

```C++
*p = 200;  // Dereference operator (*) stores 200 at the address pointed to by the pointer.
```
> *p and a refer to the same memory location - in other words, they are essentially the same. 
>In nutshell, modifying *p also modifies a, since they share the same memory address. 


