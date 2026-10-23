<div align="center">

# Namgung Geonwoo

**Physical AI Engineer**

AI that understands and acts in the physical world.

Seoul, Korea

</div>

---

## About

소프트웨어 위의 AI가 아니라, 물리 세계에서 동작하는 AI를 만듭니다.

지금은 도로 작업 구간의 **로봇신호수**가 차량 리프트에 스스로 올라타는 도킹을 **강화학습 정책 하나**로 만들고 있습니다. GPU 시뮬레이션에서 학습하고, 실물 로봇은 확인 시험만 하는 sim-to-real 파이프라인 전체를 다룹니다. 시뮬레이터, 센서 융합, 학습, 온보드 배포, 안전 규칙까지 포함합니다. 같은 로봇의 3D LiDAR 가드레일·장애물 인지, 객체 탐지 모델, 무선충전 제어도 맡고 있습니다.

그 전에는 ROS 2 기반 다중 로봇 Fleet Management System(서빙로봇 3대 + 로봇팔 2대)을 단독 설계·구현했고, RAG/LLM 기반 AI 시스템으로 고용노동부장관상을 받았습니다.

---

## Highlights

| Physical AI & Robotics | AI |
|---|---|
| 리프트 도킹 **sim-to-real 강화학습**: 16,384 병렬 환경 torch 시뮬레이터 → PPO → ONNX → Jetson Orin ROS 2 노드 | RAG/LLM 기반 **고용노동부장관상** 수상 |
| 다중 AprilTag 평면 PnP + odom·IMU **EKF 융합기** (로봇용 numpy 판 / 학습용 torch 판 동등성 검증) | 멀티 에이전트 워크플로우 (LangGraph) 설계 |
| 3D LiDAR(Hesai JT16) **가드레일·장애물 인지** (학습 없이 기하 처리, Jetson Orin NX) | 82클래스 **RF-DETR 객체 탐지** 학습·Orin NX 탑재 |
| 서빙로봇 3대 + 로봇팔 2대 통합 관제 **FMS** 단독 설계·구현 | 6개 AI/ML 프로젝트 완료 |

---

# Projects

## 1. 로봇신호수 리프트 도킹 강화학습 *(private)*

> 리프트 앞 약 5 m(횡 ±1 m, 방향 ±30°)에서 출발해 1.5 m 앞에 정렬해 서고, VMS를 접은 뒤 경사로를 올라 리프트 위 최종 자세까지 가는 전 구간을 정책 하나로 수행한다.

- PyTorch, rsl_rl(PPO), ONNX Runtime, ROS 2 Humble, Jetson Orin, Gazebo, Isaac Sim, AWS EC2(L4 GPU)

```
contracts/ (형상·센서·관측·안전 수치의 단일 정본)
   ├── sim_lite ── torch 벡터화 시뮬레이터 (16,384 env, 약 5만 step/s)
   │              태그 투영·검출 잡음·지연, 모터·odom, 경사로 턱 정체, 판 접촉, 도메인 랜덤화
   ├── fusion ──── 다중 태그 PnP + EKF (numpy 판 = 로봇, torch 판 = 학습)
   ├── train ───── PPO 커리큘럼 학습 (AWS) → 평가 → ONNX
   └── robot node ─ 융합기 + ONNX 정책 + 안전 게이트 + 깊이 카메라 장애물 정지
                    (기존 main_control 흐름 안에서 도킹 노드 자리로 동작)
```

| 구분 | 내용 |
|---|---|
| **시뮬레이터** | GPU 벡터화 sim에 실측 기하(경사로, 플랫폼 벽, 태그판)와 현상(캐스터 턱 정체·튀어 나감, 한쪽 바퀴 헛돎, 햇빛 glare, 센서 지연)을 넣고, 실차 로그로 랜덤화 범위를 보정 |
| **센서 융합** | 보이는 모든 태그 꼭짓점의 평면 3자유도 PnP + odom·IMU EKF. 지연 보정, 탑승 이벤트, 충격 롤 차단. 1.5 m 지점 좌우 오차 p95 5.0 → 3.6 cm |
| **정책 성능 (sim)** | 무작위 출발 500회 성공 99.4 %, 최종 좌우 p95 1.3 cm·방향 p95 0.7°, 판 앞 4 cm 정지 |
| **안전** | 정책 밖 안전 게이트: 속도·가속 상한, 입력 신선도, 지오펜스, 판 접촉 정지, 깊이 장애물 정지. sim 게이트와 로봇 노드가 같은 판단을 하는지 대조 |
| **검증** | Gazebo SIL(로봇 노드 폐루프), 실차 rosbag 재생 비교, Isaac Sim 3D 재생 영상 |

## 2. 3D LiDAR 가드레일·장애물 인지 *(private)*

> Hesai JT16 3D LiDAR 하나로 도로 가드레일 경계와 장애물을 추출해 ROS 2 토픽으로 발행하는 인지 컴포넌트

- ROS 2 Humble, Hesai JT16, Jetson AGX Orin(개발) / Orin NX(탑재), RViz2
- 학습 모델 없이 기하 처리만으로 구성해 데이터 수집·라벨링 없이 1주 안에 동작
- 각도별 최단 거리를 표준 `LaserScan`으로 내보내 Nav2 costmap에 바로 연결, 인지 상태(health) 발행

## 3. 로봇 탑재 객체 탐지 (82클래스) *(private)*

> COCO 80종에 도로 순찰차량·차량 트렁크 내부 2종을 더한 82클래스 탐지 모델을 학습해 로봇에 탑재

- RF-DETR(Nano / Small / Medium), PyTorch, AWS 학습, Jetson Orin NX, ROS 2
- 현장 데이터를 섞은 데이터셋 구성, 중단 규칙·배포 임계값을 설정 파일로 관리, Orin NX 실측 속도로 탑재 모델 선정(Nano)
- 로봇 카메라 노드 연동과 역광·태그 실험

## 4. 로봇 무선충전 제어 *(private)*

> 로봇이 리프트 위 충전존에 안착하면 바로 충전을 시작하고, 완충 기준에 맞춰 멈추고 다시 확인하는 ROS 2 노드

- ROS 2, C++, 시리얼 통신(수전제어기), 2.5 kW 무선충전기

## 5. [Kitchmatics](https://github.com/addinedu-roscamp-4th/roscamp-repo-1) — 다중 로봇 Fleet Management System

> ROS 2 기반 자율주행 서빙로봇 3대 + 로봇팔 2대 협업 스마트 키친 시스템

- ROS 2 Jazzy, Nav2, Python, PostgreSQL, Domain Bridge, TCP/IP, PyQt

```
Main PC (Domain 25) ─── FMS Node, Sandwich Coordinator, Domain Bridge, DB
  ├── Pinky1 (Domain 11) ── 서빙로봇
  ├── Pinky2 (Domain 12) ── 서빙로봇
  ├── Pinky3 (Domain 13) ── 서빙로봇
  ├── Arm A  (Domain 20) ── 샌드위치 제조
  └── Arm B  (Domain 21) ── 소스 도포
```

| 구분 | 내용 |
|---|---|
| **Project Manager** | 6인 팀 리드, 시스템 아키텍처 설계, 모듈 간 인터페이스 정의, 스프린트 운영 |
| **FMS 설계 및 구현** | 주문-서빙-복귀 전 과정을 관제하는 Fleet Management System 단독 설계·구현 |
| **FMS 모듈** | Task Scheduler, Fleet Controller, Zone Manager(충돌 회피·교착 해소), Path Planner, Error Recovery, 5개 도메인 Domain Bridge, 커스텀 메시지 11종, 테스트 155개 이상 |
| **GUI 개발** | 운영자용 실시간 모니터링 대시보드, 주문 접수 및 수동 제어 인터페이스 (TCP 기반) |

## 6. Omniverse · OpenUSD

- [kit-app-template](https://github.com/NGGW519/kit-app-template), [LearnOpenUSD](https://github.com/NGGW519/LearnOpenUSD): NVIDIA Omniverse Kit 앱과 OpenUSD 장면 구성 학습. Isaac Sim 3D 재생 영상 제작에 활용

---

## AI & ML

| 프로젝트 | 내용 | 기술 |
|---|---|---|
| **[고향으로 ON](https://github.com/NGGW519/7th-kDT-HACKATHON)** — 고용노동부장관상 | RAG 기반 중장년층 고향 정착 지원 플랫폼, 음성 UI/UX. 팀장, AI 시스템 설계·구현 | React Native, FastAPI, OpenAI GPT, RAG, ChromaDB |
| **[CLIKCA](https://github.com/SKNETWORKS-FAMILY-AICAMP/SKN13-FINAL-1TEAM)** — AI 업무 파트너 | 멀티 에이전트 업무 자동화, 하이브리드 검색, LangGraph 워크플로우 라우팅 | Electron, FastAPI, LangGraph, OpenAI, AWS S3 |
| **[의학 논문 팩트체킹 챗봇](https://github.com/SKNETWORKS-FAMILY-AICAMP/SKN13-3rd-1TEAM)** | 3개 의학 DB 통합 RAG 파이프라인, RAGAS 자동 평가 | GPT-4.1, ChromaDB, RAGAS, Streamlit |
| **[지금, 서울](https://github.com/SKNETWORKS-FAMILY-AICAMP/SKN13-4th-1TEAM)** | 서울 열린데이터 API 통합 AI 시정 Q&A, 관리자 대시보드 | Django, LangChain, LangGraph |
| **[DRMC](https://github.com/SKNETWORKS-FAMILY-AICAMP/SKN13-1st-2Team)** | 자동차 리콜 정보 시각화·추천, 크롤링 자동화 | Streamlit, MySQL, Selenium |
| **[환자 이탈 예측](https://github.com/SKNETWORKS-FAMILY-AICAMP/SKN13-2nd-7Team)** | 클래스 불균형 해결(SMOTE), F1 11.4 % 개선 | XGBoost, Scikit-learn |

---

## Tech Stack

<div align="center">

| Physical AI & Sim | Robotics | AI & ML | Backend & Infra |
|---|---|---|---|
| ![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=flat-square&logo=pytorch&logoColor=white) | ![ROS2](https://img.shields.io/badge/ROS2-22314E?style=flat-square&logo=ros&logoColor=white) | ![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white) | ![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white) |
| ![Isaac Sim](https://img.shields.io/badge/Isaac_Sim-76B900?style=flat-square&logo=nvidia&logoColor=white) | ![Nav2](https://img.shields.io/badge/Nav2-22314E?style=flat-square&logo=ros&logoColor=white) | ![OpenAI](https://img.shields.io/badge/OpenAI-412991?style=flat-square&logo=openai&logoColor=white) | ![Django](https://img.shields.io/badge/Django-092E20?style=flat-square&logo=django&logoColor=white) |
| ![Gazebo](https://img.shields.io/badge/Gazebo-F58113?style=flat-square&logo=ros&logoColor=white) | ![Jetson](https://img.shields.io/badge/Jetson_Orin-76B900?style=flat-square&logo=nvidia&logoColor=white) | ![LangChain](https://img.shields.io/badge/LangChain-121212?style=flat-square&logo=chainlink&logoColor=white) | ![PostgreSQL](https://img.shields.io/badge/PostgreSQL-336791?style=flat-square&logo=postgresql&logoColor=white) |
| ![ONNX](https://img.shields.io/badge/ONNX_Runtime-005CED?style=flat-square&logo=onnx&logoColor=white) | ![LiDAR](https://img.shields.io/badge/3D_LiDAR-22314E?style=flat-square&logo=ros&logoColor=white) | ![ChromaDB](https://img.shields.io/badge/ChromaDB-FF6B6B?style=flat-square&logo=database&logoColor=white) | ![MySQL](https://img.shields.io/badge/MySQL-005C84?style=flat-square&logo=mysql&logoColor=white) |
| ![OpenUSD](https://img.shields.io/badge/OpenUSD-76B900?style=flat-square&logo=nvidia&logoColor=white) | ![AprilTag](https://img.shields.io/badge/AprilTag_·_RealSense-22314E?style=flat-square&logo=intel&logoColor=white) | ![React](https://img.shields.io/badge/React-20232A?style=flat-square&logo=react&logoColor=61DAFB) | ![AWS](https://img.shields.io/badge/AWS_EC2-232F3E?style=flat-square&logo=amazon-aws&logoColor=white) |

</div>

---

## Specialization

| Physical AI | Robotics | AI Development |
|---|---|---|
| Sim-to-Real Reinforcement Learning | ROS 2 노드·안전 게이트 설계 | RAG Systems |
| GPU 벡터화 시뮬레이터·도메인 랜덤화 | 센서 융합 (PnP + EKF, LiDAR) | Multi-Agent AI (LangGraph) |
| 온보드 정책 배포 (ONNX, Jetson) | 객체 탐지 탑재 (RF-DETR, Jetson) | LLM Integration |
| | Multi-Robot Fleet Management | |

---

## GitHub Stats

<div align="center">

| ![stats](https://github-readme-stats.vercel.app/api?username=NGGW519&show_icons=true&theme=default&hide_border=true) | ![langs](https://github-readme-stats.vercel.app/api/top-langs/?username=NGGW519&layout=compact&theme=default&hide_border=true) |
|---|---|

</div>

---

## Contact

[![GitHub](https://img.shields.io/badge/GitHub-100000?style=flat-square&logo=github&logoColor=white)](https://github.com/NGGW519)
[![Email](https://img.shields.io/badge/Email-D14836?style=flat-square&logo=gmail&logoColor=white)](mailto:srrd1357@gmail.com)

---
