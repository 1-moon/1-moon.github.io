---
title: "BST(이진탐색트리)"
collection: studying
type: "Data Structure"
permalink: /studying/BST
# venue: "Home"
date: 2025-06-15
# location: "City, Country"
---
{% include toc %}

Binary Search Tree\
Requirement: [연결리스트(Linked list)](LinkedList.md) 

What is BST..?  
======

이진 트리의 한 종류로서, 각 노드는 최대 두 개의 자식 노드를 가지며, 아래와 같은 특징을 갖습니다. 
- 왼쪽 subtree에는 현재 node보다 작은 값만 위치합니다
- 오른쪽 subtree에는 현재 node보다 큰 값만 위치합니다.

Mechanism && Terminology 
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
그렇다면, 자연스럽게 이 tree를 dictionary형태로 바꿔 본다면.. 
```
  "value": 4,
  "left": {
            "value": 3,
            "left": None,
            "right": None
          },
  "right": {
            "value": 15,
            "left": None,
            "right": None
           }
```

이런식의 형태로 구성된다는 것을 알 수 있습니다. 이어서 또 다른 subtree를 아래와 같이 만들 수 있습니다.\
<img width="500" alt="Image" src="https://github.com/user-attachments/assets/9472ff11-ae6d-477a-a515-ff2344568e5d" />\
여기서 부터는 BST의 형태를 구분하는 용어를 정리 할 필요가 있습니다.

위 그림과 같은 tree는 모든 Node가 두개 혹은 None을 가르키고 있기 때문에 우리는 'FULL' tree 라고 할 수 있습니다.
### *Full binary tree는 모든 노드가 자식 노드를 0개 또는 2개 가지고 있는 트리*

반면에 아래와 같은 그림의 BST는 어떨까요? \
<img width="500" alt="image" src="https://github.com/user-attachments/assets/393ddc6f-1cb5-4042-bd23-46f7bd9f557b" />\
더이상 'FULL' tree라고 볼 수 없습니다. '7' node가 '2'라는 node를 하나만 subtree로 가지고 있기 때문입니다.

다시 돌아가서, 아래와 같은 'Full' tree는 또한 'Perfect' tree입니다.\
<img width="500" alt="Image" src="https://github.com/user-attachments/assets/9793ac33-3a77-4aed-82aa-e6b9b1fcfda3" />\
tree의 모든 층이 완벽히 node가 들어 있기 때문입니다.
### *Perfect binary tree는 자식 노드를 정확히 2개씩 가지고 있고 동일한 깊이에 있는 트리*

<img width="500" alt="image" src="https://github.com/user-attachments/assets/6f9a7e74-61f3-42f4-95a3-798407904d4a" />\
위 그림의  Full tree또한 Perfect tree라고 할 수 있습니다.\
다시 돌아가 아래 그림의 BST는 어떨까요? \
<img width="310" alt="image" src="https://github.com/user-attachments/assets/d437cd64-8b6f-49c1-957e-dfa9b2d953ee" />\
더이상 'Perfect' tree라고 볼 수 없습니다. 하지만 여전히 'Full' tree 입니다.\
아래 그림으로 한번더 돌아가서, 우리는 아래 그림을 Full, Perfect tree라고 부르고 또 'Complete' 하다고 말할 수 있습니다. 
<img width="500" alt="image" src="https://github.com/user-attachments/assets/6f9a7e74-61f3-42f4-95a3-798407904d4a" />\
그렇다면, 아래와 같은 트리는 어떨까요?\
<img width="500" alt="image" src="https://github.com/user-attachments/assets/95f31dee-fac8-4ea5-b50b-411a13284732" />\
위 그림의 BST는 더 이상 Full 하지도 않고 Perfect하지도 않습니다. 하지만, Complete BST라고 할 수 있습니다.\
왜냐하면 tree가 왼쪽부터 오른쪽으로 순서에 맞게 채워지고 있다고 판단하고 있기 때문이죠..!\
여기서 또 한번 물어볼게요. 아래와 같은 Tree는 어떤 tree 인가요?

<img width="500" alt="image" src="https://github.com/user-attachments/assets/db5d4a89-3049-4d0c-9099-0d7f6082662b" />\
모든 노드가 2개 or o개 를 가지고 있기 때문에 Full binary tree이면서 동시에 Complete binary tree라고 할 수 있습니다. 하지만 Perfect하지는 않습니다.

아래와 같은 tree는 어떨까요? 

<img width="500" alt="image" src="https://github.com/user-attachments/assets/3ce4edbd-d59a-417f-af26-2d6c451d2340" />\
Full, Perfect, Complete binary tree라는 것을 우리는 알 수 있습니다.
### *Perfect binary tree는 마지막 깊이를 제외한 모든 node가 채워져있고, 마지막 깊이의 node들은 왼쪽부터 오른쪽으로 순서대로 채워지는 트리*

또한 마지막 깊이의 node 즉, 자식 node를 갖지 않는 노드들을 우리는 **리프(leaf)** node라고 합니다.
<img width="500" alt="image" src="https://github.com/user-attachments/assets/3199ba13-6c48-424a-9fd4-a12369282a10" />




