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
![image](https://github.com/user-attachments/assets/4bc57ee2-47f9-451e-a704-4f0038b1797a)

만약 위 그림과 같은 VS, Code::Blocks 또는 온라인 컴파일러를 쓴다면, 아래와 같은 이점들을 제공합니다.
- 코드를 깔끔하게 쓰거나 편집할 수 있는 Interface를 제공합니다
- 문법 highlighting, 자동완성 그리고 실시간 오류감지
- 유저가 직접 *Compiler* 와 *Linker* 과 같이 기계어로 변환 설정할 필요 없이 IDE가 자동으로 설정하고 실행합니다.

기본적으로 IDE는 코드 자체를 실행하지는 않습니다. 대신..
- 코드를 준비하고
- 정리한 다음
- 그 뒤에서 Compiler와 linker를 호출합니다.

## Compiler 
컴퓨터는 오직 0 또는 1로만 이루어진 기계어(Machine code)만을 이해할 수 있습니다. \
컴파일러의 역할은 아래와 같습니다.(독자가 사용하는 언어를 C++로 가정해봅시다)
- `.cpp` 파일을 기계어로 변환합니다
- 오류를 확인합니다
- 실행 파일을 생성합니다.(.exe)

바로, 이 실행 파일(executable file)이 OS가 실제로 실행하는 것입니다.\
compiler에 대해서 더 자세한 article은 [여기](2025-06-20-Compiler)를 참고해주세요.


![image](https://github.com/user-attachments/assets/f0a8a7d0-1b14-4663-87a3-60e9b21f6d8e)


## Linker
만약 `iostream`과 같은 표준 라이브러리 혹은 외부 라이브러리 사용시, Linker는 아래와 같은 역할을 합니다. 
- 라이브러리를 찾습니다.
- 필수적인 코드들을 합칩니다.
- 모든 것들이 올바른 장소에 있는지 확인합니다
다른 파일이나 라이브러리를 통해서 선언된 함수나 변수를 연결(resolve)합니다.\
예를들어 iostream의 `cout`같은 것을 쓸수있게 하는 것이라 보면 될거 같습니다!\
즉, 코드상에서 `cout` 부를떄, 스크린을 통해 무언가를 print 하게 될텐데 linker가 그게 정확히 어떤 동작을 하는지, 어떤 라이브러리에 정의되어 있는지를 정확히 찾아서 연결해준다는 의미입니다.
 
![image](https://github.com/user-attachments/assets/c8244210-25f2-4f6e-95cf-7bf55a65a487)

## Code 
`#include <iostream>` 이 코드 한줄은 Compiler에게 **iostream** library를 포함시키라 요청합니다. 
- cout: screen에 결과값을 보여줍니다.
- cin: 사용자로부터 입력값을 받습니다.
이 코드 한줄 없다면, `cout`을 당연히 사용할 수 없겠죠..?

이 문장을 한번 생각해봅시다.
> "저기, C++아 keyboard나 screen와 이야기할 수 있는 통로가 필요해..."

![image](https://github.com/user-attachments/assets/bb0d15ed-f1f8-451c-b09f-ae73dd6d876f)

#### Using namespace std;
C++는 `std`라는 namespace를 통해 `cout`, `cin`, `string` 같은 표준 기능들을 구성하고 관리합니다.\
C++에서의 namespace는 변수나 함수 그리고 클래스와 같은 것들을 하나의 이름안에서 그룹화하는 역학을 하죠.\
한마디로 이름의 혼동을 줄이기 위해 일종의 폴더를 만들어 안에 넣어서 관리한다고 생각하시면 됩니다.\
`cout`을 사용하기 위해서는 아래와 같이 사용할것입니다. 
```
  std::cout << "Hello, World!";
```
만약 `std`를 사용하게된다면, `std::`를 생략이 가능합니다.
```
  cout << "Hello, World!";
```
#### `std` for only beginner ? 
`std`를 쓰는건 정말 편리합니다. 하지만... 실제 큰 프로젝트에서는 사용을 권장하지는 않습니다. 이유는 아래와 같아요.
- `std` namespace는 정말 많은 이름들을 가지고 있습니다.
- 사용자가 작성한 변수, 함수, 라이브러리는 같은 이름을 사용함으로써 **충돌(conflict)**를 발생시킬 위험이 있습니다.
- 코드의 사이즈가 커지면 커질수록 유지보수나 에러를 잡기가 어려워집니다.
따라서 `std::`를 직접 쓰는게 권장됩니다. 특히 개인이 아닌 큰 프로젝트에서는 더더욱..!
> Explicit. Clear. Safe.

#### int main(){...}
위 소제목은 C++ 프로그램의 시작점이라 볼 수 있습니다.
`main`함수는 항상 프로그램이 시작될때 첫번째로 시작되는 컴파일됩니다. 

#### cout << "Hello, World!";
이것은 screen상에 출력문입니다.
- `cout`은 콘솔결과를 의미합니다.
- `<<`은 삽입 연산자(insertion operator)입니다. 즉, 문자열을 cout에 보내는 역할을 하죠
결과는...
```
  Hello, World!
```
여기서 우리가 screen상에서 말하고 있는 부분은 `terminal`, `console` 또는 `standard output` - aka `stdout`입니다. 
```
  "Hello, World!"
   ↓
  << (insertion operator)
   ↓
  stdout (console screen)
```

#### return 0;
이것은 main 함수의 끝이며 OS에게 이 프로그램이 성공적으로 끝냈다라는 것을 말해줍니다.\
![image](https://github.com/user-attachments/assets/c2fbd808-43b4-4dc4-b08b-1373f8b65093)

## Execution - Hello, World! 
IDE에서 Run 혹은 Compile & Run 버튼을 누르면 - 그때, 아래와 같은 모든 것들이 실행됩니다.  
- `.cpp`파일은 기계어로 컴파일됩니다. 
- Linker가 곧바로 모든 것들을 이어붙입니다.
- 그리고 재탄생 -> 당신의 프로그램이 `.exe`파일 형태로 OS를 통해 실행가능한 파일로 만들어집니다.

![image](https://github.com/user-attachments/assets/0eb4f4a6-307c-4f28-bd56-56e4d2d8a82a)

마침내 마지막 출력까지 도달했습니다.
1. OS는 프로그램을 memory상에 올려놓습니다.
2. main 함수로 부터 실행합니다.
3. `cout << "Hello, World!";` 는 결과값을 `stdout`에 보냅니다.
4. Screen에 Hello, World!가 출력됩니다.  

![image](https://github.com/user-attachments/assets/f55c58ac-61dd-4709-abbc-8a400f71c533)

## Summary 
방금 첫번째 C++언어 코드를 완성했고 최소한의 이해를 하십겁니다..!
```
  [main.exe] 
    ↓
  OS loads program into memory
    ↓
  main() runs
    ↓
  cout sends text to stdout
    ↓
  "Hello, World!" appears on screen
```








