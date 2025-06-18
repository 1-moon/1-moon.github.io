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

What is Linked List..?  
======
Linked List는 기본적으로 index가 없습니다.\
반면에, 일반적으로 우리가 알고있는 List는 메모리에서 연속적인 공간을 사용하여 데이터를 저장합니다.
예시로 아래와 같은 list를 생각해볼 수 있습니다.
<img width="300" alt="image" src="https://github.com/user-attachments/assets/fe741643-e78f-49a0-9c88-2df4fb3fedaf" />\
하지만 Linked list의 경우 각 node들이 memory안에서 무작위로 공간을 차지 하고 있을겁니다.\
각 노드가 **포인터**를 통해 다음 요소와 연결되기 때문에 index가 필요 없는 것이죠..!
<img width="500" alt="image" src="https://github.com/user-attachments/assets/e08122f7-ec35-4fcc-8871-d28e380c3e5d" />

실제 메모리 상에서 Linked list를 본다면 어떨까요?\
<img width="500" alt="image" src="https://github.com/user-attachments/assets/5ac888aa-1716-4e3d-a623-33584800924a" />


Big O
======
