# 데이터의 가정과 해석 범위를 검증합니다

**이상민 (Sangmin Lee)** - 광운대학교 국제통상학 전공 · 경영학 복수전공 (2027년 2월 졸업예정)

경제·경영의 맥락 위에서 데이터를 분석하고, “이 결과로 무엇을 결정할 수 있는가”와 “어디까지는 말할 수 없는가”를 함께 정리하는 데이터 분석가를 지향합니다.

숫자를 크게 보이게 만드는 것보다 **그 숫자의 해석 범위를 명확히 하는 것**이 분석의 신뢰를 만든다고 생각합니다.

**Portfolio:** [abovemin.com/portfolio/submission](https://abovemin.com/portfolio/submission)

**Email:** aquariusmin01@naver.com

---

## What I Focus On

| Focus | How I Show It |
| :--- | :--- |
| 문제 정의 | 분석 전에 어떤 의사결정을 돕는지 먼저 정리합니다. |
| 지표 설계 | 원자료에 직접 없는 현상은 대체 지표로 설계하고 해석 범위를 제한합니다. |
| 데이터 QA | 높은 수치가 나오면 병합 키, 변수 정의, 정렬 오류를 먼저 확인합니다. |
| 모델 해석 | SHAP, 회귀 결과, R²를 인과나 예측 성과로 과장하지 않습니다. |
| AI 활용 | 코드 초안과 대안 탐색에는 AI를 쓰되, 문제 정의와 검증 기준은 직접 결정합니다. |

---

## Representative Projects

| Project | Core Question | What I Focused On |
| :--- | :--- | :--- |
| [Busan Urban Rail Dwell Analysis](https://github.com/aquariusmin/busan-station-dwell) | 승하차 데이터만으로 체류 전환 실패 구간을 찾을 수 있을까? | 대체 지표 설계, 음수 결과 진단, min-shift 보정, 정책 후보 재해석 |
| [Customer Churn XAI](https://github.com/aquariusmin/kw-corp-churn-strategy-analysis) | 이탈 예측을 어떻게 고객군별 개입 우선순위로 바꿀 수 있을까? | 모델 비교, SHAP 기반 해석, 실험 검증 필요성 구분 |
| [Satellite GDP Insight](https://github.com/aquariusmin/Satellite-GDP-Insight) | 야간조도는 GDP의 대체 경제지표로 어디까지 유효한가? | 회귀 분석, 데이터 정합성 검증, 재현 스크립트, 해석 한계 명시 |

---

## Project Notes

### [Busan Urban Rail Dwell Analysis](https://github.com/aquariusmin/busan-station-dwell)

공개 데이터에 없는 “체류”를 승하차 기록만으로 직접 측정한다고 주장하지 않고, **체류 전환 가능성**을 보는 대체 지표로 설계한 프로젝트입니다.

- 시간대별 승하차 40,544행(2026.01-06, 112개 역)을 활용해 철도 기인 순체류 흐름을 구성
- 초기 산식이 주거형 역에서 음수로 붕괴하는 문제를 발견하고, 데이터 오류가 아니라 지표 가정의 문제로 진단
- 일별 최저점 기준 min-shift 보정을 적용해 유입형/주거형 패턴을 분리
- 승하차량 순위가 아니라 체류 전환 실패 구간을 정책 후보로 재해석
- 해운대역 사례에서 숙박업소 체크아웃 가설은 신호를 확인했지만 전체 유입 설명 비중이 작아 핵심 설명으로 사용하지 않음

**해석 범위:** 개인 단위 실제 체류 로그가 아니라 승하차 기반 대체 지표입니다. 카드 매출, Wi-Fi/통신 체류 로그 등 외부 데이터 검증이 다음 단계입니다.

### [Customer Churn XAI](https://github.com/aquariusmin/kw-corp-churn-strategy-analysis)

이탈 가능성 예측에서 끝내지 않고, 모델 결과를 고객군별 개입 우선순위와 실험 검증 계획으로 바꾸는 데 초점을 둔 프로젝트입니다.

- 통신사 고객 7,043건을 정제하고 7개 분류모델을 비교
- Gradient Boosting 기준 ROC-AUC 0.841을 `reproduce.py`로 재현 가능하게 정리
- SHAP 기반 해석으로 월 단위 계약, 짧은 가입기간, 높은 월 요금, 보안/기술지원 미가입 등을 모델 판단 신호로 확인
- 이탈률 5.0%p 감소는 실제 달성치가 아니라 실행 전 제안 목표로 구분

**해석 범위:** SHAP은 모델 판단 설명이지 인과관계 증명이 아닙니다. 실제 캠페인 효과는 통제 실험 또는 A/B 테스트로 검증되어야 합니다.

### [Satellite GDP Insight](https://github.com/aquariusmin/Satellite-GDP-Insight)

북한 야간 위성 이미지와 통계 신뢰성 문제에서 출발해, 야간조도가 국가별 경제 수준의 보조 지표로 어디까지 유효한지 검증한 프로젝트입니다.

- 2019-2023년 164개국 820개 국가-연도 데이터를 구성
- `ln(GDP) ~ ln(야간조도)` 단순회귀에서 R² = 0.819, N = 791의 표본 내 설명력을 확인
- 도시인구·전력접근성 조절효과는 유의하지만 설명력 증가분은 작다고 해석
- 기존 `.xlsx` 조도 열이 GDP와 국가-연도 기준으로 어긋난 문제를 발견
- `.sav` 기준 `reproduce.py`로 기준 결과를 재계산하도록 정리

**해석 범위:** GDP 예측 정확도, 인과관계, 새로운 학술 방법론을 주장하지 않습니다. 대체 경제지표 검증과 데이터 QA 사례로 설명합니다.

---

## Explore / Archive

| Project | How I Use It |
| :--- | :--- |
| [Arctic Route Accessibility](https://github.com/aquariusmin/arctic-route-accessibility-analysis) | 낯선 도메인을 AI 도움으로 학습하며 수행한 탐색형 프로젝트입니다. 대표 역량보다는 데이터 출처 고정, 합성 대체값 구분, 검증 기준 설계 경험으로 배치합니다. |
| [tqt / Quant Trading](https://github.com/aquariusmin/toss-api-quant-trading) | 수익률 자랑이 아니라 walk-forward OOS, API 제약 반영, 수익률과 낙폭의 교환관계 해석 경험으로 설명합니다. |
| [Quant Trading Fleet](https://github.com/aquariusmin/quant_trading_fleet) | FastAPI, SQLite/SQLAlchemy, React/TypeScript 기반의 운영 대시보드 구현 경험입니다. |
| [Korean Air Valuation](https://github.com/aquariusmin/koreanair_equity_research) | 투자 의견이 아니라 재무 가정, WACC, FCF, 상대가치평가 간 충돌을 검토한 분석 연습입니다. |
| [Financial AI Model Study](https://github.com/aquariusmin/financial-ai-model-study) | 복잡한 모델이 항상 좋은 일반화 성능을 내는 것은 아니라는 점을 확인한 모델 비교 학습 기록입니다. |

---

## AI-assisted Analysis

AI는 분석 판단을 대체하는 도구가 아니라, 구현 속도를 높이고 대안을 탐색하기 위한 보조 도구로 사용했습니다.

제가 직접 결정한 것은 다음과 같습니다.

- 분석 질문과 문제 정의
- 사용할 데이터와 제외할 데이터
- 변수와 지표의 의미
- 모델 또는 통계 방법 선택 기준
- 검증 기준과 실패 판단
- 최종 해석과 한계 문장

AI를 활용한 부분은 주로 코드 초안 작성, 문서 구조화, 방법론 대안 탐색, 테스트 케이스 보조였습니다. 특히 북극항로처럼 AI 도움을 많이 받은 작업은 대표 프로젝트가 아니라 Explore로 낮춰 배치했습니다.

---

## Skills

| Area | Tools / Methods |
| :--- | :--- |
| Data Analysis | Python, SQL, Pandas, NumPy, Excel, SPSS |
| Statistics / Modeling | Regression, Classification, OLS, Model Evaluation, Train/Test Validation |
| Interpretability | SHAP, Feature Importance, Model Diagnostics |
| Validation | Data QA, Reproducibility, Assumption Check, Limitation Notes |
| Web / Product | Next.js, TypeScript, Supabase, Vercel, FastAPI |

---

## Education & Certificates

**광운대학교** 경영대학 · 국제통상학부 국제통상전공 / 경영학 복수전공 - 2027년 2월 졸업예정

- 전체 3.86 / 4.50 · 주전공 3.96 · 복수전공 4.25 (총취득 133학점, 백분율 92.7)
- 데이터·분석 과목: 빅데이터분석 A+ · 금융과인공지능 A+ · 경영데이터베이스 A+ · 시장조사방법론 A+ · 경제경영통계 A+ · 재무분석 A+

**자격 / 어학**

- ADsP (데이터분석 준전문가) · 글로컬마케터 3급
- 빅데이터분석기사 필기 합격, 실기 결과 대기 · SQLD 준비 중
- G-TELP Level 2 76점 (2026.07)
- 호주 단기 어학연수 1개월 (2025.02)

**병역** - 대한민국 공군 병장 만기전역 (2021.07-2023.04)

---

## Experience

**재무학회 운영 지원** (2025)

학술행사 운영 및 주최·연사·참가자 간 행정 조율을 담당하며 금융 산업의 실무 흐름과 이해관계자 조정 과정을 경험했습니다.

**뮤엠영어 교육 지원** (2024.04-2025.01)

학생별 성취도 데이터 관리와 일일 학습 이행도 점검을 수행하며 관리 데이터를 체계화했습니다.

**비너발트 홀 운영** (2023.06-2023.09)

피크타임 고객 응대와 테이블 운영을 담당하고, 유입 패턴에 따른 서빙 동선 개선을 제안했습니다.
