---
title: 'Dive into AI Image Generation'
date: 2025-06-10
permalink: /posts/2025/06/blog-post-1/
tags:
  - Text-to-Video
  - Image-to-Video
  - Frame Interpolation
---
디지털동화 오픈소스 참여를 위해 시작한 stable diffsion에 대해 알아가보고자 작성 
[What is Stable Diffsion?](https://medium.com/@tahirbalarabe2/what-is-stable-diffusion-deep-dive-into-ai-image-generation-d16236e1edc2) by Medium 기사를 해석한 내용


What is Stable Diffusion..?
======
<p align="center">
  <img src="https://github.com/user-attachments/assets/44e213cf-89a6-4332-b4c6-8b8483128057" width="500" />
</p>

최근 몇 년 사이에 AI 기반 Image generator들이 급격히 인기를 얻고 있습니다.\
이러한 유명세에도 불구하고, 대부분의 사람들은 그러한 이미지 생성이 어떻게 작동하는지 알지 못합니다.\
이 글에서는 Stable Diffusion에 대해 자세히 살펴보겠습니다. 

Stable diffusion은 단지 text 프롬프트를 통해서 생성되는게 아닙니다.\
이 기술은 '생성형 AI'로 알려진 보다 광범위한 기술 집합의 일부라고 생각하시면 됩니다.

생성형 AI는 쓰이는 분야가 다양합니다.
- Text-to-text: ChatGPt, Gemini, Claude, Mistral, LLAMA, Gro
- Text-to-image: Midjourney, DALL-E, Imagine, Muse, Stable Diffusion
- Text-to-music: MusicLM, MusicGen, Stable Audio, SoonO
- Text-t0-video: Imagine Video, Lumiere, Emu Video, Stable Video DIffusion, OpenAI's Sora

<p align="center">
  <img src="https://github.com/user-attachments/assets/cfef2c83-9792-4416-9594-b5dc3db7abda" width="500" />
</p>  

걸핏보기에 AI 이미지 생성은 마법같이 보일 수 있습니다.\ 
단지 몇번의 타이핑으로 실제로 존재하지 않는 이미지를 사실적으로 그려주니 그럴 수 밖에요.\
그러나 진짜는 더 흥미롭고 복잡합니다...!\
Stable Diffusion은 이미지 생성에 있어서 가장 강력한 오픈소스 중 하나입니다.\
왜냐하면 수학적 변환과정이 매우 정교하게 작동하기 때문입니다.\
한번 차근차근 살펴봅시다..!

Training the Model
======
첫번째로, 매우 잘 훈련된 모델이 필요합니다.\
에를들어 '모나리자' 미술작품을 생각해봅시다.\
만약 '모나리자'작품만을 훈련된 모델이 있다면, 그 모델이 생성할 수 있는 것은 단지 모나리자 하나 뿐 입니다.\
그래서 새로운 인물등을 넣어 다양한 작품을 훈련시키는게 필요합니다.\
하지만, 이미지의 양이 충분치 않을 때는 어떨까요?\
그래서 작품에 대한 '설명' 또한 필요합니다. 따라서 Stable diffusion은 수백만의 Image-text가 필수적입니다.

실제로 Stable Diffusion 1.5 모델은 23억개의 Image-text를 가지고 있습니다.\
신기하게도 그 엄청난 양의 데이터가 2GB가 조금 넘는 모델에 들어갈 수 있을까요? 그리고 어떻게 완전히 새로운 이미지를 생성할 수 있을까요?

훈련의 Key가되는 요소들이 있습니다.
- Image-Text pairs:  [LAION-5B](https://laion.ai/blog/laion-5b/) 같은 데이터셋을 사용해 인터넷에서 수집되었습니다. 
>LAION에 대해서 간단하게 설명하자면 대규모 머신러닝 모델과 데이터세트 관련 코드를 비영리적으로 공개하고 있는 단체입니다.
- Deep Learning: Image-text로 부터 학습과 처리를 위해 신경망(Neural network)를 사용합니다.

Two Network Layers:
- Convolutional Layer: 이미지로 부터 특징을 추출합니다. 
- Self-Attention Layer: 모델이 문맥을 잘 이해하고 있는지 확인합니다.

이러한 층들은 유기적으로 연결되어있으며, 모델이 이미지와 text사이의 복잡한 관계를 배울 수 있게 합니다. 

<p align="center">
  <img src="https://github.com/user-attachments/assets/a52938a9-dc4d-4a68-9b38-9e828b7f59c2" width="500" />
</p>  


Neural Networks 
------
신경망의 모든 뉴런들은 서로 층을 따라 연결되어 있습니다. \
입력(Input), 하나 이상의 은닉(hidden)층이 있고, 그리고 출력(output)층으로 구성됩니다.\
이처럼 모든 뉴런이 완전히 연결되는 구조는, 이미지 생성과 같은 작업에서는 막대한 수의 연결이 필요하기 때문에 비현실적일 수 있습니다.

대신, 합성곱 신경망(CNN, Convolutional neural networks)을 사용합니다.\
CNN은 입력 뉴런 중 일부만을 은닉층에 연결하여, 전체 연결 수를 줄이는 데 도움을 줍니다.\
>CNN은 이미지의 local region(국소 영역)에 집중하여, edge(윤곽선)과 shape(형태)와 같은 특징들을 효과적으로 추출할 수 있습니다.

Computer Vision 
------
Computer vision은 image 속의 내용을 이해하는 기술입니다. 이 과정은 크게 네 가지 수준으로 나눌 수 있습니다. 
- Classificaiton: 이미지 전체를 보고 어떤 객체가 있는지를 판별 ex) "이 이미지는 고양이다" 
- Localization: 객체가 이미지의 어디에 있는지 파악 ex) "고양이는 이미지의 왼쪽 상단에 있다."
- Object Detection: 객체의 종류와 위치를 동시에 식별 ex)  "이 이미지에는 고양이와 강아지가 있으며, 위치는 각각 이렇다"
- Semantic Segmentation: 이미지의 각 픽셀 단위로 어떤 객체에 속하는지 분류 ex) "고양이, 강아지, 배경 등을 색으로 나누어 표현"

Stable diffusion은 segmantic segmentation 수준까지 작동합니다. 즉, 모델이 이미지의 픽셀 단위까지 이해하거나 조작할 수 있다는 이야기입니다.\
이것은 UNet 구조(encoding과 decoding층을 결합한 U자형 네트워크)를 기반으로 합니다.
>Encoder: 더 넓은 범위의 특징(예: 전체 구조나 윤곽)을 포착하기 위해 이미지를 점점 축소(downscale) 하면서 고수준의 의미 있는 정보를 추출합니다.
>Decoder: 인코더에서 축소된 특징 맵(feature map)을 바탕으로 이미지를 다시 복원(upscale) 하며, 세부적인 정보와 공간적 구조를 되살려 냅니다
<p align="center">
  <img src="https://github.com/user-attachments/assets/30edce0d-60dc-449d-8b7e-b521f2e53f61" width="500" />
</p>  

Noise and Denoising 
------
이미지를 무에서 유를 창조하기란 어려운 일입니다.\
하지만, 이미지의 noise를 제거하는 것은 컴퓨터에게 우리가 학습을 시킬 수 있습니다.

작동원리:
1. Noising Process: 어떤 이미지에 랜덤한 noise를 반복적으로 입힙니다
>마치 픽셀로 이루어진 눈보라처럼 무작위한 픽셀로 가득 찬 pure static상태
2. Denoising Process: 이것을 반대로 신경망을 학습시킵니다.
> 노이징된 이미지들을 보여주고, 가르친다음, 원래의 모습이 무엇인지 예측하는 형태
3. Generation: 새로운 이미지 생성
> 무작위 노이즈에서 신경망이 그것을 반복적으로 노이즈 제거하여 의미 있는 이미지로 바꿈.  

이 일련의 과정이 diffusion modeling이라 부릅니다. 그러한 이유로 이 시스템을 Stable diffusion이라 부릅니다.\
그런데 무엇을 만들지 어떻게 알 수 있을까요? 여기서 text prompts가 필요로 합니다. 






