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
### Object dectection
노인을 인지하기 위해서는 반드시 이 기술이 필요하다.\
위험상황 감지시 사용했던 YOLO 11 nano model을 사용했으며, YOLO 모델은 기본적으로 '사람'을 감지하도록 이미 훈련이 되어있기에\
모델의 기본 성능을 이용하였다.
#### Re-Identification 
요양원 환경에서는 많은 사람들이 오고 가기 때문에, 특정 노인을 지속적으로 추적하는 것이 중요하다.\
이를 위해 색상 및 체형 정보를 기반으로 어르신의 특징을 저장한 후, 특징 벡터를 생성하여 유사도를 비교하는 방식으로 재식별(ReID)을 구현을 했었음.
유사도 비교는 크기와 색상 정보를 결합한 압축된 특징 벡터를 사용하며, Cosine 유사도를 활용해 두 벡터 간 유사도를 측정.\
또한, 최대 90 프레임 내외에서 일정한 유사도 임계값을 설정하여, 임계값 이상일 경우 같은 ID로 재식별하도록 구현을 했었음.

note) 딥러닝 기반의 임베딩 특징을 활용하는 방법도 있다고는 들었는데, 프로젝트 기간상 비교는 하지 못해 매우 아쉬웠음. 

### Depth Estimation
노인과 로봇이 충돌하지 않도록 일정한 간격을 유지하며 주어진 경로를 따라 이동하는 것이 핵심이다.\
이를 위해 Stereo 카메라 또는 단일 카메라를 사용할 수 있지만, 예산상의 제한으로 인해 단일 카메라 기반의 Depth Estimation 기술을 활용하여 실시간 거리 정보를 추정하도록 하였다.\
로봇의 전면 카메라는 장애물 감지등 다른 영역에서 사용하기에 추가로 후면 카메라를 활용해 간격을 유지하도록 하였다.  
#### Depth anything v2 
딥러닝 기반 Depth Estimation 모델들이 여러 있다. 예를들어 *MiDaS, DenseDepth* 등 여러 있어지만, 홍콩대학교 연구팀이 개발한 모델 *Depth Anythong v2*를 사용하였다.
이유는 **Hugging Face**의 Transformers 라이브러리를 통해 모델을 간편하게 로드하여 실행할 수 있고 별도의 모델 학습 없이 바로 실험해 볼 수 있어서 큰 장점이었음. 
기본적으로 딥러닝 기반 모델은 많은 행렬 연산을 수행하기에 GPU 가속(CUDA) 적용하는게 CPU로 돌리는 것보다 훨씬 좋은 실시간 처리 성능을 확인 해볼 수 있어서 좋았음.
 
note) Stereo camera를 이용하여 Disparity Map 깊이 추정하는 방법이 있어, 다른 방식을 활용해볼 기회를 놓쳐서 아쉬웠음. 
 l
## 정서적 대화
<div align="center">
  <iframe src="https://drive.google.com/file/d/11CfjPYbVZIDjEtyWtSgoaH126BffTP9d/preview" width="640" height="360" allow="autoplay"></iframe>
</div>

요양원 환경에서는 단순한 이동뿐만 아니라 **어르신과의 상호작용**이 중요한 역할을 한다. 따라서 **대화 기능**을 추가하도록 노력하였다. 
처음 구상은 Pre-trained 된 ollma or deepseek같은 모델을 활용하여 요양원 환경에 최적화된 Fine-tuned 모델 사용과 RAG를 적용시켜 단순한 AI응답 말고, 실제 요양원 시간표 및 생활 정보와 연계하여 반응하도록 하려고 했다. 하지만 크게 아래와 같은 제약들이 있었음.\
- HW 성능 제한, 3060 6GB laptop GPU를 사용하다 보니 QLORA를 활용한 모델 학습 자체도 돌아가지 못했음\
- 데이터 부족 및 전처리, 어르신과의 충분한 대화 데이터가 필요하지만 많이 없었고, 기본 대화 조차도 전처리를 했어야 하다보니 시간상 여유가 없었음.

이런 제약을 고려해서 차선책이었던, API를 적극활용하기로 하였음.\
- STT (Google Cloud Speech API): 실시간 음성 인식을 활용해 노인의 말을 받아들이고
- LLM (OpenAI API) with context history: 문맥을 이해하고 감정을 반영하여 GPT 기반 응답을 생성
- TTS (Google Text-to-Speech API): 생성된 응답을 음성으로 변환하여 전달
특히 LLM 같은 경우 대화 문맥을 이해하고 답변을 해야하기에 Json 파일로 이전 대화 histroy 를 축적하도록 구현을 하였고, Prompt를 작성하여 요양원 환경에 맞게 커스텀마이징을 하였음.
ROS 통신을 통해 PC가 아닌 로봇을 활용해야 하다 보니 LLM 을 PC 서버쪽으로 돌리고 STT와 TTS를 로봇쪽에서 처리하도록 구현하였음.\
Reference: https://github.com/Auromix/ROS-LLM/tree/ros2-humble 

