# RecordNote

Google Meet 스타일의 회의·강의 녹화 & 실시간 STT 웹앱

---

## 주요 기능

- **화면 녹화 / 음성 녹음** 모드 전환
- **실시간 자막 (STT)** — 한국어 / 영어 전환 지원
- **AI 회의록 / 강의 요약** 자동 생성 (google/gemini-2.0-flash-exp:free)
- **오탈자·문법 교정** + diff 하이라이트 비교
- 전사본·요약본 **텍스트 다운로드**
- 토스 스타일 UI, 모바일/PC 완전 반응형

---

## 로컬 실행

### 방법 A — Vercel Dev (AI 기능 포함, 권장)

`.env.local`에 OpenRouter 키를 입력한 뒤 Vercel Dev 서버로 실행합니다.

```bash
# 1. .env.local 키 설정
# OPENROUTER_API_KEY=sk-or-...  ← openrouter.ai에서 무료 발급

# 2. Vercel Dev 서버 실행 (.env.local 자동 로드)
npx vercel dev
```

> `npx vercel dev`로 실행해야 `.env.local`의 환경변수가 `/api/claude` 서버리스 함수에 적용됩니다.

### 방법 B — 파일 직접 열기 (STT·녹화만)

```bash
open index.html     # macOS
start index.html    # Windows
```

> AI 정리/교정 버튼 클릭 시 OpenRouter API 키 입력 모달이 뜨며, 키를 입력하면 브라우저에서 직접 API를 호출합니다.  
> 키는 `localStorage`에만 저장되며 외부로 전송되지 않습니다.

---

## GitHub 업로드

```bash
git init
git add .
git commit -m "feat: RecordNote 초기 커밋"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPO.git
git push -u origin main
```

---

## Vercel 배포

1. [Vercel 대시보드](https://vercel.com/dashboard) 접속
2. **Add New → Project** 클릭
3. GitHub 저장소 선택 후 **Import**
4. **Settings → Environment Variables** 에서 아래 변수 추가:

   | Name | Value |
   |------|-------|
   | `OPENROUTER_API_KEY` | [openrouter.ai](https://openrouter.ai)에서 무료 발급한 키 |

5. **Deploy** 클릭 → 자동 빌드 & 배포 완료

이후 `main` 브랜치에 push할 때마다 자동으로 재배포됩니다.

---

## 환경변수

| 변수명 | 설명 |
|--------|------|
| `OPENROUTER_API_KEY` | [openrouter.ai](https://openrouter.ai)에서 무료 발급 |

로컬 개발 시 프로젝트 루트의 `.env.local` 파일에 설정합니다:

```
OPENROUTER_API_KEY=sk-or-...
```

> ⚠️ `.env.local` 및 `.env` 파일은 **절대 GitHub에 올리지 마세요.** `.gitignore`에 이미 포함되어 있습니다.

---

## 기술 스택

- **Frontend:** Vanilla JS + CSS (단일 `index.html`), Pretendard 폰트
- **Backend:** Vercel Serverless Function (`api/claude.js`)
- **AI:** OpenRouter API (`google/gemini-2.0-flash-exp:free` — 무료)
- **STT:** Web Speech API (브라우저 내장)
- **녹화:** MediaRecorder API, getDisplayMedia / getUserMedia
