# AI 동화 다시쓰기 연구소 2.0

중학생을 위한 성 고정관념 분석 및 생성형 AI 활용 수업 웹사이트입니다.

## 주요 기능
- AI 윤리 안내 및 이용 약속
- 신데렐라, 백설공주, 잠자는 숲속의 공주, 인어공주 교육용 원작 요약
- 존중 감수성 다섯 질문별 판단·근거·해석 기록
- 학생의 개선 방향 및 프롬프트 작성
- Netlify Function을 통한 Gemini AI 동화 초안 생성 (API 키는 서버 환경변수로 보관)
- AI 결과 비판적 검토, 최종 수정, 성찰
- 총 100점 4수준 수행평가 루브릭 (미수행 0점)
- 브라우저 로컬 임시 저장, 텍스트 파일 다운로드

## GitHub → Netlify 배포
1. GitHub에서 **새 저장소**를 만들고 이 폴더의 파일을 업로드합니다. `index.html`, `app.js`, `styles.css`, `netlify.toml`, `netlify/functions/generate.mjs`의 구조를 유지하세요.
2. Netlify → **Add new project** → **Import an existing project** → **GitHub** → 저장소를 선택합니다.
3. 배포 설정: **Build command 비움**, **Publish directory `.`** (Netlify는 `netlify.toml`의 설정도 읽습니다).
4. Netlify → **Project configuration → Environment variables**에서 `GEMINI_API_KEY`를 등록합니다. 키는 GitHub 파일이나 브라우저 코드에 절대 넣지 마세요.
5. 새 환경변수를 등록했다면 **다시 배포**하세요. `GEMINI_MODEL`을 설정하지 않으면 `gemini-2.5-flash`가 사용됩니다. 모델 사용 가능 여부는 계정에 따라 다를 수 있습니다.
6. 배포 URL에서 AI 요청을 테스트합니다. Netlify 무료 사용량 및 Gemini API 할당량에 유의하세요.

## 로컬 개발
- `npm install` 후 `npx netlify dev` 실행 (Netlify CLI 필요)
- 로컬에서 AI 호출 테스트 시 Netlify 환경변수 또는 로컬 `.env` 파일에 `GEMINI_API_KEY`를 설정합니다. `.env`는 Git에 올리지 않습니다.
- `index.html`을 파일로 직접 열면 화면은 보이지만 AI 함수는 동작하지 않습니다.

## 개인정보 및 교육적 유의점
- 기본 구현에는 **학생별 계정, 교사용 조회, 서버 기록, 자동 제출, 자동 채점이 없습니다**.
- 입력한 활동 내용은 해당 브라우저의 `localStorage`에 남습니다. 공용 PC에서는 활동 종료 후 삭제하거나 브라우저 데이터를 정리하도록 지도하세요.
- **AI 생성 요청**에 포함된 선택 동화·요약·개선 방향·프롬프트는 Gemini API에 전송됩니다. AI 요청문에 실명이나 민감한 개인정보를 입력하지 않도록 지도하세요.
- 교사의 API 키를 사용한다고 해서 교사가 학생의 입력 전체를 자동으로 열람할 수 있는 것은 아닙니다. 사용량과 비용은 키 소유자의 계정에 귀속될 수 있습니다.
- 실제 수업에 적용하기 전에 학교의 개인정보 처리 기준, AI 서비스 이용 연령 요건, 학부모 동의 등 관련 정책을 확인하세요.
- 루브릭은 예시이며 교사가 교육과정과 평가계획에 맞춰 수정·확정해야 합니다.
- 동화는 원문 전체가 아니라 판본을 명시한 **교육용 요약**입니다. 판본마다 장면과 결말이 달라질 수 있습니다.

## 파일
- `index.html`: 화면 구성
- `styles.css`: 반응형 디자인
- `app.js`: 단계별 활동, 루브릭, 로컬 저장 및 제출 파일 생성
- `netlify/functions/generate.mjs`: 서버에서 Gemini API 호출
- `netlify.toml`: Netlify 설정
