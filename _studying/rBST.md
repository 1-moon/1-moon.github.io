---
title: "rBST(재귀적 이진탐색트리)"
collection: studying
type: "Algorithm"
permalink: /studying/rBST
# venue: "University 1, Department"
date: 2025-06-10
# location: "City, Country"
---
{% include toc %}

Recursive Binary Search Tree\
Requirement: [이진탐색트리(Binary Search Tree)](BST.md) 

What is Recursive BST..?  
======
재귀적(recursive) + 이진탐색트리(Binary Search Tree)\
대부분의 탐색 알고리즘은 반복문(iterative loop)를 통해 구현되는 경우가 많습니다다. \
하지만 BST의 경우 구조자체를 recursive하게 직관적으로 구현이 가능합니다.

Contain
======
```
    def contains(self, current_node, value):
```
이처럼 node pointer와 value값을 input으로 받는 한번만 불리는 보통의 contain method와 달리\
contain method에 또다른 method를 calling을 할 것입니다. 

```
    def r_contains(self, value):
        return self.__r_contains(self.root, value)
```
rBST의 contain은 value값만 받는다. 
`__r_contain` 의 underscore을 앞에 붙이는 이유는 Python의 접근 제어 디자인 패턴으로, OOP 코딩스타일로 따지자면 Private 역할을 한다고 볼 수 있습니다.\
`__r_contain` 함수를 구현을 할떄 첫번째로 생각해야 할 것은 BST가 Empty(비어있음)인지 아닌지 판단해야 합니다. \
```
    def __r_contains(self, current_node, value):
        if current_node == None:
            return False
```

그렇다면, tree안에 내가 찾고자 하는 value값이 root에 있다면..? 
```
    def __r_contains(self, current_node, value):
        if current_node == None:
            return False
        if value == current_node.value:
            return True 
```
여기서 부터 고민을 해야한다. 예를들어\
<img width="203" alt="Image" src="https://github.com/user-attachments/assets/9f4c22c8-e8ab-4f93-b2b8-ac13cb2f595d" /> \
tree가 이렇게 51->30의 구조로 이루어져있다고 가정하고 value값이 '30'인 node를 찾는다고 한다면..?

`r_contain` method가 호출될때는 처음 root node(51)에서 시작합니다. \
call stack을 생각해본다면 \
<img width="141" alt="Image" src="https://github.com/user-attachments/assets/224eed09-4f0c-4e38-ba24-f6246922c77b" /> \
'51' instance는 call stack에 들어있을 것이고, `r_contain(30)` 을 통해서 해당 node를 재귀적으로 찾는 코드를 더해야합니다. 
```
    def __r_contains(self, current_node, value):
        if current_node == None:
            return False
        if value == current_node.value:
            return True 
        if value < current_node.value:
            return self.__r_contains(current_node.left, value) 
```
30 < 51 에 의해 '30'도 call stack에 들어가게 될것입니다. \
<img width="124" alt="Image" src="https://github.com/user-attachments/assets/1a4888fe-009e-46f6-8cd0-7110d1185aa0" /> \
call stack에 들어간 30은 반환된 True로 인하여 다시 빠져나오게 되고,  `self.__r_contains(current_node.left, value)`이 값은 True로 변환되어\
남아있던 51도 call stack으로 부터 빠져나가게 됩니다.\

마지막으로 BST는 오른쪽 노드도 훑기 때문에.. left와 right모두 생각을 해야 합니다..!
```
    def __r_contains(self, current_node, value):
        if current_node == None:
            return False
        if value == current_node.value:
            return True 
        if value < current_node.value:
            return self.__r_contains(current_node.left, value) 
        if value > current_node.value:
            return self.__r_contains(current_node.right, value) 
```

최종적으로 '30'은 BST에 포함되어 있다는 것을 우리는 알 수 있습니다.
```
    def r_contains(self, value):
        return True 
```

Insert
======
`r_contain`와 큰 차이점은 `r_insert`은 return statement를 반환하지 않기 때문에 약간 다르다. 
```
    def __r_insert(self, current_node, value):

    def r_insert(self, value):
        self.__r_insert(self.root, value)

    def r_contain(self, value):
        return self.__r_contain(self.root, value)
```
return 을 반환하지 않는 다면 어떤점이 contain과 다른지 살펴보자.\
<img width="300" alt="image" src="https://github.com/user-attachments/assets/0e489ca4-16b0-4b4c-a9aa-53c81b9de199" />
<img width="300" alt="image" src="https://github.com/user-attachments/assets/c1c74940-1056-4648-895b-82fcff6845cb" />
우선 위 그림과 같이 root instance 를 call stack에 넣고 시작하면, 
```
    def __r_insert
```

