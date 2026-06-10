# 관광·호스피탈리티 경영 학술 논문 작성 스킬

[English](README.md) | [简体中文](README.zh-CN.md) | [日本語](README.ja.md) | [한국어](README.ko.md)

OpenCode / Claude Code / Codex 등 AI 코딩 에이전트를 위한 관광·호스피탈리티 경영 학술 논문 작성 스킬입니다. 주제 선정부터 이론적 프레임워크, 연구 설계, 데이터 분석, 완전한 초고까지 전 과정을 다룹니다.

관광·호스피탈리티 분야 주요 6개 저널을 지원합니다: **Tourism Management, Annals of Tourism Research, JTR, IJHM, IJCHM, JST**.

## 기능

AI 에이전트가 관광·호스피탈리티 논문의 **0→초고 5단계 파이프라인**을 수행하도록 안내합니다:

| 단계 | 산출물 | 주요 결과물 |
|------|--------|-----------|
| **1단계**: 주제 선정 | Gap table, 저널 추천, 기여陈述 | 어느 저널 + 무엇이 새로운가 |
| **2단계**: 이론적 프레임워크 | 개념 모델, 가설 도출, 문헌 통합 | §2 문헌·프레임워크 초고 |
| **3단계**: 연구 설계 | 방법론 설계도(양적/질적/혼합), 측정 척도, 표본 계획 | §3 방법론 초고 |
| **4단계**: 데이터 분석 | 양적(SEM, 회귀, 관광 수요) 또는 질적(근거이론, 민족지학, 주제 분석) 결과 | §4-5 분석 결과 초고 |
| **5단계**: 집필 및 조립 | Introduction, 논의, 이론적·실무적 시사점, Abstract | 완전한 초고 |

**도메인 특화**: 일반 작성 스킬이 다루지 않는 관광·호스피탈리티 저널 고유의 관행(개념 모델 제시 구조, 척도 개발 기준, 질적 연구 신뢰성 기준, 혼합 연구법 통합 프레임워크, 심사자 기대치 등)을 내장하고 있습니다.

---

## 설치

### 1. 저장소 클론

```bash
git clone https://github.com/liyuanbo1024/tourism-management-writing.git
```

### 2. AI 에이전트에 설치

| 에이전트 | 설치 명령어 |
|---------|-----------|
| **OpenCode** | `cp -r tourism-management-writing ~/.config/opencode/skills/` |
| **Claude Code** | `cp -r tourism-management-writing ~/.claude/skills/` |
| **Codex** | `cp -r tourism-management-writing ~/.agents/skills/` |
| **Cursor** | `cp -r tourism-management-writing ~/.cursor/skills/` |
| **Windsurf** | `cp -r tourism-management-writing ~/.windsurf/skills/` |

설치 후 자연어로 스킬을 호출할 수 있습니다:
- `소셜 미디어가 관광 행동에 미치는 영향에 관한 논문을 쓰고 싶습니다. 포지셔닝을 도와주세요`
- `개념 모델과 가설이 완성되었습니다. 측정 척도를 설계해 주세요`
- `관광 경영 논문 작성 파이프라인 전체를 실행해 주세요`

---

## 사용법

### 파이프라인 모드

```
"관광 경영 논문 작성 파이프라인을 실행해 주세요. 제 주제는…"
```

에이전트가 현재 단계를 평가하고 1단계부터 5단계까지 순차적으로 실행하며, 각 단계마다 확인을 요청합니다.

### 단계 건너뛰기

| 트리거 문구 | 이동 단계 |
|-----------|---------|
| "연구 아이디어가 있습니다…" | 1단계: 주제 선정 |
| "이론적 프레임워크를 구축해 주세요" | 2단계: 이론적 프레임워크 |
| "연구 방법을 설계해 주세요" | 3단계: 연구 설계 |
| "설문/인터뷰 데이터를 분석해 주세요" | 4단계: 데이터 분석 |
| "완전한 논문을 작성해 주세요" | 5단계: 집필 및 조립 |

### 참조 모드

```
"Tourism Management의 질적 연구 엄격성 기준은 무엇인가요?"
"JTR의 가설 도출은 어떻게 구성해야 하나요?"
```

---

## 지원 저널

| 저널 | 핵심 정체성 |
|------|----------|
| Tourism Management (TM) | 광범위한 관광 연구, 높은 엄격성, 정책·실무 연계 |
| Annals of Tourism Research (ATR) | 이론적 깊이, 사회학·인류학적 관점 |
| Journal of Travel Research (JTR) | 양적 연구 중심, 소비자 행동, 목적지 마케팅 |
| Int. J. Hospitality Management (IJHM) | 호스피탈리티 운영, 인적자원관리, 서비스 경영 |
| Int. J. Contemporary Hospitality Mgmt (IJCHM) | 현대적 이슈, 혁신, 전략적 호스피탈리티 |
| Journal of Sustainable Tourism (JST) | 지속가능성, 윤리, 커뮤니티 영향, 환경 |

### 저널별 방법론 선호도

| 방법 | TM | ATR | JTR | IJHM | IJCHM | JST |
|------|-----|------|------|------|-------|-----|
| 양적(SEM, 회귀) | ✓✓✓ | ✓ | ✓✓✓ | ✓✓✓ | ✓✓✓ | ✓✓ |
| 질적(근거이론, 민족지학) | ✓✓ | ✓✓✓ | ✓ | ✓✓ | ✓✓ | ✓✓✓ |
| 혼합 연구법 | ✓✓ | ✓✓ | ✓✓ | ✓✓ | ✓✓✓ | ✓✓✓ |
| 척도 개발 | ✓✓✓ | ✓ | ✓✓✓ | ✓✓✓ | ✓✓✓ | ✓✓ |
| 관광 수요 모델링 | ✓✓✓ | ✓ | ✓✓✓ | ✓ | — | — |
| 체계적 문헌고찰/메타분석 | ✓✓ | ✓✓✓ | ✓✓ | ✓✓ | ✓✓✓ | ✓✓ |

---

## 파일 구조

```
tourism-management-writing/
├── SKILL.md                              메인 스킬 파일
├── references/                           8개 참조 파일
├── assets/                               개념 모델 예시
├── examples/                             LaTeX 템플릿 + R + Python
├── README.md / README.zh-CN.md / .ja.md / .ko.md
└── LICENSE
```

---

## 라이선스

MIT License — [LICENSE](LICENSE) 참조.

---

## 감사의 글

[agentskills.io](https://agentskills.io) 명세와 [OpenCode](https://github.com/anomalyco/opencode)의 스킬 작성 방법론을 기반으로 합니다. 관광·호스피탈리티 도메인 지식은 Elsevier 저널(Tourism Management, ATR, IJHM, IJCHM), Sage(JTR), Taylor & Francis(JST)의 편집 성명에 의존합니다.
