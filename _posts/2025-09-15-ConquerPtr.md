
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
  <img src="https://github.com/user-attachments/assets/93f2c877-42f2-428d-bce4-9d727a16ec0c" width="500" />
</p>

```C++
  int  a = 100;  // Memory is allocated for a, and 100 is stored in that memory. 
  int  *p;    // Declaring a pointer that can store a memory address. 
  p = &a;
  cout << p; 
```

- The address of a variable can be extracted by **address-of operator(&)** 
  - & operator : address-of operator
  - \* operator : dereference operator

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



## Pass by pointer 
Pointers can be parameters in a function.

```C++
  void update(int *p){
    *p = 20; 
  }

  int main(){
    int c = 10;
    update(&c);  // address of c 
    cout << c;   // Prints 20 
  }
```

<p align="center">
  <img src="https://github.com/user-attachments/assets/75dd9362-2231-449e-8e2a-1b15a8950b49" width="700" />
</p>

- Instead of passing `c`, we passed its address(&c)
- Inside the function, `*p = 20;` modified the value at the memory address stored in `p`
- Since `p` points to `c`, `c` is updated directly  

The pointer variable `p` has its own memory address. 


## Pass by Reference (Alternative to Pointer)

C++ allows you to pass variables by reference, unlike C. This is similar to using pointers, but cleaner.
```C++
  void update(int &r){
    r = 20; 
  }

  int main(){
    int c = 10;
    update(c);  // address of c is passed
    cout << c;  // Prints 20 
  }
```
No need to use `*` to access the value - `c` is modified directly. 

<p align="center">
  <img src="https://github.com/user-attachments/assets/c45f089c-a02b-4798-b660-075161630d34" width="700" />
</p>

If you pass by reference, you have to **make sure that the variable will never be null.** \
If you think it might be null, then pass it as a pointer.


## Handling `nullptr` in pointers
When using pointers, there's always a risk that might not point to a valid memory location.\
If you try to dereference a `nullptr`(a pointer that doesn't point to anything), your program always exhibits undefined behavior.\

To prevent this, always check if a pointer is `nullptr` before dereferencing it:

```C++
  void  update(int *p){
    if (p == nullptr) return; // Avoid dereferencing a null pointer
    *p = 4; // Safe to modify the value now
  }
```

## Final Thoughts
Pointers are tricky, but once you understand memory addresses and references, they become powerful tools for optimizing code.

Whether you’re managing dynamic memory, passing large objects efficiently, or working with data structures like linked lists, pointers are essential in C++.

