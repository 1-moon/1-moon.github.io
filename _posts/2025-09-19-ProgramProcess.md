---
title: 'How program works?'
date: 2025-09-19
permalink: /posts/2025/09/blog-post-4/
tags:
  - Knockledge
  - Process
  - Operating System 
---

While I am doing programming and typeing code, I found myself i need to know the mechanism that how my code is interpreted and works on HW.\ 
So, I will organise the process works on when my code goes through hardware, memory and CPU. 

# How a program works on computer? 
<p align="center">
  <img src="https://github.com/user-attachments/assets/6ee44dc0-2a9d-4687-8cd3-61608c59c40c" width="80%" alt="Image" />
</p>

As we all know, when we run and build a "Hello World!", the message is priented to the ouput stream\ 
But how does that work? Can you explain it? At first, I couldn't easily tell who was a newbie.

이 문자열은 우리가 코드를 빌드할때 실행파일 어딘가에 함께 저장이 된다. 
실행파일은 보통 하드디스크에 저장이 됩니다.
hello world라는 문구는 실행파일에 포함된 상태로 하드디스크에 보통 저장이 된다. 
프로그래머나 사용자가 실행파일을 실행을 시키겠다고 한다면 운영체제에 요청을 하게되면 
운영체제는 하드디스크로 부터 실행파일을 읽어 메모리에 집어 넣습니다. 이 운영체제는 다시 cpu에게 명령을 내린다.
메모리의 어떤 위치에, 즉 helloworld가 저장된 위치에 읽어다가 시키는대로 한줄 한줄 실행시켜라라고 명령을 내린다.
그러므로 cpu는 os가 시키는대로 메모리에 있는 프로그램을 한줄한줄 실행을 시키게 되고 그 명령어중에 helloworld를 화면에 출력하라라는 명령이 있으면 
화면에 출력을 하게됨 

코드를 빌드하는것도 미리 만들어져있는 컴파일러를 사용하게되고 프로그램을 실행시키는 중간 과정도 거의 운영체제가 알아서 해결해 주게됨 
코딩테스트를 준비할때도 메모리와 cpu가 어떻게 일을 해서 어떻게 내가 원하는 결과를 만들어 낼 수 있을지에 집중하여 공부를 하면서 해결해나가야 한다. 

# Memory 
<p align="center">
  <img src="https://github.com/user-attachments/assets/ab069d38-b89a-45e3-b272-a54e1c8da9ee" width="80%" alt="Image" />
</p>
컴퓨터에서 가장 중요한게 뭐냐 물어보면 cpu라 대답하는 사람이 많을거라 생각
틀린말은 아니지만, 예전에 컴퓨터를 배운사람들은 cpu에게 명령을 어떻게 내리는지에 집중
요즘 cpu가 발전을 많이 해서 빨라졌고, 우리가 작성하는 프로그래밍언어를 컴퓨터가 실행시킬 수 있는 형태로 바꿔주는 컴파일러 성능도 아주 많이 좋아졌기에 
최근에는 프로그래밍을 잘한다 효율적인 프로그래밍을 만든다고 하면 cpu보다는 memory쪽이 더 중요하지 않나 특히 자료구조를 메모리 안에 잘 만드는게 중요하다고 생각함 
결과적으로는 둘다 능숙하게 사용하는게 키포인트
일단 용어에 친숙해 질 필요가 있음.
메모리안에 데이터가 어떤식으로 저장되는지부터 살펴보자 
레이아웃은 집의 도면같은거라 생각하면서 메모리안에 어떤데이터가 어떤 방식으로 저장이 되는지를 보는 그림 
크게 네가지 
text segment -> cpu에게 명령을 내리는 명령어들이 저장되는 장소
data ->명령어가 아니라 데이터에 해당하는 부분
메모리를 두가지로 저장 
stack -> 미리 잡아 놓는 공간 -> 내부적으로 stack이라는 자료구조를 사용하기 때문에 네이밍
heap -> 우리가 미리 크기를 알수 없는 경우 
전화번호부를 만들때 회원수가 100명에 해당하는 
동적으로 다이나믹은 힙 
stack은 최대사용량이 정해져있기때문, 재귀호출에 의해 stack을 너무 많이 사용하게 되버리면 그때는 stack over flow 오류가 날거임 
heap은 컴퓨터 사양에 따라 거의 무제한으로 사용가능 운영체제가 가상으로 커다란 메모리가 있는것처럼 관리를 하기때문에

프로그램을 실행할때 메모리를 어떤식으로 사용하는지 좀더 구체적으로 알아봤음 



