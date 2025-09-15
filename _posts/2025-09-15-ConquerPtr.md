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
  int P;   // memory is allocated for p, but it contains a garbage value initially
  P = 10;  // The value at P's memory address is updated to 10
```
<p align="center">
  <img src="https://github.com/user-attachments/assets/fab7fb2f-f046-47e5-9f3d-a5355a528260" width="300" />
</p>
