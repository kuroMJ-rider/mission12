# mission12
# 🚲 자전거 대여 수요 예측 및 운영 최적화 (Bike Sharing Demand)

## 📌 1. 프로젝트 개요 (Project Overview)
- **페르소나:** 자전거 대여 시스템 운영 담당자
- **분석 목표:** 날씨, 시간, 계절 등 환경 변수를 활용하여 특정 시간대의 총 자전거 대여 수(Count)를 정확히 예측하는 머신러닝 모델 개발
- **비즈니스 목적:** 대여 패턴 분석을 통한 시간대별/날씨별 자전거 배치(Rebalancing) 효율 극대화 및 사용자 맞춤형 운영 전략 도출
- **작성자:** 전미정 (MJ)

## 📊 2. 평가 지표 (Evaluation Metric)
- **RMSLE (Root Mean Squared Logarithmic Error)**
- **사용 이유:** 수치적 단순 오차가 아닌 '비율 오차'에 집중하며, 대여량이 적은 구간과 많은 구간의 오차를 고르게 반영하여 운영 관점(과대/과소 재고 배치 리스크)에서 적합한 지표로 활용

## ⚙️ 3. 기술 스택 (Tech Stack)
- **Language:** Python
- **Libraries:** Pandas, NumPy, Scikit-learn, XGBoost, Matplotlib, Seaborn
- **Environment:** Google Colab

## 🚀 4. 모델링 진행 과정 및 성능 개선 (Modeling Process)
점진적인 피처 엔지니어링과 모델 고도화를 통해 **최초 모델 대비 약 66%의 성능(오차) 개선**을 달성했습니다.

| 단계 | 모델 및 적용 기법 | 성과 (RMSLE) | 핵심 내용 |
|:---:|:---|:---:|:---|
| **1차** | Baseline (선형 회귀) | `1.0250` | 기본 데이터 전처리 및 탐색적 데이터 분석(EDA) 적용 |
| **2차** | Linear + OHE | `0.5808` | 계절, 날씨, 시간 등 범주형 변수에 원-핫 인코딩(One-Hot Encoding) 적용하여 비선형 패턴 학습 유도 |
| **3차** | XGBoost + 파생 변수 | `0.3450` | 출퇴근 시간(`is_rush_hour`), 체감온도 등 복합 파생 변수 추가 및 희소 행렬에 강한 트리 기반 앙상블 모델 도입 |
| **최종** | **Two-Track 모델 (XGBoost)** | **`0.3398`** | **Casual(비회원)과 Registered(정기권) 타겟을 분리(Target Separation)하여 각각 학습 후 최종 예측값을 합산하는 기법 도입** |

## 💡 5. 핵심 인사이트 및 운영 전략 (Key Insights & Strategies)
1. **수요 양극화와 맞춤형 운영 (Casual vs Registered)**
   - **정기권(Registered):** 평일 출퇴근 시간(08시, 17~18시)에 수요가 폭발하는 M자형 패턴. 주요 오피스 환승역 중심으로 선제적 대규모 재배치(Rebalancing) 집중.
   - **비회원(Casual):** 날씨가 좋은 주말 오후(12~16시)에 역U자형 패턴으로 수요 증가. 기상 예보와 연동하여 주요 공원/관광지에 자전거 집중 배치 및 프로모션 전개.
2. **골든 타임의 재발견**
   - 대여량이 0에 수렴하는 새벽 시간대(03~05시)를 단순 방치 시간이 아닌, 전사적 자전거 일제 정비 및 대형 트럭을 동원한 재배치의 '유지보수 골든 타임'으로 활용.

## 🔮 6. 향후 개선 과제 (Future Roadmap)
- **Lag / Rolling Feature 도입:** 전일/전주 동시간대 대여량 등 시계열 연속성을 반영하는 파생 변수 추가
- **Hyperparameter Tuning:** Optuna 등 최적화 프레임워크를 활용한 모델 정밀 튜닝
- **Ensemble / Stacking:** LightGBM, CatBoost 등 이종 모델과의 스태킹 앙상블을 통한 일반화 성능 극대화
- **External Data:** 상세 강수량, 지역 축제/이벤트 등 외부 데이터 결합으로 설명력 보완
- 
- <img width="1490" height="590" alt="다운로드 (7)" src="https://github.com/user-attachments/assets/4da20957-183b-48a5-9fe7-799015dae1e3" />

- <img width="1189" height="590" alt="다운로드 (8)" src="https://github.com/user-attachments/assets/2efbee51-8406-4da9-96e1-52081cb6d628" />
