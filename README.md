# 📚 책 줄거리 요약 프로그램

![Python](https://img.shields.io/badge/Python-3.9+-3776AB?style=flat&logo=python&logoColor=white)
![PyQt5](https://img.shields.io/badge/UI-PyQt5-41CD52?style=flat)
![HuggingFace](https://img.shields.io/badge/🤗-HuggingFace-FFD21E?style=flat)
![KoT5](https://img.shields.io/badge/Model-KoT5-FF6F00?style=flat)

---

## 📌 프로젝트 개요

현대인의 일상이 바빠지면서 책 한 권을 끝까지 읽을 시간을 확보하기 어려워졌습니다.
또한 수많은 도서 중에서 자신의 취향에 맞는 책을 고르는 것도 점점 어려운 일이 되었습니다.

이 문제를 해결하기 위해, 책의 줄거리를 **원하는 길이로 자동 요약**해주고 **키워드 기반으로 책을 추천**해주는 프로그램을 개발했습니다.

- AI Hub 도서 요약 데이터셋으로 KoT5 모델을 파인튜닝하여 요약 모델 3종 직접 학습
- 네이버 책 검색 API를 활용한 추천 시스템 구현
- PyQt5 기반 데스크탑 GUI 제공

---

## 🎯 주요 기능

| 기능 | 설명 |
|------|------|
| 키워드 요약 | 핵심 키워드만 추출 (KEYBERT 알고리즘) |
| 중간 요약 | 2~3줄 수준의 핵심 내용 요약 |
| 긴 요약 | 3줄 이상의 상세 요약 |
| 책 추천 | 검색어 입력 시 관련 도서 최대 50권 추천 (제목·저자·간략 설명 포함) |

---

## 🤖 모델 성능

KoT5 파인튜닝 모델 3종을 자동 평가 지표(ROUGE, BERTScore)로 평가했습니다.

### 키워드 요약 모델
| 지표 | 점수 |
|------|------|
| ROUGE-1 F1 | 0.2000 |

> 일부 핵심 단어 추출에는 성공하나, 정답 키워드와 표현 차이로 인해 단어 수준 일치율은 낮게 나타남

### 중간 요약 모델
| 지표 | 점수 |
|------|------|
| ROUGE-1 F1 | 0.3467 |
| ROUGE-2 F1 | 0.2000 |
| ROUGE-L F1 | 0.3467 |

> 핵심 정보는 충실히 요약되나 문장 연결성·표현 다양성은 향상 여지 있음

### 긴 요약 모델
| 지표 | 점수 |
|------|------|
| BERTScore Precision | 0.7066 |
| BERTScore Recall | 0.7420 |
| BERTScore F1 | 0.7238 |

> 의미적으로 약 72% 유사한 요약 생성 — 정답 의미를 잘 담아내는 수준으로 평가

---

## 🔧 기술 스택

| 분야 | 기술 |
|------|------|
| 프로그래밍 | Python 3.9+ |
| UI | PyQt5 |
| NLP 모델 | HuggingFace Transformers, KoT5 |
| 키워드 추출 | KEYBERT |
| 책 검색 | 네이버 책 검색 API |
| 데이터 | AI Hub 도서 요약 데이터셋 (JSONL 포맷) |

---

## 🤗 HuggingFace 모델

직접 학습한 모델 3종은 HuggingFace에 공개되어 있습니다.

- [JiinLee/kot5-keyword-summary](https://huggingface.co/JiinLee/kot5-keyword-summary)
- [JiinLee/kot5-mid-summary](https://huggingface.co/JiinLee/kot5-mid-summary)
- [JiinLee/kot5-long-summary](https://huggingface.co/JiinLee/kot5-long-summary)

`transformers` 라이브러리로 토큰 없이 바로 불러올 수 있습니다.

---

## ⚙️ 실행 방법

```bash
# 패키지 설치
pip install -r requirements.txt

# 실행
python src/main.py
```

---

## 📁 디렉토리 구조

```
teamproject/
├── README.md
├── requirements.txt
├── .gitignore
├── huggingface_links.md
│
├── src/
│   ├── main.py                       # GUI 실행 진입점
│   ├── summarize.py                  # 요약 모델 실행
│   ├── naver_books.py                # 네이버 API 책 검색
│   ├── p.py                          # PyQt 환경 설정
│   ├── preprocess/
│   │   ├── aihub_mid_preprocess.py   # 중간 요약 전처리
│   │   ├── keyword_preprocess.py     # 키워드 요약 전처리
│   │   └── long_preprocess.py        # 긴 요약 전처리
│   └── training/
│       ├── finetune_keyword.py       # 키워드 요약 파인튜닝
│       ├── finetune_mid.py           # 중간 요약 파인튜닝
│       └── finetune_long.py          # 긴 요약 파인튜닝
│
└── data/
    ├── preprocessed_data.jsonl
    ├── summary_keyword_train.jsonl
    ├── summary_keyword_val.jsonl
    └── ...
```

---

## 📄 문서

- 📘 [사용자 가이드](user_guide.md)
- 🛠️ [개발자 가이드](developer_guide.md)

---

## 👥 팀원
3인 팀 프로젝트
