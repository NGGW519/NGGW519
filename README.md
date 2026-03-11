# Namgung Geonwoo

**Physical AI Engineer**

AI that understands and acts in the physical world.

Seoul, Korea

---

## About

소프트웨어 위의 AI가 아니라, 물리 세계에서 동작하는 AI를 만듭니다.

ROS 2 기반 다중 로봇 Fleet Management System을 설계하고 구현하면서, AI 판단이 실제 로봇의 움직임으로 이어지는 전체 파이프라인을 경험했습니다. CARLA 시뮬레이터에서의 교통 흐름 생성과 LiDAR/Camera/IMU 센서 데이터 처리부터, 실제 로봇 5대의 Fleet 관제까지 — 시뮬레이션과 실물 양쪽에서 Physical AI를 다룰 수 있는 엔지니어를 지향합니다.

---

## Highlights

| Robotics | Simulation | AI |
| --- | --- | --- |
| 서빙로봇 3대 + 로봇팔 2대 통합 관제 **FMS** 설계 및 구현 | CARLA 시뮬레이터 기반 교통 흐름 생성 및 연동 | RAG/LLM 기반 **고용노동부장관상** 수상 |
| FMS 전 모듈 단독 개발 (스케줄링, 충돌 회피, 경로 계획, 장애 복구) | LiDAR, Camera, IMU 센서 모델링 및 데이터 처리 | 6개 AI/ML 프로젝트 완료 |

---

## Projects

### Table of Contents

| # | 프로젝트 | 분류 | 기술 키워드 |
|---|---------|------|------------|
| [1](#1-kitchmatics---smart-kitchen-fleet-management-system) | Kitchmatics — Smart Kitchen FMS | Robotics / FMS | ROS 2, Nav2, Domain Bridge, PyQt |
| [2](#2-고향으로-on) | 고향으로 ON | AI / RAG | RAG, LangChain, ChromaDB, FastAPI ★ 고용노동부장관상 |
| [3](#3-clikca---ai-업무-파트너) | CLIKCA — AI 업무 파트너 | AI / Multi-Agent | LangGraph, LLM, Hybrid Search |
| [4](#4-의학-논문-기반-팩트체킹-챗봇) | 의학 논문 팩트체킹 챗봇 | AI / RAG | RAG, RAGAS, GPT-4.1, ChromaDB |
| [5](#5-지금-서울---ai-시정-qa) | 지금, 서울 — AI 시정 Q&A | Web / AI | LangGraph, Django, 서울시 API |
| [6](#6-drmc---자동차-리콜-정보-서비스) | DRMC — 자동차 리콜 정보 서비스 | Web / Data | Streamlit, MySQL, Selenium |
| [7](#7-환자-이탈-예측-모델) | 환자 이탈 예측 모델 | Data Science / ML | XGBoost, SMOTE, Scikit-learn |

---

### 1. Kitchmatics - Smart Kitchen Fleet Management System

> ROS 2 기반 자율주행 서빙로봇 3대 + 로봇팔 2대 협업 스마트 키친 시스템

[Repository](https://github.com/addinedu-roscamp-8th/roscamp-repo-1) · ROS 2 Jazzy, Nav2, Python, PostgreSQL, Domain Bridge, TCP/IP, PyQt

```
Main PC (Domain 25) ─── FMS Node, Sandwich Coordinator, Domain Bridge, DB
  ├── Pinky1 (Domain 11) ── 서빙로봇
  ├── Pinky2 (Domain 12) ── 서빙로봇
  ├── Pinky3 (Domain 13) ── 서빙로봇
  ├── Arm A  (Domain 20) ── 샌드위치 제조
  └── Arm B  (Domain 21) ── 소스 도포
```

#### My Role

| 구분 | 내용 |
| --- | --- |
| **Project Manager** | 6인 팀 리드, 시스템 아키텍처 설계, 모듈 간 인터페이스 정의, 스프린트 운영 |
| **FMS 설계 및 구현** | 주문-서빙-복귀 전 과정을 관제하는 Fleet Management System 단독 설계/구현 |
| **GUI 개발** | 운영자용 실시간 모니터링 대시보드, 주문 접수 및 수동 제어 인터페이스 (TCP 기반) |

#### FMS 상세 모듈

| 모듈 | 기능 |
| --- | --- |
| **Task Scheduler** | 주문 큐 관리, 픽업 슬롯 할당, 우선순위 기반 태스크 스케줄링 |
| **Fleet Controller** | 서빙로봇 3대 + 로봇팔 2대 실시간 상태 모니터링, 가용 로봇 자동 배정 |
| **Zone Manager** | 다중 로봇 충돌 회피, 구역 예약 시스템, 교착 상태 감지 및 해소 |
| **Path Planner** | Navigation Graph 기반 최적 경로 계획 |
| **Error Detection & Recovery** | 장애 자동 감지 및 복구 핸들러 |
| **Domain Bridge** | ROS_DOMAIN_ID 격리 환경에서 5개 도메인 간 통신 브릿지 구축 |
| **fleet_interfaces** | 커스텀 ROS 2 메시지 패키지 설계 (11개 메시지 타입) |
| **Testing** | 단위/통합/E2E 155개 이상의 테스트 케이스 |

[↑ 목차로](#table-of-contents)

---

### 2. 고향으로 ON

**★ 제7회 k-DigitalTraining Hackathon 고용노동부장관상 수상작**

RAG 기반 중장년층 고향 정착 지원 플랫폼. 음성 UI/UX, 지역별 맞춤 정보 제공.

[Repository](https://github.com/NGGW519/7th-kDT-HACKATHON) · React Native, TypeScript, FastAPI, OpenAI GPT, RAG, ChromaDB, MySQL

- **역할**: 팀장, AI 시스템 설계 및 구현
- RAG 파이프라인 핵심 설계 및 LangChain 기반 LLM-벡터 검색 로직 연동
- 중장년층 접근성을 위한 음성 STT 기반 인터페이스 구현

[↑ 목차로](#table-of-contents)

---

### 3. CLIKCA — AI 업무 파트너

**멀티 에이전트 시스템 기반 업무 자동화 솔루션**

[Repository](https://github.com/SKNETWORKS-FAMILY-AICAMP/SKN13-FINAL-1TEAM) · Electron, React, FastAPI, LangGraph, OpenAI, ChromaDB, AWS S3

- **역할**: 팀장 & PM, AI 워크플로우 아키텍처 설계 및 LangGraph 구현
- 하이브리드 검색(키워드+벡터), LangGraph 멀티 에이전트 라우팅
- SSE 기반 실시간 스트리밍 응답, 온보딩 기간 12주 → 4주 단축

[↑ 목차로](#table-of-contents)

---

### 4. 의학 논문 기반 팩트체킹 챗봇

**신뢰할 수 있는 의학 정보 제공 AI 시스템**

[Repository](https://github.com/SKNETWORKS-FAMILY-AICAMP/SKN13-3rd-1TEAM) · GPT-4.1, ChromaDB, RAG, RAGAS, Streamlit

- **역할**: RAG 파이프라인 설계 및 RAGAS 평가 구현
- 3개 의학 DB(Europe PMC, PubMed, MedRxiv) 통합 RAG 파이프라인
- RAGAS(Context Recall / Faithfulness / Answer Relevancy) 자동 평가 시스템

[↑ 목차로](#table-of-contents)

---

### 5. 지금, 서울 — AI 시정 Q&A

**서울시 행정 정보 AI 문답 시스템** (2일 개발)

[Repository](https://github.com/SKNETWORKS-FAMILY-AICAMP/SKN13-4th-1TEAM) · Django, LangChain, LangGraph, ChromaDB, MySQL

- **역할**: LangChain 기반 RAG 설계 및 LangGraph 챗봇 에이전트 구현
- 서울 열린데이터 광장 API 통합, FAQ 자동 응답, 관리자 대시보드

[↑ 목차로](#table-of-contents)

---

### 6. DRMC — 자동차 리콜 정보 서비스

**자동차 안전 정보 제공 플랫폼** (2일 개발)

[Repository](https://github.com/SKNETWORKS-FAMILY-AICAMP/SKN13-1st-2Team) · Streamlit, MySQL, Selenium, Python

- **역할**: 데이터 시각화 및 데이터베이스 설계
- 리콜 정보 시각화, 맞춤 추천, 웹 크롤링 자동화

[↑ 목차로](#table-of-contents)

---

### 7. 환자 이탈 예측 모델

**머신러닝 기반 의료 데이터 분석**

[Repository](https://github.com/SKNETWORKS-FAMILY-AICAMP/SKN13-2nd-7Team) · Python, XGBoost, SMOTE, Scikit-learn

- **역할**: 데이터 분석 및 모델링
- 클래스 불균형 해결(SMOTE), **F1 Score 11.4% 개선** (0.4624 → 0.5153)
- 뉴욕주 병원 입원·퇴원 데이터 256만 건 분석, 주요 이탈 인자 식별

[↑ 목차로](#table-of-contents)

---

## Tech Stack

| AI & ML | Backend | Frontend | Robotics | Database & Infra |
| --- | --- | --- | --- | --- |
| Python | FastAPI | React | ROS2 | PostgreSQL |
| OpenAI | Django | TypeScript | Nav2 | MySQL |
| LangChain | Flask | Electron | Domain Bridge | AWS |
| ChromaDB | | PyQt | CARLA | Docker |

---

## Specialization

| Physical AI & Robotics | Simulation & Sensor | AI Development | Backend & Leadership |
| --- | --- | --- | --- |
| Multi-Robot Fleet Management | CARLA Simulator | RAG Systems | FastAPI / Django |
| Task Scheduling & Collision Avoidance | LiDAR / Camera / IMU | Multi-Agent AI (LangGraph) | System Architecture |
| ROS 2 / Nav2 / Domain Bridge | Sensor Fusion & Data Pipeline | LLM Integration | Project Management |

---

## Contact

[![GitHub](https://img.shields.io/badge/GitHub-100000?style=flat-square&logo=github&logoColor=white)](https://github.com/NGGW519)
[![Email](https://img.shields.io/badge/Email-D14836?style=flat-square&logo=gmail&logoColor=white)](mailto:srrd1357@gmail.com)
