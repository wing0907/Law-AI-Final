# LawAI Frontend

React + TypeScript + Vite 기반의 싱글 페이지 애플리케이션으로, LangGraph 백엔드와 연동하여 법률 질의/응답 경험을 제공합니다.

## Tech Stack
- React 19, TypeScript
- Vite 7 (ESBuild 기반 번들링)
- React Router DOM
- Font Awesome
- Fetch API / Axios (HTTP 클라이언트)
- ESLint + TypeScript ESLint

## Prerequisites
- Node.js 20 LTS 권장 (최소 18 이상)
- 백엔드 서버: 기본적으로 `http://localhost:8000` 에서 실행 중이라고 가정합니다. 개발 서버는 `/api` 경로를 해당 백엔드로 프록시합니다.

## Getting Started
```bash
cd Law_AI_Front
npm install
npm run dev
```

기본적으로 개발 서버는 `http://localhost:5173` 에서 열리며, `/api/*` 요청은 Vite 프록시 설정에 따라 FastAPI 백엔드로 전달됩니다.

## Available Scripts
- `npm run dev` – 개발 서버 실행 (HMR 지원)
- `npm run build` – 프로덕션 번들 생성
- `npm run preview` – 빌드 결과를 로컬에서 테스트

## Project Structure
```
Law_AI_Front/
├── src/
│   ├── api/askBackend.ts     # 백엔드 질의 유틸
│   ├── components/           # Logo, Topbar 등 UI 컴포넌트
│   ├── pages/                # Landing, Login, Signup 페이지
│   ├── hooks/                # 커스텀 훅
│   ├── styles.css, index.css # 전역 스타일
│   └── main.tsx              # 앱 엔트리
├── public/
├── package.json
└── vite.config.ts
```

## Integration Notes
- `src/api/askBackend.ts` 는 `fetch("/api/answer")` 로 백엔드와 통신합니다. 배포 환경에서는 프록시 대신 환경 변수를 사용해 API URL을 주입하는 방법을 고려하세요.
- 인증 토큰은 `localStorage` 의 `access_token` 키로 관리합니다. 로그아웃 시 토큰을 제거하고 `/login` 으로 리다이렉션합니다.
- 추가적인 정적 자산이나 글로벌 스타일은 `src/assets` 및 `src/styles.css` 에 정리되어 있습니다.
