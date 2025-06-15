---
title: "BST(이진탐색트리)"
collection: studying
type: "Data Structure"
permalink: /studying/BST
# venue: "Home"
date: 2025-06-15
# location: "City, Country"
---

Binary Search Tree\
Requirement: [연결리스트(Linked list)](LinkedList.md) 

What is BST..?  
======

이진 트리의 한 종류로서, 각 노드는 최대 두 개의 자식 노드를 가지며, 아래와 같은 특징을 갖습니다. \
- 왼쪽 subtree에는 현재 node보다 작은 값만 위치합니다
- 오른쪽 subtree에는 현재 node보다 큰 값만 위치합니다.

How to implement..?  
======

Tree 형태를 가지고 있는 간단한 Linked list를 준비합니다.\
<img width="300" alt="Image" src="https://github.com/user-attachments/assets/16bf92bf-515f-4d8e-a373-544cc8b2e3dd" />\
여기서 기억해야 할 것은 위 그림의 노드 형태는 아래와 같은 형태를 가지고 있습니다.
```
  "value": 4,
  "next": None
```

여기서 Binary tree로의 변행을 위해서는 2개의 화살표가 자식노드를 가리켜야 합니다.\
<img width="300" alt="Image" src="https://github.com/user-attachments/assets/19b709ce-1e27-40ec-b4ff-17f32fc1e96b" />\
위 그림의 노드 형태는 자연스럽게 아래와 같은 형태를 띕니다.
```
  "value": 4,
  "left": None,
  "right": None
```

이제부터, 왼쪽 오른쪽 subtree에 value 값을 넣게 된다면. 예시로 아래와 같은 그림을 생각해 볼 수 있습니다.\
<img width="500" alt="Image" src="https://github.com/user-attachments/assets/9793ac33-3a77-4aed-82aa-e6b9b1fcfda3" />\
그렇다면, 자연스럽게 이 tree를 dictionary 
