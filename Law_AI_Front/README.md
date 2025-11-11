# LawAI Frontend

LawAI 프론트엔드는 React와 TypeScript를 기반으로 하며 백엔드의 법률 질의응답 API와 연동되는 사용자 인터페이스를 제공합니다.

## Tech Stack
- **Framework:** React 19, React Router DOM
- **Language & Tooling:** TypeScript, Vite
- **HTTP Client:** Axios
- **UI & Icons:** Font Awesome, CSS Modules 스타일 구조
- **Linting & Formatting:** ESLint (typescript-eslint)

## Prerequisites
- Node.js 20 이상
- npm 10 이상 (또는 호환되는 패키지 매니저)

## Setup
```bash
cd Law_AI_Front
npm install
```

## Run
```bash
npm run dev
```

- 개발 서버: `http://127.0.0.1:5173`
- 백엔드 연동 주소는 `src/api/askBackend.ts`에서 확인할 수 있습니다.

## Project Structure
- `src/pages/` – 로그인, 회원가입, 랜딩 페이지 등 라우팅 페이지
- `src/components/` – 재사용 가능한 UI 컴포넌트 모음
- `src/api/askBackend.ts` – 백엔드와 통신하는 API 래퍼
- `src/hooks/` – 커스텀 훅 모음
- `src/main.tsx` – React 앱 엔트리포인트
