# 🤖 AI Interviewer Agent v2.0
### Resume-driven Multi-stage Interview Agent with Reflection & Strategy Control

본 프로젝트는 이력서(PDF/DOCX)를 입력으로 받아  
**면접 질문 생성 → 답변 평가 → 평가 타당성 검증(reflection) → 전략 전환 →  
최종 면접 피드백 보고서 생성**까지 수행하는  
**LangGraph 기반 다단계 AI 면접관 Agent**입니다.

단순 Q&A 챗봇이 아닌,  
**면접 전략·평가·흐름 제어를 명시적으로 모델링한 Agent 구조**를 목표로 합니다.

---

## 📌 Project Overview

### 🎯 목표
- 이력서 기반 자동 면접 진행 Agent 구현
- 질문 생성·답변 평가·종료 판단을 **규칙 + LLM 혼합 구조**로 설계
- 평가의 신뢰성을 높이기 위한 **Reflection(재검토) 단계 도입**
- 전략별 면접 결과를 **보고서 형태로 요약**

---

## 🧩 Input Data

- **입력 형식**: PDF / DOCX 이력서
- **주요 입력 정보**
  - 학력 / 경력
  - 프로젝트 경험
  - 기술 스택
  - 자기소개 문항
- **전처리**
  - 텍스트 추출 (PDF, DOCX)
  - 전체 요약 및 핵심 키워드 추출

---

## 🧠 Problem Definition

### 왜 다단계 면접 Agent인가?
- 실제 면접은 **질문 생성 → 답변 평가 → 다음 질문 판단**의 반복 구조
- 단일 LLM 호출로는
  - 질문의 일관성 유지
  - 평가 기준 통제
  - 면접 종료 판단이 어려움

👉 따라서 면접 과정을 **상태 기반(State-driven) Agent**로 재정의

---

## 🧱 Agent Architecture
Resume Input
↓
Resume Analysis & Summary
↓
Question Strategy Planning
↓
[ Interview Loop ]
Question → Answer → Evaluation → Reflection → Decision
↓
Interview Termination
↓
Final Feedback Report

---

## 🧠 Interview Strategy Design

면접은 다음 5개 전략 영역을 기준으로 진행됩니다.

- 경력 및 경험
- 동기 및 커뮤니케이션
- 논리적 사고
- 기술 역량 및 전문성
- 성장 가능성 및 자기주도성

각 전략은:
- 사전 정의된 질문 방향
- Vector DB 기반 참조 질문
- LLM 생성 질문  
을 조합하여 구성됩니다.

---

## 🔍 Step 1. Resume Pre-processing

- 이력서 전체 요약 생성
- 전략별 질문 생성에 활용할 핵심 키워드 추출
- 전략 영역별 질문 방향 자동 설계
- 초기 질문 자동 선택

---

## 🤖 Step 2. Interview Agent (LangGraph)

### 주요 노드 구성
- **evaluate**: 답변 평가 (관련성 / 구체성)
- **reflect**: 평가 타당성 검증
- **re_evaluate**: 재평가 (1회 제한)
- **decide**: 다음 행동 결정
- **generate**: 다음 질문 생성
- **summarize**: 최종 피드백 생성

---

## 🔁 Reflection Mechanism

다음 조건에서 평가 재검토 수행:
- 답변이 지나치게 짧은 경우
- 평가 결과 간 논리적 모순 발생
- 근거 대비 과도하게 낮은 평가

> 무한 루프 방지를 위해 **Reflection은 최대 1회만 허용**

---

## 🔀 Interview Flow Control

다음 기준에 따라 면접 흐름을 제어합니다.

1. 질문-답변 횟수 초과 시 종료
2. 아직 진행하지 않은 전략 우선 선택
3. 낮은 평가 발생 시 동일 전략 심화 질문
4. 모든 전략 소진 시 종료

---

## 🧾 Step 3. Feedback Report Generation

### 전략별 피드백
- 답변 요약
- 강점
- 보완점
- 평가 경향

### 종합 피드백
- 전체 면접 인상
- 핵심 강점
- 개선 필요 역량

---

## 🛠 Tech Stack

- Python
- LangChain / LangGraph
- OpenAI API
- Chroma Vector DB
- PyMuPDF, python-docx
- Gradio

---

## 📊 Key Insights

- 면접 Agent에서는 **모델 성능보다 흐름 설계가 중요**
- Reflection 구조는 평가 신뢰도 향상에 효과적
- 전략 기반 질문 설계는 면접 일관성을 크게 개선

---

## ⚠️ Limitations

- 실제 음성 면접(STT/TTS) 미적용
- 회사/직무별 맞춤 전략은 기본 수준
- 평가 점수의 정량화 한계

---

## 🚀 Future Work

- 직무·기업별 면접 전략 템플릿
- 음성 기반 실시간 면접
- 평가 점수 시각화 대시보드
- PDF 면접 리포트 자동 생성

---

## ✍️ Summary
> 이력서 기반 면접 과정을 상태 기반 Agent로 재구성하여  
> 질문 생성, 평가, 흐름 제어를 구조적으로 설계한  
> 다단계 AI 면접관 Agent 프로젝트

