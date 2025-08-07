---
title: "Nursing AI Assistant System"
excerpt: "요양병원에서 사용되는 이동형 간호 로봇의 핵심 기능 개발<br/><img src='https://github.com/user-attachments/assets/dbaf59f4-1230-4a45-b7aa-616ddc4eaeaa' width='300' height='100'>"
collection: portfolio
---

Project period: 2025.04 ~ 2025.05
link: [요양보호사 보조 로봇](https://github.com/1-moon/ros-careGiver/tree/main)
<div align="center">
  <img src="https://github.com/user-attachments/assets/885951dd-7ec7-4e69-9baa-d252f889d720" width="500" />
</div>

본 프로젝트는 요양원을 배경으로, ROS(Robot OS)를 활용한 주행로봇이 요양보호사의 업무를 어떻게 보조할 수 있는지를 탐구하는 것을 목적으로 진행되었습니다.
제가 맡은 파트는 AI를 적극활용한 로봇의 기능구현 담당으로서, 어르신의 산책 보조와 순찰 및 정서적대화를 구현을 했었고, 기타 트러블 슈팅 및 디버깅을 함께 진행했었습니다.

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

요양 보호사를 대신하여 여러 업무중 위험상황을 감지할 수 있는 서비스가 필요하다고 판단하였고,\
실내에서 발생할 수 있는 비상상황을 크게 두가지를 가정하고 진행하였습니다. 
-  **쓰러짐**
-  **화재**

쓰러짐과 화재를 감지하기 위해서는 딥러닝 모델 YOLO를 활용하여 진행.\
기본적으로 YOLO는 총 80개 class를 제공하지만, 쓰러짐 감지나 화재 감지처럼 특수한 상황에 맞춘 탐지를 위해서는 맞춤형 데이터셋으로 모델을 재학습(Fine-tuning)이 필요했었음.\
필자는 아래와 같은 기준으로 Fine-tuning을 실시하였음.
- Model: Yolov11 nano
- Class : 2개(Fire, Fall)
- Images : 약 19,000장 by roboflow
- Ratio: 학습, 검증, 테스트(7:2:1)

YOLO 모델 학습시 학습 안정성과 속도 같의 균형을 고려 하여 설정한 Parameter 값은 아래와 같음. 
- 학습은 총 **100 epochs** 기준으로 수행
- Early Stopping을 위해 **30 patience**
- 이미지 입력 크기는 **416x416**
- **Batch size 32**로 설정

아래와 같은 결과 값을 얻었다. 
<img width="1363" alt="Image" src="https://github.com/user-attachments/assets/086841a1-9023-46ec-9bed-fa8058035ffe" />

<table>
  <tr>
    <td width="50%"><img src="https://github.com/user-attachments/assets/ab39a7bf-9e4c-45b5-8937-e3d9a13f6cce"><br></td>
    <td width="50%"><img src="https://github.com/user-attachments/assets/c946b797-c03f-4f4b-9b9a-372d0a7e6756"><br></td>
  </tr>
</table>

Note) 
- 왜 YOLOv11 인가...?\
nano모델에서 아키텍처의 큰차이가 없어 사실 성능의 큰차이는 없지만, 최신버전인 Yolo 11이 다른 버전보다 미세하게 우세.\
단순한 쓰러짐, 화재 감지라서 nano모델 이상의 더 크고 강력한 모델을 쓸 필요는 없었음.
- 직접 labelling을 하지 않은 이유..?\
촉박한 시간에 labelling에 시간을 쏟는 이유가 없었으며, Fire와 Fall에 관한 데이터 자료가 충분하였기에 고려 x  

- 해당 parametre 값들로 설정한 이유..?\
이전 실험을 통해 80~90epochs 이후의 성능 정체가 있었고, 100 epochs는 충분한 학습기회를 제공하며 과적합 없이 수렴할거라 판단.\
Patience의 경우 loss가 완만하게 수렴되는 구조를 띄고 있어서 길게 잡을 필요는 없을거라 판단.\
Batch size 32는 64로 하기엔 메모리 부담이 있었고, 16은 학습에 많은 epochs가 필요할거라 판단하여 균형있는 32를 선택.\
나머지는 Roboflow reference대로 진행하였음.  

## 재활 - 산책 
<table>
  <tr>
    <td width="50%"><img src="https://github.com/user-attachments/assets/050bb257-d4b0-4d40-a96b-9316eebbc71d"><br></td>
    <td width="50%"><img src="https://github.com/user-attachments/assets/dbaf59f4-1230-4a45-b7aa-616ddc4eaeaa"><br></td>
  </tr>
</table>

요양원 내에서 어르신의 신체활동을 도모하기 위해 모바일 로봇을 활용한 걷기 서비스를 제공하기로 판단.\
아래와 같은 AI 기술을 활용하여 진행하였음.

### Object dectection
노인을 인지하기 위해서는 반드시 이 기술이 필요했었음.\
위험상황 감지시 사용했던 YOLO 11 nano model을 사용했으며, YOLO 모델은 기본적으로 '사람'을 감지하도록 이미 훈련이 되어있기에\
모델의 기본 성능을 활용하였음.
> Yolo model Class[0] == Person

#### Re-Identification 
요양원 환경에서는 사람이 많고, 조명이 일정하지 않아 얼굴 기반 식별이 어려울것이라 판단.\
따라서 색상 + 체형 기반의 비전 정보를 활용한 비얼굴 기반 재식별이 적합하다고 생각이 들었음.\
이를 위해 색상 및 체형 정보를 기반으로 어르신의 특징을 저장한 후, 특징 벡터를 생성하여 유사도를 비교하는 방식으로 재식별(ReID) 구현\
유사도 비교는 크기와 색상 정보를 결합한 압축된 특징 벡터를 사용하며, Cosine 유사도를 활용해 두 벡터 간 유사도를 측정.\
또한, 최대 90 프레임 내외에서 일정한 유사도 임계값을 설정하여, 임계값 이상일 경우 같은 ID로 재식별하도록 구현을 했었음.\

> 결과
딥러닝 기반의 ReID모델은 연산량이 매우 많지만, Cosine 유사도는 연산량이 많지 않아 상대적으로 안정적인 성능을 보여줬었음.

### Depth Estimation
노인과 로봇이 충돌하지 않도록 일정한 간격을 유지하며 주어진 경로를 따라 이동하는 것이 핵심.\
예산 제한으로 인해 고가의 Stero 카메라 대신 단일 카메라 기반의 뎁스추정을 활용해야 했음.\
로봇의 전면 카메라는 장애물 감지등 다른 영역에서 사용하기에 추가로 후면 카메라를 활용해 간격을 유지기능에 활용.
> 모델 선택 기준
> 1. 실시간 거리 정보를 받아야 하므로, 빠른 추론 속도 중요
> 2. 복잡한 학습 없이 바로 적용 가능한 모델

#### Depth anything v2 
딥러닝 기반 Depth Estimation 모델이 존재.
1.MiDaS -> 추론 속도가 느렸음 
2.DenseDepth -> 학습이 따로 필요 했음 

홍콩대학교 연구팀이 개발한 모델 *Depth Anythong v2*를 사용
- Hugging Face Transformers 라이브러리를 통해 손쉽게 로드 및 실행 가능
- GPU 가속(CUDA) 적용 시 실시간 추론 가능

<table>
  <tr>
    <td width="30%"><img src="https://github.com/user-attachments/assets/89d78db5-605f-43a2-9ada-84af036f3ae8"><br></td>
    <td width="30%"><img src="https://github.com/user-attachments/assets/f6a6820b-fec3-4e08-af06-8d63b886479b"><br></td>
  </tr>
</table>

## 정서적 대화

<div align="center">
  <iframe src="https://drive.google.com/file/d/11CfjPYbVZIDjEtyWtSgoaH126BffTP9d/preview" width="640" height="360" allow="autoplay"></iframe>
</div>

요양원 환경에서는 단순한 이동뿐만 아니라 **어르신과의 상호작용**이 중요한 역할을 한다. 따라서 **대화 기능**을 추가하도록 노력하였음. \
처음 구상은 훈련된 ollma 혹은 deepseek같은 모델을 활용하여 요양원 환경에 최적화된 모델 사용과 RAG를 적용시켜 단순한 AI응답이 아닌, 실제 요양원 시간표 및 생활 정보와 연계하여 반응하도록 시도했었음 하지만,\
크게 아래와 같은 제약들이 있었음.
- HW 성능 제한, 3060 6GB laptop GPU를 사용하다 보니 QLORA를 활용한 모델 학습 자체도 돌아가지 못했음
- 데이터 부족 및 전처리, 어르신과의 충분한 대화 데이터가 필요하지만 많이 없었고, 기본 대화 조차도 전처리를 했어야 하다보니 시간상 여유가 없었음.

이런 제약을 고려해서 차선책이었던, API를 적극활용하기로 하였음.

### LLM 구축 
<div align="center">
  <img src="https://github.com/user-attachments/assets/db09ec13-7a91-44ba-997b-cf49cdecbb66" width="300"/>
</div>

- STT (Google Cloud Speech API): 실시간 음성 인식을 활용해 노인의 말을 받아들이고
- LLM (OpenAI API) with context history: 문맥을 이해하고 감정을 반영하여 GPT 기반 응답을 생성
- TTS (Google Text-to-Speech API): 생성된 응답을 음성으로 변환하여 전달
  
대화를 하기 위해서는 이전 문맥을 이해하고 답변을 해야하기에 Json 파일로 이전 대화 histroy 를 축적하도록 구현을 하였음.\
Prompt를 작성하여 요양원 환경에 맞게 커스텀마이징을 하였음.\
ROS 통신을 통해 PC가 아닌 로봇을 활용해야 하다 보니 LLM 을 PC 서버쪽으로 돌리고 STT와 TTS를 로봇쪽에서 처리하도록 구현하였음.

### 통신 구조 
<div align="center">
  <img src="https://github.com/user-attachments/assets/9eee537d-94fa-4251-b2af-86c9850caa49" width="500"/>
</div>

STT, LLM, TTS 각각을 하나의 노드로 작성하여 ROS2의 Topic 기반 통신을 통해 유기적으로 작동하도록 시도했음.\
전체 시스템 flow를 큰 틀에서 살펴보자면
1. 사용자 음성 (trigger_word)
2. STTNode: stt로 음성->text (input topic 발행)
3. LLMNode: (input topic 구독) LLM 처리 및 OpenAI 연동 -> text 반환 (feedback topic 발행)
4. TTSNode: (feedback topic 구독) text -> 음성 반환 

> llm_state를 통해 현재 상황을 노드 간의 공유(e.g. 'listening', 'processing', 'speaking')

Reference: https://github.com/Auromix/ROS-LLM/tree/ros2-humble 



