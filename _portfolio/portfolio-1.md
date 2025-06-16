---
title: "Nursing AI Assistant System"
excerpt: "요양병원에서 사용되는 이동형 간호 로봇의 핵심 기능 개발<br/><img src='https://github.com/user-attachments/assets/dbaf59f4-1230-4a45-b7aa-616ddc4eaeaa' width='300' height='100'>"
collection: portfolio
---

Project period: 2025.04 ~ 2025.05
link: [요양보호사 보조 로봇](https://github.com/1-moon/ros-careGiver/tree/main)

본 프로젝트는 요양원을 배경으로, ROS(Robot OS)를 활용한 주행로봇이 요양보호사의 업무를 어떻게 보조할 수 있는지를 탐구하는 것을 목적으로 진행되었습니다.
제가 맡은 파트는 AI를 적극활용한 로봇의 기능구현 담당으로서, 어르신의 산책 보조와 순찰 및 정서적대화를 구현했습니다. 

This Project was initially launched to support caregivers with some tasks in a senior care facility, utilizing the ROS (Robot Operating System) framework.
I was responsible for developing AI-powered features such as walking assistnace, patrol functionality, and emotional interaction for elderly people 

## 모바일 로봇 
<div align="center">
  <img src="https://github.com/user-attachments/assets/cba18e75-6183-4275-9e25-5836891e04e6" width="500" />
</div>
<ul>
  <li>ROS2(Jazzy): <a href="https://docs.ros.org/en/jazzy/index.html">https://docs.ros.org/en/jazzy/index.html</a></li>
  <li>Robot Courtesy by <a href="https://pinklab.art/?page_id=5849">PINKLAB</a></li>
</ul>

## 위험상황 감지 
<div align="center">
  <img src="https://github.com/user-attachments/assets/cd75db53-d6ef-4544-aa1f-29ed19fd34d2" width="500" />
</div>

요양원에서의 비상상황을 크게 두가지를 가정하였다.
-  **쓰러짐**
-  **화재**

쓰러짐과 화재를 감지하기 위해서는 딥러닝 모델인 YOLO를 사용하였다.\
기본적으로 YOLO는 총 80개 class를 제공하지만, 쓰러짐 감지나 화재 감지처럼 특수한 상황에 맞춘 탐지를 위해서는 맞춤형 데이터셋으로 모델을 재학습(Fine-tuning)이 필요하다.\
필자는 아래와 같은 기준으로 Fine-tuning을 실시하였다. 
- Model: Yolov11 nano
- Class : 2개(Fire, Fall)
- 이미지 : 약 19,000장 by roboflow
- 학습, 검증, 테스트(7:2:1)

YOLO 모델 학습시 Parameter 값은 아래와 같이 설정 하였다. 
학습은 총 **100 epochs** 기준으로 수행\
Early Stopping을 위해 **30 patience**\
이미지 입력 크기는 **416x416**\
**Batch size 32**로 설정하여 학습 안정성과 속도 같의 균형을 고려 했다. 

아래와 같은 결과 값을 얻었다. 
<img width="1363" alt="Image" src="https://github.com/user-attachments/assets/086841a1-9023-46ec-9bed-fa8058035ffe" />

<table>
  <tr>
    <td width="50%"><img src="https://github.com/user-attachments/assets/ab39a7bf-9e4c-45b5-8937-e3d9a13f6cce"><br></td>
    <td width="50%"><img src="https://github.com/user-attachments/assets/c946b797-c03f-4f4b-9b9a-372d0a7e6756"><br></td>
  </tr>
</table>

note) YOLOv8을 쓰지 않은 이유...?\
nano모델에서 아키텍처의 큰차이가 없어 사실 성능의 큰차이는 없지만, 최신버전인 Yolo 11이 미세하게 우세.\
단순한 쓰러짐, 화재 감지라서 nano모델 이상의 더 크고 강력한 모델을 쓸 필요는 없었음.. 아쉬웠음. 

## 재활 - 산책 
<table>
  <tr>
    <td width="50%"><img src="https://github.com/user-attachments/assets/050bb257-d4b0-4d40-a96b-9316eebbc71d"><br></td>
    <td width="50%"><img src="https://github.com/user-attachments/assets/dbaf59f4-1230-4a45-b7aa-616ddc4eaeaa"><br></td>
  </tr>
</table>

산책기능을 구현하기 위해서 아래와 같은 기술을 사용하였다.
- Object dectection
이전의   
- Depth Estimation
노인과 로봇이 부딪히지 않고 일정한 간격을 두고 주어진 경로에 따라 움직여야 한다.
  
#### Person Re-ID
#### Depth Anything v2(객체 깊이 추정) 




## 정서적 대화

<div align="center">
  <iframe src="https://drive.google.com/file/d/11CfjPYbVZIDjEtyWtSgoaH126BffTP9d/preview" width="640" height="360" allow="autoplay"></iframe>
</div>
