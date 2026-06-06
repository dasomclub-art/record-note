# RecordNote

Google Meet 스타일의 회의·강의 녹화 & 실시간 STT 웹앱

---

## 주요 기능

- **화면 녹화 / 음성 녹음** 모드 전환
- **실시간 자막 (STT)** — 한국어 / 영어 전환 지원
- **AI 회의록 / 강의 요약** 자동 생성
- **오탈자·문법 교정** + diff 하이라이트 비교
- 전사본·요약본 **텍스트 다운로드**
- 토스 스타일 UI, 모바일/PC 완전 반응형

---

## 로컬 실행

`index.html`을 브라우저에서 바로 열 수 있습니다.

```bash
# 별도 설치 없이 브라우저로 열기
open index.html     # macOS
start index.html    # Windows
```

> **주의:** AI 정리/교정 기능은 `/api/claude` 서버리스 함수가 필요하므로 **Vercel 배포 환경에서만 동작합니다.**  
> 로컬에서 화면 녹화·STT는 정상 동작합니다.

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
   | `ANTHROPIC_API_KEY` | Anthropic Console에서 발급받은 키 |

5. **Deploy** 클릭 → 자동 빌드 & 배포 완료

이후 `main` 브랜치에 push할 때마다 자동으로 재배포됩니다.

---

## 환경변수

| 변수명 | 설명 |
|--------|------|
| `ANTHROPIC_API_KEY` | [Anthropic Console](https://console.anthropic.com)에서 발급 |

> ⚠️ `.env` 파일은 **절대 GitHub에 올리지 마세요.** `.gitignore`에 이미 포함되어 있습니다.

---

## 기술 스택

- **Frontend:** Vanilla JS + CSS (단일 `index.html`), Pretendard 폰트
- **Backend:** Vercel Serverless Function (`api/claude.js`)
- **AI:** Anthropic Claude API (`claude-sonnet-4-20250514`)
- **STT:** Web Speech API (브라우저 내장)
- **녹화:** MediaRecorder API, getDisplayMedia / getUserMedia
