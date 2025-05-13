# LawAI Frontend

React와 TypeScript를 기반으로 한 법률 AI 챗봇 프론트엔드 애플리케이션입니다. Vite를 사용한 빠른 개발 환경과 현대적인 UI/UX를 제공합니다.

## 🛠️ 기술 스택

### 핵심 프레임워크
- **React 19.1.1** - 사용자 인터페이스 구축을 위한 라이브러리
- **TypeScript 5.8.3** - 타입 안정성을 위한 정적 타입 언어
- **Vite 7.1.7** - 빠른 개발 서버 및 빌드 도구

### 라우팅
- **React Router DOM 7.9.4** - 클라이언트 사이드 라우팅
  - `/login` - 로그인 페이지
  - `/signup` - 회원가입 페이지
  - `/landing` - 메인 대시보드 (법률 상담)

### HTTP 클라이언트
- **Axios 1.12.2** - RESTful API 통신

### UI/UX
- **FontAwesome 7.1.0** - 아이콘 라이브러리
  - `@fortawesome/fontawesome-svg-core`
  - `@fortawesome/free-solid-svg-icons`
  - `@fortawesome/react-fontawesome`

### 개발 도구
- **ESLint 9.36.0** - 코드 품질 및 스타일 검사
- **TypeScript ESLint 8.44.0** - TypeScript 전용 린팅 규칙
- **ESLint React Hooks Plugin** - React Hooks 규칙 검사
- **ESLint React Refresh Plugin** - Fast Refresh 지원

## 📁 프로젝트 구조

```
Front/
├── public/
│   └── vite.svg              # 공개 정적 파일
│
├── src/
│   ├── api/
│   │   └── askBackend.ts     # 백엔드 API 클라이언트
│   │
│   ├── assets/
│   │   └── react.svg         # 이미지 리소스
│   │
│   ├── components/
│   │   ├── Logo.tsx          # 로고 컴포넌트
│   │   ├── PatternLayer.tsx  # 배경 패턴 레이어
│   │   ├── SearchDrawer.tsx  # 검색 드로어 컴포넌트
│   │   └── Topbar.tsx        # 상단 바 컴포넌트
│   │
│   ├── hooks/
│   │   └── useLogo.ts        # 로고 애니메이션 커스텀 훅
│   │
│   ├── pages/
│   │   ├── Landing.tsx       # 메인 대시보드 페이지
│   │   ├── Login.tsx         # 로그인 페이지
│   │   └── Signup.tsx        # 회원가입 페이지
│   │
│   ├── App.tsx               # 메인 앱 컴포넌트 (라우팅)
│   ├── main.tsx              # 앱 진입점
│   ├── types.ts              # TypeScript 타입 정의
│   ├── index.css             # 전역 스타일
│   └── styles.css            # 추가 스타일
│
├── index.html                # HTML 템플릿
├── vite.config.ts            # Vite 설정
├── tsconfig.json             # TypeScript 설정
├── tsconfig.app.json         # 앱용 TypeScript 설정
├── tsconfig.node.json        # Node.js용 TypeScript 설정
├── eslint.config.js          # ESLint 설정
└── package.json              # 프로젝트 의존성 및 스크립트
```

## 🚀 설치 및 실행

### 1. 사전 요구사항

- Node.js 18 이상
- npm 또는 yarn 패키지 매니저

### 2. 의존성 설치

```bash
npm install
```

### 3. 개발 서버 실행

```bash
npm run dev
```

개발 서버가 실행되면 브라우저가 자동으로 열리고 다음 주소에서 확인할 수 있습니다:
- http://localhost:5173

### 4. 프로덕션 빌드

```bash
npm run build
```

빌드된 파일은 `dist/` 디렉토리에 생성됩니다.

### 5. 프로덕션 미리보기

```bash
npm run preview
```

## ⚙️ 설정

### Vite 설정 (`vite.config.ts`)

```typescript
export default defineConfig({
  plugins: [react()],
  server: {
    port: 5173,
    open: true,
    host: true,
    proxy: {
      '/api': {
        target: 'http://localhost:8000',
        changeOrigin: true,
      }
    }
  }
})
```

- **포트**: 5173 (기본값)
- **프록시**: `/api` 요청을 백엔드 서버(`http://localhost:8000`)로 전달

### API 설정

`src/api/askBackend.ts`에서 백엔드 API 엔드포인트를 관리합니다:

```typescript
const API_BASE_URL = '/api';  // Vite 프록시를 통해 백엔드로 전달
```

## 🎨 주요 컴포넌트

### 페이지 컴포넌트

#### Login.tsx
- 사용자 로그인 폼
- 이메일/비밀번호 입력
- JWT 토큰 저장 (localStorage)

#### Signup.tsx
- 회원가입 폼
- 이메일/비밀번호 입력 및 검증

#### Landing.tsx
- 메인 대시보드
- 법률 질문 입력 및 답변 표시
- 검색 결과 표시

### 공통 컴포넌트

#### Topbar.tsx
- 상단 네비게이션 바
- 로고 및 사용자 메뉴

#### SearchDrawer.tsx
- 검색 드로어 컴포넌트
- 질문 입력 및 답변 표시

#### Logo.tsx
- 애니메이션 로고 컴포넌트

#### PatternLayer.tsx
- 배경 패턴 레이어

## 🔌 API 통신

### 백엔드 API 호출

`src/api/askBackend.ts`에서 백엔드와 통신:

```typescript
export async function askBackend(
  query: string, 
  noLLM = false
): Promise<BackendResponse> {
  const response = await axios.post(`${API_BASE_URL}/answer`, {
    query,
    no_llm: noLLM
  });
  return response.data;
}
```

### 인증 API

로그인 및 회원가입은 `axios`를 직접 사용하여 호출:

```typescript
// 로그인
axios.post('/api/auth/login', { email, password })

// 회원가입
axios.post('/api/auth/register', { email, password })
```

## 🛣️ 라우팅 구조

### 경로 정의

- `/` → `/login`으로 리다이렉트
- `/login` - 로그인 페이지
- `/signup` - 회원가입 페이지
- `/landing` - 메인 대시보드 (보호된 라우트)
- `*` - 정의되지 않은 경로는 `/landing`으로 리다이렉트

### 보호된 라우트

현재 `ProtectedRoute` 컴포넌트는 모든 사용자를 허용합니다. 향후 JWT 토큰 검증 로직을 추가할 수 있습니다.

## 🎯 주요 기능

### 사용자 인증
- 회원가입
- 로그인
- JWT 토큰 기반 인증 (localStorage 저장)

### 법률 상담
- 실시간 질문 입력
- RAG 기반 답변 생성
- 검색된 법률 문서 표시
- 답변 및 출처 정보 표시

## 🐛 문제 해결

### 백엔드 연결 오류
- 백엔드 서버가 `http://localhost:8000`에서 실행 중인지 확인
- `vite.config.ts`의 프록시 설정이 올바른지 확인

### CORS 오류
- 백엔드의 CORS 설정에서 프론트엔드 주소(`http://localhost:5173`)가 허용되어 있는지 확인

### 포트 충돌
- 포트 5173이 사용 중인 경우, `vite.config.ts`에서 다른 포트로 변경

## 📚 참고 자료

- [React 공식 문서](https://react.dev/)
- [TypeScript 공식 문서](https://www.typescriptlang.org/)
- [Vite 공식 문서](https://vitejs.dev/)
- [React Router 공식 문서](https://reactrouter.com/)
- [Axios 공식 문서](https://axios-http.com/)

## 🔧 개발 팁

### Hot Module Replacement (HMR)
Vite는 기본적으로 HMR을 지원하므로 코드 변경 시 자동으로 브라우저가 업데이트됩니다.

### 타입 안정성
TypeScript를 사용하여 타입 안정성을 보장합니다. 타입 오류가 발생하면 빌드가 실패합니다.

### 코드 품질
ESLint를 사용하여 코드 품질을 유지합니다. IDE에서 실시간으로 린팅 오류를 확인할 수 있습니다.
