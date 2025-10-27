---
title: "StoryTeller"
excerpt: "아이맞춤형 AI 동화 생성 및 리딩 서비스<br/><img src='https://github.com/user-attachments/assets/8a5c0e1a-0edd-49b6-8582-80fb7d6528c9' width='300' height='100'>"
collection: portfolio
---

## Overview
Project period: 2025.06 ~ 2025.10
link: [StoryTeller](https://github.com/ING-First)
<div align="center">
  <iframe width="560" height="315"
    src="https://www.youtube.com/embed/IhlMm7Sdbdo"
    title="YouTube video player"
    frameborder="0"
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
    allowfullscreen>
  </iframe>
</div>
</ br>

2025 오픈소스 개발자대회 참가 출전작으로 AI(LLM & Stable diffusion)를 활용한 교육용 서비스를 오픈소스로 만들고자 참여하게 되었음.

</ br>
<p align="center">
  <a href="https://docs.google.com/presentation/d/1K7izor5Px3n0uWPPXWq2igYqOLvkR59O/edit?usp=sharing&ouid=113099810683180168409&rtpof=true&sd=true">Presentation</a>
</p>

## Abstract
<img src="https://github.com/user-attachments/assets/dce256df-6293-43b5-91fb-2f0edafbc3a5" width="300" style="display:inline-block; margin-right:10px;">
<img src="https://github.com/user-attachments/assets/3f62efa3-879b-4ff1-97f9-d5a6fab1ef80" width="400" style="display:inline-block;">

공모전에 참여하기 위해서 자유과제, 지정과제, 지속발전과제 등 3개의 유형 중 하나를 선택해야만 했었음.\
AI를 최대한 활용하는 프로젝트를 진행하고자 자유과제를 선정.\

서비스 'StoryTeller'를 통해..
- 자유롭게 이야기 구성을 설정할 수 있음,
- AI는 이에 적합하고 참신한 애니메이션, 이미지, 등장인물, 텍스트, 음성 등의 멀티미디어 동화 콘텐츠를 생성
- 누구나 동화 속 무대의 관객이자 감독이 될 수 있는 새로운 창작·감상 경험을 제공함으로써, 창의적 상호작용형 스토리텔링의 가능성을 확대

## Design

<p align="center">
  <img src="https://github.com/user-attachments/assets/0dc25a98-6a86-4b56-920d-553bd3171e67" width="500">
</p>

| Tech Stack | Framework | Description |
|----|-----|-----|
| FE | React + TypeScript 기반 환경 |  서비스를 제공하기 위해서는 web 기반 UI를 선택 하였음 | 
| BE | FastAPI(Python), exposed via ngrok | 팀원 모두 공통적으로 주 개발 언어는 Python이었기 때문에 Fastapi framework를 이용.\ 온라인으로 개발을 하다보니 서버를 외부와 연결이 필수적이라 ngrok 사용.| 
| DB | AWS RDS with MySQL | AWS 사용에 매우 익숙 |
| AI | Fine-tuned LLM foundation model | 동화 생성, 평가, 요약을 위해 QLoRA & LoRA 시행 | 
| Image AI | Fine-tuned stable diffusion model | 동화 삽화 생성 | 


## Contribution 




