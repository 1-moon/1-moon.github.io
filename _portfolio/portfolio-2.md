---
title: "Fitness AI Agent"
excerpt: "AI 기반 스마트 피트니스 트레이닝 시스템<br/><img src='https://github.com/user-attachments/assets/fc12cd22-ef3a-408d-b2a1-71b10ff9d416' width='300' height='100'>"
collection: portfolio
---

Project period: 2025.03 ~ 2025.04 link: [피트니스 AI 어시스턴트](https://github.com/addinedu-ros-8th/deeplearning-repo-1)

이 프로젝트는 ML과 DL을 활용하여 피트니스 트레이너 역할을 대신할 수 있도록 개발되었습니다.\
운동 동작 분석, 피드백 제공, 실시간 운동 자세 교정등을 통해 사용자가 더욱 효과적인 피트니스 트레이닝을 받을 수 있도록 돕습니다.\
제가 맡은 파트는 Hand gesture를 이용한 UI 및 인공지능 모델 학습을 맡았습니다. 


## Hand Gesture UI 
![Image](https://github.com/user-attachments/assets/4879d38c-d6cb-4a4c-a3a6-226bc995d4b0)
![Image](https://github.com/user-attachments/assets/5ce51d23-7b70-46bd-af8f-2a0e75ded9b8) 

피트니스 앱 특성상, 운동중에 아래와 같이 불편한 상황이 발생할 수 있다. 
- 중단하거나 멈추고 싶을때 마다 컴퓨터 앞으로 와야 한다는 점.
- 다른 운동을 하고 싶을때마다 컴퓨터 앞으로 와야 한다는 점.
- 어떤 운동인지 확인하고 싶을때마다 컴퓨터 앞으로 와야 한다는 점.

Hand gesture 기능을 사용한다면 이러한 불편함을 해결해 줄 수 있다고 생각했고, MediaPipe 라이브러리를 적극적으로 사용하기로 하였음.
- **MediaPipe Hands** 모델을 사용하여 실시간으로 손의 랜드마크 감지 
- webcam으로 부터 frame을 받아 손을 감지하고, 각 손가락의 랜드마크 좌표 추출
- 손가락 개수에 따라 특정 동작을 수행할 수 있도록 손가락 인식 알고리즘 적용
- webcam frame위에 버튼이 보이도록 설정하고, 클릭 이벤트 실행 
- 손이 버튼 영역 안에 있는지 확인 
- 손이 일정 시간 동안 버튼을 가리키면 클릭 감지


## Deep Learning model
<div align="center">
  <img src="https://github.com/user-attachments/assets/319174e8-532d-40fd-819d-b4e536d2ff55" width="500" />
</div>

운동 데이터를 학습시킬때 정적인 이미지를 학습시키면 안됨\
따라서 순차 데이터를 분석하는 데 최적화된 RNN(Recurrent Neural Network) 모델인 LSTM을 사용.

입력 데이터 셋
- **스쿼트** : 26개
- **숄더 프레스** : 11개
- **니업** : 14개
- **런지** : 18개
- **Train,Valid** : 80%, 20%
원하는 데이터 셋을 구하지 못해서 대부분은 직접 영상을 찍어 frame으로 나누어 학습 시켰음. 


### Model Layer 
<div align="center">
  <img src="https://github.com/user-attachments/assets/a6d335ef-159e-4331-a0dd-6a4dfdb4d79b" width="500" />
</div>

LSTM parameter 설정 
- **epochs** : 20
- **batch_size** : 100
- **sequence** : 20, 30   -> 이전 20~30 frame을 참고하여 예측

### Evaluation 
#### Sequence size 
- Sequence size 20
<table>
  <tr>
    <td><img src="https://github.com/user-attachments/assets/f87df427-a4a4-4249-9fb8-4493216c2d62" width="300"></td>
    <td><img src="https://github.com/user-attachments/assets/144eaa57-c065-4896-bd38-8ee5a2b086ee" width="300"></td>
  </tr>
  <tr>
    <td align="center">Confusion Matrix</td>
    <td align="center">정확도: 77%</td>
  </tr>
</table>
- Sequence size 30
<table>
  <tr>
    <td><img src="https://github.com/user-attachments/assets/6f33ed1e-d01f-4cb7-afaf-a82e28d7b84d" width="300"></td>
    <td><img src="https://github.com/user-attachments/assets/6f4c5e8b-9ef7-41e1-b692-21a3dcb4406a" width="300"></td>
  </tr>
  <tr>
    <td align="center">Confusion Matrix</td>
    <td align="center">정확도: 86%</td>
  </tr>
</table>

- Training History
<br />
<img src="https://github.com/user-attachments/assets/cfd90b57-cc5b-41eb-b3b3-fbecb73dfe15" width="500">

- result
<br />
<img src="https://github.com/user-attachments/assets/eb6fbcc9-7537-4757-beca-b1ba8d499f8d" width="500">

## 
