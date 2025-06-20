---
title: 'What Happens When You Run Hello World?'
date: 2025-06-20
permalink: /posts/2025/06/Helloworld/
tags:
  - Article
  - Compiler
---

Link: [What Happens When You Run Hello World?](https://medium.com/code-like-a-girl/hello-world-what-happens-when-you-run-this-9da52a99cc98)\
평소 구독하고 있는 [Medium](https://medium.com/) 에서 우연히 재미있는 article이 있어 가져와 봤다.

처음 프로그래밍을 접할때, 'Hello world'를 print하는 것부터 시작한다.\
우리는 단순히 IDE에서 Run을 통해 compile하면, 단순히 "Hello world"를 출력하지만 실제로 어떤 원리를 통해 print되는지 모른다.\
Compiling에 대해 한번이라도 공부한 사람은 알지만, 다시 복습차원에서 살펴보면 좋을거 같아서 가져와 봤다.

# What happens when you run 'Hello world'
프로그래밍을 시작할때, 아마도 독자는 Visual Studio를 설치했거나 online editor를 열어보셨을 겁니다.\
만약, 학교에서 저처럼 Borland Turbo C++를 배우셨다면 저처럼 매우 고통스러운 나날이셨을 겁니다.
> Borland Turbo C..?\
> 1990년대에 많이 쓰였던 C 개발 환경, 요즘 기준으로는 사용하기 불편하고 제한적인 부분이 많음\
> 현재는 단종. 자세한 내용 [wiki](https://en.wikipedia.org/wiki/Turbo_C%2B%2B)
어쨌든, 아래와 같은 코드를 다들 생각하고 계실겁니다.
```
  #include <iostream>
  
  using namespace std;
  
  int main() {
      cout << "Hello, World!";
      return 0;
  }
```

## IDE or Your Code Editor 
어떤 것이든 코드를 진행하기에 앞서, 이 코드를 담을 그릇이 필요합니다.\
그 그릇은 우리는 흔히 IDE(Integrated Development Environment) or code editor라 부릅니다.\
![image](https://github.com/user-attachments/assets/4bc57ee2-47f9-451e-a704-4f0038b1797a)\
만약 위 그림과 같은 VS, Code::Blocks 또는 온라인 컴파일러를 쓴다면, 아래와 같은 이점들을 제공합니다\
- 코드를 깔끔하게 쓰거나 편집할 수 있는 Interface를 제공합니다
- 문법 highlighting, 자동완성 그리고 실시간 오류감지
- 유저가 직접 *Compiler* 와 *Linker* 과 같이 기계어로 변환 설정할 필요 없이 IDE가 자동으로 설정하고 실행합니다.

기본적으로 IDE는 코드 자체를 실행하지는 않습니다. 대신..
- 코드를 준비하고
- 정리한 다음
- 그 뒤에서 Compiler와 linker를 호출합니다.

## Compiler 
컴퓨터는 오직 0 또는 1로만 이루어진 기계어(Machine code)만을 이해할 수 있습니다. \
컴파일러의 역할은 아래와 같습니다.(독자가 사용하는 언어를 C++로 가정해봅시다)\
- `.cpp` 파일을 기계어로 변환합니다
- 오류를 확인합니다
- 실행 파일을 생성합니다.(.exe)

바로, 이 실행 파일(executable file)이 OS가 실제로 실행하는 것입니다.\
compiler에 대해서 더 자세한 article은 [여기](2025-06-20-Compiler)를 참고해주세요.


![image](https://github.com/user-attachments/assets/f0a8a7d0-1b14-4663-87a3-60e9b21f6d8e)












