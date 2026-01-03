# 📱 Smartphone Sensor-Based Hierarchical Motion Classification

스마트폰 가속도·자이로 센서 데이터를 활용하여  
사용자의 행동을 **계층적 분류(Hierarchical Classification)** 방식으로 예측하는 프로젝트입니다.

본 프로젝트는 기존의 6개 행동 다중 분류 문제를  
**정적 / 동적 행동 → 세부 행동 분류**의 두 단계로 재구성하여  
센서 데이터의 물리적 특성을 효과적으로 반영하는 것을 목표로 합니다.

---

## 📌 Project Overview

- **Task**
  - 스마트폰 센서 데이터 기반 사용자 행동 인식
- **Dataset**
  - UCI Human Activity Recognition (HAR) Dataset
- **Total Classes**
  - LAYING, SITTING, STANDING  
  - WALKING, WALKING_UPSTAIRS, WALKING_DOWNSTAIRS

---

## 🧠 Key Idea: Hierarchical Classification

기존 방식  
- 6개 행동을 한 번에 분류 →  
  정적 행동(SITTING / STANDING) 간 혼동 발생

개선 방식  
1. **Stage 1**  
   - 정적(0) / 동적(1) 행동 이진 분류  
2. **Stage 2**  
   - 정적 행동 → LAYING / SITTING / STANDING  
   - 동적 행동 → WALKING / UP / DOWN  

➡️ 문제를 단계적으로 분해하여 분류 성능과 해석력을 동시에 확보

---

## 📊 Exploratory Data Analysis (EDA)

- RandomForest 기반 **Feature Importance 분석**
- 주요 관찰 사항
  - 중력 및 각도 관련 feature가 LAYING 구분에 매우 중요
  - 정적/동적 행동은 센서 에너지·주기성에서 명확한 차이를 보임
- 결론
  - 정적/동적 분리는 데이터 관점에서 매우 안정적

---

## 🏗️ Modeling Architecture

### Stage 1: Static vs Dynamic Classification
- Model: Deep Neural Network (Binary Classification)
- Input: 561 sensor features
- Output: is_dynamic (0 or 1)
- Accuracy: **~100%**

### Stage 2-1: Static Activity Classification
- Classes: LAYING / SITTING / STANDING
- Accuracy: **~93%**
- 주요 혼동: SITTING ↔ STANDING

### Stage 2-2: Dynamic Activity Classification
- Classes: WALKING / WALKING_UPSTAIRS / WALKING_DOWNSTAIRS
- Accuracy: **~97%**

---

## 🔄 End-to-End Pipeline

- 전처리 → 스케일링 → 단계별 예측 → 성능 평가
- 새로운 데이터(test)에 바로 적용 가능하도록 함수화
- 실제 서비스 구조를 고려한 파이프라인 구성

---

## 🧪 (Optional) Multi-Task Learning Model

- 하나의 네트워크에서
  - is_dynamic
  - activity
  를 동시에 예측
- 목적
  - 계층 구조를 단일 모델로 통합 가능성 실험
- 결과
  - 성능은 유사
  - 해석력 측면에서는 단계적 모델이 더 명확

---

## 📈 Performance Summary

| Task | Accuracy |
|-----|---------|
| Static vs Dynamic | ~1.00 |
| Static Activity | ~0.93 |
| Dynamic Activity | ~0.97 |
| Overall (Pipeline) | ~0.96 |

---

## ⚠️ Limitations

- SITTING / STANDING 구분의 센서 물리적 한계
- 시계열 구조를 직접 활용하지 않음
- 개인별(subject) 특성 미반영

➡️ 단, 문제 구조 재설계를 통해 한계를 완화

---

## 🛠️ Tech Stack

- Python
- Pandas, NumPy
- Scikit-learn
- TensorFlow / Keras
- Matplotlib, Seaborn

---

## ✨ Summary

> 센서 데이터의 물리적 특성을 고려하여  
> 행동 인식 문제를 계층적으로 재정의한  
> **Hierarchical Motion Classification 프로젝트**

