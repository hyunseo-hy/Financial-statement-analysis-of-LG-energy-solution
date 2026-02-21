# Financial Statement Analysis of LG Energy Solution

LG에너지솔루션의 재무제표를 분석하고 기업가치를 추정하는 프로젝트입니다.

## 📁 구조

```
Financial-statement-analysis-of-LG-energy-solution/
├── 01_financial_statements/        # 재무제표 데이터 및 추출 코드
│   ├── LG에너지솔루션_재무제표.xlsx
│   ├── LG에너지솔루션_재무제표_수정본.xlsx
│   └── 재무제표_추출.py
├── 02_ratio_analysis/              # 재무비율 분석
│   ├── 비율분석_계산_수정본.xlsx
│   ├── 비율분석_문제풀이.pdf
│   └── 비율분석.py
├── 03_estimated_statements/        # 추정재무제표
│   ├── 추정재무제표.xlsx
│   └── 추정재무제표_작성.py
└── 04_valuation/                   # 기업가치 평가
    └── RIM_EVA_계산.py
```

## 📌 분석 단계

1. **재무제표 수집** — DART `dart_fss` 라이브러리로 공시 데이터 추출
2. **비율 분석** — 수익성, 유동성, 레버리지, 효율성 지표 계산
3. **추정재무제표 작성** — 미래 손익계산서 및 재무상태표 추정
4. **기업가치 평가 (RIM)** — Ohlson 잔여이익 모델 기반 주주가치 산출
5. **기업가치 평가 (EVA)** — 경제적 부가가치 모델 기반 주주가치 산출

## 🛠 사용 기술

![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=flat&logo=pandas&logoColor=white)
![Excel](https://img.shields.io/badge/Excel-217346?style=flat&logo=microsoft-excel&logoColor=white)
