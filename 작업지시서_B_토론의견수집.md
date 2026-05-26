# 작업지시서 B — 토론 의견 수집 앱

## 프로젝트 개요
- **앱 이름**: 토론 의견 수집
- **목적**: 학생들이 토론 활동 중 의견과 근거를 실시간으로 기록하고, 교사가 전체 학생 의견을 한눈에 조회
- **배포**: GitHub Pages (정적 사이트)
- **DB**: Supabase

---

## 기술 스택
- HTML / CSS / JavaScript (단일 index.html 파일)
- Supabase JS 클라이언트 v2 (CDN)
- config.js — Supabase URL, anon key 분리 관리 (.gitignore 포함)
- GitHub Pages 배포

---

## Supabase 설정

아래 정보를 입력하고 SQL을 생성해 주세요.

- **PROJECT_URL**: [여기에 Supabase Project URL 입력]
- **ANON_KEY**: [여기에 Supabase anon key 입력]

### DB 설정 지시
위 정보를 바탕으로 아래를 수행해 주세요.
- 테이블 생성 SQL 코드를 작성해 주세요 (테이블명: debate_records)
- RLS 설정 SQL 코드도 포함해 주세요 (insert/select: anon 모두 허용)
- 학생이 Supabase SQL Editor에 붙여넣기만 하면 바로 실행되도록 전체 SQL을 하나로 묶어 주세요

### 테이블 컬럼 구성
| 컬럼명 | 타입 | 설명 |
|--------|------|------|
| id | uuid | 기본키 (자동생성) |
| created_at | timestamp | 제출 시간 (자동생성) |
| topic | text | 토론 주제 |
| school_level | text | 학교급 (초등/중등/고등) |
| student_name | text | 학생 이름 |
| stance | text | 입장 (찬성/반대/중립) |
| reason | text | 이유 |
| evidence | text | 근거 |
| counter | text | 반대 의견에 대한 생각 |
| learned | text | 배운 점 |

---

## 화면 구성 (3개 화면, 단일 페이지 내 전환)

### 1. 설정 화면 (교사용)
- 토론 주제 입력
- 학교급 선택 (초등 / 중등 / 고등) — 선택에 따라 이후 화면 언어 변경
- 시작 버튼 → 학생 입력 화면으로 전환
- 전체 의견 조회 버튼 → 조회 화면으로 전환

### 2. 학생 입력 화면
공통 항목: 이름 입력

학교급별 입력 항목 및 언어:
| 항목 | 초등 | 중등 | 고등 |
|------|------|------|------|
| 입장 | 나는 어떻게 생각해요? | 나의 입장 | 주장 |
| 이유 | 왜 그렇게 생각했나요? | 그렇게 생각한 이유 | 주장의 근거 |
| 근거 | 어떤 예를 들 수 있나요? | 구체적인 근거나 예시 | 논거 및 자료 |
| 반대 의견 | 다른 생각도 있나요? | 반대 의견에 대한 생각 | 반론 및 재반박 |
| 배운 점 | 오늘 새로 알게 된 것 | 토론 후 생각이 바뀐 점 | 관점 변화 |

입장 선택: 찬성 / 반대 / 중립 (버튼)

### 3. 전체 조회 화면 (교사용)
- 전체 학생 의견 테이블 표시 (최신순)
- 입장별 필터 (찬성/반대/중립)
- 새로고침 버튼
- 제출 인원 수, 찬성/반대/중립 비율 통계

---

## 파일 구조
```
aiedu-dev01/
├── index.html
├── config.js
├── .gitignore
└── README.md
```

---

## 환경변수 처리 규칙
config.js 형식:
```javascript
const SUPABASE_URL = 'your-supabase-url';
const SUPABASE_ANON_KEY = 'your-anon-key';
```
- .gitignore에 config.js 반드시 포함

---

## 디자인 가이드
- 배경: 흰색 또는 연한 회색
- 포인트 컬러: 주황/노랑 계열 (토론 활기찬 느낌)
- 폰트: Noto Sans KR 우선
- 모바일 대응: 최대 너비 600px 중앙 정렬
- 입장별 색상: 찬성(초록) / 반대(빨강) / 중립(회색)

---

## 에러 핸들링 규칙
- Supabase 연결 실패 시 사용자 안내 메시지 표시
- 필수 항목 미입력 시 제출 버튼 비활성화
- 제출 중 로딩 상태 표시
- console.error로 에러 로깅 포함

---

## 개발 순서 (마일스톤)

### MVP
1. index.html 기본 구조
2. config.js 및 Supabase 연결
3. 설정 화면 구현
4. 학생 입력 화면 (중등 언어 기준)
5. Supabase insert 연동
6. 조회 화면 구현
7. GitHub Pages 배포 (레포명: aiedu-dev01)

### v0.2.0
- 학교급별 언어 전환
- 입장별 필터 및 통계
- 모바일 반응형 개선

### v1.0.0
- 디자인 완성
- 에러 핸들링 강화

---

## 주의사항
- config.js는 절대 GitHub에 push하지 않는다
- 단일 HTML 파일로 구현
- Supabase CDN: https://cdn.jsdelivr.net/npm/@supabase/supabase-js@2
- 한국어 주석 필수
- GitHub 레포명: aiedu-dev01
