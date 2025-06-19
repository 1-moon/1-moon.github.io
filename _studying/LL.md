---
title: "LL(연결 리스트)"
collection: studying
type: "Data Structure"
permalink: /studying/LL
# venue: "Home"
date: 2025-06-17
# location: "City, Country"
---

{% include toc %}

Liked List\
Requirement: [리스트(List)](List.md) 

# What is Linked List..?  

Linked List는 기본적으로 index가 없습니다.\
반면에, 일반적으로 우리가 알고있는 List는 메모리에서 연속적인 공간을 사용하여 데이터를 저장합니다.\
예시로 아래와 같은 list를 생각해볼 수 있습니다.\
<img width="300" alt="image" src="https://github.com/user-attachments/assets/fe741643-e78f-49a0-9c88-2df4fb3fedaf" />\
하지만 Linked list의 경우 각 node들이 memory안에서 무작위로 공간을 차지 하고 있을겁니다.\
각 노드가 **포인터**를 통해 다음 요소와 연결되기 때문에 index가 필요 없는 것이죠..!
<img width="500" alt="image" src="https://github.com/user-attachments/assets/e08122f7-ec35-4fcc-8871-d28e380c3e5d" />

실제 메모리 상에서 Linked list를 본다면 어떨까요?\
<img width="500" alt="image" src="https://github.com/user-attachments/assets/5ac888aa-1716-4e3d-a623-33584800924a" />


# Big O

### 1)Append
<img width="500" alt="image" src="https://github.com/user-attachments/assets/60fb22f0-6f48-40ad-9323-e1f5b15bf854" />

**This is O(1)**\
It doesn't matter how many nodes we have in the list, the number of operations to add it to the end is exactly same. 
  
### 2)Remove
<img width="500" alt="image" src="https://github.com/user-attachments/assets/1d0ff8ec-279e-43b6-b9a8-5abfb6392cf4" />\
when we are removing from the end of a linked list, it's more complicated than `append`

**This is O(n)**\
In order to get to the node `7`\
we should follow a set of pointers.\
head -> 5 -> 1 -> 21 -> 7 

### 3)Add an item on the front
<img width="500" alt="image" src="https://github.com/user-attachments/assets/0bbdf698-051b-476c-86a2-8e972af9c8d8" />\
It doesn't matter how many items we have in the list.\
It's going to be the same number of operations to add an item on the front of the list.

**This is O(1)**

### 4)Remove an item on the front
Once again this is gonna be **O(1)** because it doesn't matter how many items we have in the list.\
It's the same number of operations to remove that. 

### 5)Add an item somewhere in the middle of the list
<img width="500" alt="image" src="https://github.com/user-attachments/assets/627142af-a08b-4dd1-aae4-f451d1e778f6" />\
Let's say we're going to insert that `4` after the `21` node.

In order to find that node, we have to start at the head and iterate through the list until we get to that `21` node.\
<img width="500" alt="image" src="https://github.com/user-attachments/assets/0e2caf96-b9f2-441a-9224-33051467e619" />

**This is O(n)**

### 6)Remove an item somewhere in the middle of the list
Once again we had to iterate through the list.\
Same as adding, so **O(n)**

Implementation
======
