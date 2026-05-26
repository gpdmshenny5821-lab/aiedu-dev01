# 토론 의견 수집 앱

초등·중등·고등 토론 활동에서 학생 의견을 실시간으로 기록하고 교사가 한눈에 조회할 수 있는 앱입니다.

## 빠른 시작

### 1. Supabase 테이블 만들기
Supabase 프로젝트 → SQL Editor → [아래 SQL 붙여넣기 후 실행]

```sql
-- debate_records 테이블 생성
CREATE TABLE IF NOT EXISTS debate_records (
  id           uuid      DEFAULT gen_random_uuid() PRIMARY KEY,
  created_at   timestamptz DEFAULT timezone('utc', now()) NOT NULL,
  topic        text NOT NULL,
  school_level text NOT NULL,
  student_name text NOT NULL,
  stance       text NOT NULL,
  reason       text,
  evidence     text,
  counter      text,
  learned      text
);

-- RLS 활성화
ALTER TABLE debate_records ENABLE ROW LEVEL SECURITY;

-- 익명 INSERT 허용
CREATE POLICY "anon_insert" ON debate_records
  FOR INSERT TO anon WITH CHECK (true);

-- 익명 SELECT 허용
CREATE POLICY "anon_select" ON debate_records
  FOR SELECT TO anon USING (true);
```

### 2. config.js 수정
```js
const SUPABASE_URL = 'https://xxxx.supabase.co';  // 본인 URL
const SUPABASE_ANON_KEY = 'eyJ...';               // 본인 anon key
```

### 3. GitHub Pages 배포
- 레포명: `aiedu-dev01`
- `config.js`는 `.gitignore`에 포함되어 있어 자동으로 제외됩니다.
- Settings → Pages → main 브랜치 루트(`/`) 선택

## 사용 방법

| 화면 | 대상 | 설명 |
|------|------|------|
| 설정 화면 | 교사 | 토론 주제 입력, 학교급 선택, 시작 |
| 학생 입력 | 학생 | 이름·입장·이유·근거·반론·배운점 제출 |
| 전체 조회 | 교사 | 실시간 의견 목록, 통계, 입장 필터 |

## 파일 구조
```
aiedu-dev01/
├── index.html   # 앱 전체 (단일 파일)
├── config.js    # Supabase 연결 정보 (gitignore됨)
├── .gitignore
└── README.md
```
