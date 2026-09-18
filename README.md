## KBO Future Scout

KBO 퓨처스리그 선수 데이터를 기반으로 선수의 현재 경기력, 성장 추세, 향후 1군 성장 가능성을 분석하는 데이터 기반 AI 스카우팅 플랫폼입니다.

본 프로젝트는 **2026 경기스포츠산업 공모전 - 경기력 향상 기술 / AI 기반 경기분석** 분야 출품을 목표로 진행합니다.

---

## Overview

퓨처스리그에는 많은 유망주가 존재하지만 단순 타율, 홈런, 평균자책점 같은 기본 기록만으로는 선수의 성장 가능성을 충분히 판단하기 어렵습니다.

KBO Future Scout는 다음 요소를 함께 분석합니다.

- 선수의 나이
- 현재 경기력
- 시즌별 성장 추세
- 동연령대 대비 성과
- 과거 유사 선수의 성장 패턴
- 이후 1군에서의 실제 성과

이를 바탕으로 선수의 성장 가능성을 정량적으로 분석하고, 강점과 개선 포인트를 데이터 기반으로 제공합니다.

---

## Core Question

> 퓨처스리그에서 좋은 성적을 기록한 선수 중 어떤 선수가 실제로 1군에서 성장할 가능성이 높은가?

본 프로젝트는 과거 퓨처스리그 기록과 이후 1군 기록을 연결해 이 질문에 데이터 기반으로 접근합니다.

---

## Main Features

### Future Star Ranking

퓨처스리그 선수의 경기력과 성장 지표를 기반으로 주목할 선수를 탐색합니다.

### Player Performance Analysis

타자와 투수의 주요 경기 지표를 분석합니다.

**Batter**
- AVG
- OBP
- SLG
- OPS
- ISO
- BB%
- K%
- BB/K
- HR%

**Pitcher**
- ERA
- WHIP
- K/9
- BB/9
- HR/9
- K-BB%

### Growth Trend

여러 시즌의 기록을 연결해 선수의 경기력이 실제로 개선되고 있는지 확인합니다.

### Potential Score

나이, 경기력, 성장 추세, 과거 선수 패턴 등을 기반으로 선수의 성장 가능성을 하나의 지표로 표현합니다.

### Similar Player Analysis

현재 선수와 기록 패턴이 유사했던 과거 퓨처스리그 선수를 탐색하고 이후 성장 경로를 비교합니다.

### AI Scout Report

분석 결과를 바탕으로 다음 내용을 자연어 리포트 형태로 제공합니다.

- 강점
- 위험 요소
- 성장 포인트

---

## Data

### KBO Futures League

Source:

- https://www.koreabaseball.com/Futures/Player/Hitter.aspx
- https://www.koreabaseball.com/Futures/Player/Pitcher.aspx

사용 범위:

- 2010 ~ 2026

활용 목적:

- 퓨처스 선수 경기력 분석
- Feature Engineering
- 성장 추세 분석
- 머신러닝 입력 데이터

### KBO First Team

사용 범위:

- 2011 ~ 2026

활용 목적:

- 퓨처스 선수의 이후 1군 성과 확인
- 성장 결과 Label 생성
- 과거 선수 성장 패턴 검증

### Prediction Structure

Futures Season t  
→ First Team t+1 ~ t+3  
→ Growth Outcome

학습 데이터:

- 2010 ~ 2023 Futures

현재 예측 대상:

- 2024 ~ 2026 Futures Players

### Naver Sports Internal API

Base URL:

- https://api-gw.sports.naver.com

사용 예시:

- https://api-gw.sports.naver.com/statistics/categories/kbo/seasons/{year}/players?playerType=HITTER
- https://api-gw.sports.naver.com/statistics/categories/kbo/seasons/{year}/players?playerType=PITCHER

네이버 스포츠 API는 공식 개발자용 공개 API가 아니므로 핵심 학습 데이터로 사용하지 않고, 다음과 같은 보조 용도로만 활용합니다.

- 1군 기록 검증
- 경기 일정
- 경기 결과
- 향후 경기 단위 분석 기능
- 데이터 보완

---

## Data Pipeline

KBO Futures Data  
→ Data Cleaning  
→ Player Information Join  
→ Feature Engineering  
→ First-Team Performance Join  
→ Machine Learning  
→ Potential Score  
→ Similar Player Analysis  
→ AI Scout Report

---

## Machine Learning

초기 모델 후보:

- Logistic Regression
- Random Forest
- XGBoost
- LightGBM

모델 결과는 단순 예측값만 제공하지 않고 Feature Importance와 SHAP 등을 활용해 선수가 왜 높은 또는 낮은 평가를 받았는지 설명하는 것을 목표로 합니다.

---

## Tech Stack

### Frontend
- React
- Vite

### Backend
- FastAPI

### Data Analysis
- Python
- Pandas
- NumPy

### Machine Learning
- Scikit-learn
- XGBoost
- LightGBM

### Visualization
- Plotly

### Database
- PostgreSQL
- Supabase

### Infrastructure
- Docker
- Docker Compose

### Version Control
- Git
- GitHub

---

## Architecture

KBO / External Data  
→ Data Collection  
→ Data Processing  
→ Machine Learning  
→ FastAPI  
→ React  
→ User

---

## Project Structure

kbo-future-scout/

- frontend/
- backend/
- analysis/
- data/
  - raw/
  - interim/
  - processed/
  - external/
- models/
- notebooks/
- scripts/
- docs/
- docker-compose.yml
- README.md
- requirements.txt

---

## Project Goal

본 프로젝트는 미래의 스타를 확정적으로 예측하는 시스템을 목표로 하지 않습니다.

선수의 실제 성장은 부상, 출장 기회, 코칭, 팀 상황 등 다양한 외부 요인의 영향을 받습니다.

KBO Future Scout는 과거 기록과 성장 패턴을 활용해 선수의 성장 가능성을 정량적으로 탐색하고, 스카우팅과 선수 분석을 보조하는 것을 목표로 합니다.