# LawAI Frontend

React + TypeScript + Vite로 구축된 법률 질의응답 웹 애플리케이션 프론트엔드입니다.

## 🛠 기술 스택

### 핵심 프레임워크
- **React** (v19.1.1) - UI 라이브러리
- **React DOM** (v19.1.1) - React DOM 렌더링
- **TypeScript** (v5.8.3) - 타입 안정성을 위한 정적 타입 언어

### 빌드 도구
- **Vite** (v7.1.7) - 빠른 개발 서버 및 빌드 도구
- **@vitejs/plugin-react** (v5.0.3) - React 플러그인

### 라우팅
- **React Router DOM** (v7.9.4) - 클라이언트 사이드 라우팅

### HTTP 클라이언트
- **Axios** (v1.12.2) - API 통신

### 아이콘
- **@fortawesome/fontawesome-svg-core** (v7.1.0) - FontAwesome 코어
- **@fortawesome/free-solid-svg-icons** (v7.1.0) - FontAwesome 솔리드 아이콘
- **@fortawesome/react-fontawesome** (v3.1.0) - React용 FontAwesome

### 개발 도구
- **ESLint** (v9.36.0) - 코드 린팅
- **TypeScript ESLint** (v8.44.0) - TypeScript 린팅 규칙
- **ESLint Plugin React Hooks** (v5.2.0) - React Hooks 린팅 규칙
- **ESLint Plugin React Refresh** (v0.4.20) - React Fast Refresh 지원

### 타입 정의
- **@types/react** (v19.2.2) - React 타입 정의
- **@types/react-dom** (v19.2.2) - React DOM 타입 정의

## 📁 프로젝트 구조

```
Law_AI_Front/
├── public/
│   └── vite.svg
├── src/
│   ├── api/
│   │   └── askBackend.ts      # 백엔드 API 호출 함수
│   ├── assets/
│   │   └── react.svg
│   ├── components/
│   │   ├── Logo.tsx           # 로고 컴포넌트
│   │   ├── PatternLayer.tsx   # 배경 패턴 레이어
│   │   ├── SearchDrawer.tsx   # 검색 드로어 컴포넌트
│   │   └── Topbar.tsx         # 상단 바 컴포넌트
│   ├── hooks/
│   │   └── useLogo.ts         # 로고 애니메이션 커스텀 훅
│   ├── pages/
│   │   ├── Landing.tsx        # 메인 랜딩 페이지 (질의응답)
│   │   ├── Login.tsx          # 로그인 페이지
│   │   └── Signup.tsx         # 회원가입 페이지
│   ├── App.tsx                # 라우터 설정 및 앱 진입점
│   ├── main.tsx               # React 앱 마운트
│   ├── types.ts               # TypeScript 타입 정의
│   ├── index.css              # 전역 스타일
│   └── styles.css             # 추가 스타일
├── index.html                 # HTML 진입점
├── package.json
├── tsconfig.json              # TypeScript 설정
├── tsconfig.app.json          # 앱용 TypeScript 설정
├── tsconfig.node.json         # Node.js용 TypeScript 설정
├── vite.config.ts             # Vite 설정
└── eslint.config.js           # ESLint 설정
```

## 🚀 설치 및 실행

### 1. 의존성 설치

```bash
npm install
```

### 2. 개발 서버 실행

```bash
npm run dev
```

개발 서버는 `http://localhost:5173`에서 실행됩니다.

### 3. 프로덕션 빌드

```bash
npm run build
```

빌드된 파일은 `dist/` 디렉토리에 생성됩니다.

### 4. 프로덕션 미리보기

```bash
npm run preview
```

## 🔐 인증 흐름

- **로그인/회원가입**: `/login`, `/signup` 페이지에서 인증
- **토큰 저장**: JWT 토큰을 `localStorage`의 `access_token`에 저장
- **보호된 라우트**: `/landing` 페이지는 인증이 필요하며, 미인증 시 `/login`으로 리다이렉트

## 📡 API 통신

백엔드 API는 `src/api/askBackend.ts`에서 관리됩니다.
- 기본 URL: `http://localhost:8000`
- 인증 토큰은 요청 헤더에 포함됩니다.

## 🎨 주요 기능

- 사용자 인증 (회원가입/로그인)
- 법률 질의응답 인터페이스
- 반응형 디자인
- 로고 애니메이션
- 검색 드로어 UI

## 🔧 개발 설정

### TypeScript 설정
- 엄격한 타입 체크 활성화
- React JSX 지원
- ES2020 타겟

### ESLint 설정
- React Hooks 규칙 활성화
- TypeScript 규칙 적용
- React Refresh 지원
