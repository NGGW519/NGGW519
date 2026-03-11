<div align="center">

# Namgung Geonwoo

**Physical AI Engineer**

AI that understands and acts in the physical world.

Seoul, Korea

</div>

---

## About

소프트웨어 위의 AI가 아니라, 물리 세계에서 동작하는 AI를 만듭니다.

ROS 2 기반 다중 로봇 Fleet Management System을 설계하고 구현하면서, AI 판단이 실제 로봇의 움직임으로 이어지는 전체 파이프라인을 경험했습니다. 로봇 5대(서빙로봇 3대 + 로봇팔 2대)를 격리된 네트워크 도메인에서 통합 관제하는 FMS를 단독 설계/구현하고, RAG/LLM 기반 AI 시스템으로 장관상을 수상하며 — 로보틱스와 AI 양쪽에서 실전 경험을 쌓고 있는 엔지니어입니다.

---

## Highlights

| Robotics | AI |
|---|---|
| 서빙로봇 3대 + 로봇팔 2대 통합 관제 **FMS** 설계 및 구현 | RAG/LLM 기반 **고용노동부장관상** 수상 |
| FMS 전 모듈 단독 개발 (스케줄링, 충돌 회피, 경로 계획, 장애 복구) | 멀티 에이전트 워크플로우 (LangGraph) 설계 |
| 5개 ROS_DOMAIN_ID 격리 환경 간 Domain Bridge 구축 | 6개 AI/ML 프로젝트 완료 |

---

# Projects

## 1. Robotics - [Kitchmatics](https://github.com/addinedu-roscamp-4th/roscamp-repo-1)

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

### - My Role

| 구분 | 내용 |
|---|---|
| **Project Manager** | 6인 팀 리드, 시스템 아키텍처 설계, 모듈 간 인터페이스 정의, 스프린트 운영 |
| **FMS 설계 및 구현** | 주문-서빙-복귀 전 과정을 관제하는 Fleet Management System 단독 설계/구현 |
| **GUI 개발** | 운영자용 실시간 모니터링 대시보드, 주문 접수 및 수동 제어 인터페이스 (TCP 기반) |

### - FMS 상세 모듈

주문 접수부터 조리, 품질 검사, 서빙, 복귀까지 전 과정을 자동으로 관제하는 시스템을 단독 설계/구현했습니다.

| 모듈 | 기능 |
|---|---|
| **Task Scheduler** | 주문 큐 관리, 픽업 슬롯 할당, 우선순위 기반 태스크 스케줄링 |
| **Fleet Controller** | 서빙로봇 3대 + 로봇팔 2대 실시간 상태 모니터링, 가용 로봇 자동 배정 |
| **Zone Manager** | 다중 로봇 충돌 회피, 구역 예약 시스템, 교착 상태 감지 및 해소 |
| **Path Planner** | Navigation Graph 기반 최적 경로 계획 |
| **Error Detection & Recovery** | 장애 자동 감지 및 복구 핸들러 |
| **Domain Bridge** | ROS_DOMAIN_ID 격리 환경에서 5개 도메인 간 통신 브릿지 구축 |
| **fleet_interfaces** | 커스텀 ROS 2 메시지 패키지 설계 (11개 메시지 타입) |
| **Testing** | 단위/통합/E2E 155개 이상의 테스트 케이스 |

---

## 2. AI & ML

**[고향으로 ON](https://github.com/NGGW519/7th-kDT-HACKATHON)** — 고용노동부장관상 수상작

RAG 기반 중장년층 고향 정착 지원 플랫폼. 음성 UI/UX, 지역별 맞춤 정보 제공.
- 기술: React Native, TypeScript, FastAPI, OpenAI GPT, RAG, ChromaDB, MySQL
- 역할: 팀장, AI 시스템 설계 및 구현

**[CLIKCA](https://github.com/SKNETWORKS-FAMILY-AICAMP/SKN13-FINAL-1TEAM)** — AI 업무 파트너

멀티 에이전트 기반 업무 자동화 시스템. 하이브리드 검색(키워드+벡터), LangGraph 워크플로우 라우팅.
- 기술: Electron, React, FastAPI, LangGraph, OpenAI, ChromaDB, AWS S3
- 역할: AI 워크플로우 아키텍처 설계 및 LangGraph 구현

**[의학 논문 팩트체킹 챗봇](https://github.com/SKNETWORKS-FAMILY-AICAMP/SKN13-3rd-1TEAM)**

3개 의학 DB(Europe PMC, PubMed, MedRxiv) 통합 RAG 파이프라인. RAGAS 자동 평가 시스템.
- 기술: GPT-4.1, ChromaDB, RAG, RAGAS, Streamlit
- 역할: RAG 파이프라인 설계 및 RAGAS 평가 구현

---

## 3. Web Services

**[지금, 서울](https://github.com/SKNETWORKS-FAMILY-AICAMP/SKN13-4th-1TEAM)** — AI 시정 Q&A

서울 열린데이터 광장 API 통합, FAQ 자동 응답, 관리자 대시보드. 2일 개발.
- 기술: Django, LangChain, LangGraph, ChromaDB, MySQL

**[DRMC](https://github.com/SKNETWORKS-FAMILY-AICAMP/SKN13-1st-2Team)** — 자동차 리콜 정보 서비스

리콜 정보 시각화, 맞춤 추천, 웹 크롤링 자동화. 2일 개발.
- 기술: Streamlit, MySQL, Selenium, Python

---

## 4. Data Science

**[환자 이탈 예측 모델](https://github.com/SKNETWORKS-FAMILY-AICAMP/SKN13-2nd-7Team)**

클래스 불균형 해결(SMOTE), F1 Score 11.4% 개선. 주요 이탈 인자 식별.
- 기술: Python, XGBoost, SMOTE, Scikit-learn

---

## Tech Stack

<div align="center">

| AI & ML | Backend | Frontend | Robotics | Database & Infra |
|---------|---------|----------|----------|-----------------|
| ![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white) | ![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white) | ![React](https://img.shields.io/badge/React-20232A?style=flat-square&logo=react&logoColor=61DAFB) | ![ROS2](https://img.shields.io/badge/ROS2-22314E?style=flat-square&logo=ros&logoColor=white) | ![PostgreSQL](https://img.shields.io/badge/PostgreSQL-336791?style=flat-square&logo=postgresql&logoColor=white) |
| ![OpenAI](https://img.shields.io/badge/OpenAI-412991?style=flat-square&logo=openai&logoColor=white) | ![Django](https://img.shields.io/badge/Django-092E20?style=flat-square&logo=django&logoColor=white) | ![TypeScript](https://img.shields.io/badge/TypeScript-007ACC?style=flat-square&logo=typescript&logoColor=white) | ![Nav2](https://img.shields.io/badge/Nav2-22314E?style=flat-square&logo=ros&logoColor=white) | ![MySQL](https://img.shields.io/badge/MySQL-005C84?style=flat-square&logo=mysql&logoColor=white) |
| ![LangChain](https://img.shields.io/badge/LangChain-121212?style=flat-square&logo=chainlink&logoColor=white) | ![Flask](https://img.shields.io/badge/Flask-000000?style=flat-square&logo=flask&logoColor=white) | ![Electron](https://img.shields.io/badge/Electron-2B2E3A?style=flat-square&logo=electron&logoColor=9FEAF9) | ![Python](https://img.shields.io/badge/Domain_Bridge-22314E?style=flat-square&logo=ros&logoColor=white) | ![AWS](https://img.shields.io/badge/AWS-232F3E?style=flat-square&logo=amazon-aws&logoColor=white) |
| ![ChromaDB](https://img.shields.io/badge/ChromaDB-FF6B6B?style=flat-square&logo=database&logoColor=white) | | ![PyQt](https://img.shields.io/badge/PyQt-41CD52?style=flat-square&logo=qt&logoColor=white) | | |

</div>

---

## Specialization

| Physical AI & Robotics | AI Development | Backend & Leadership |
|---|---|---|
| Multi-Robot Fleet Management | RAG Systems | FastAPI / Django |
| Task Scheduling & Collision Avoidance | Multi-Agent AI (LangGraph) | System Architecture |
| ROS 2 / Nav2 / Domain Bridge | LLM Integration | Project Management |

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
