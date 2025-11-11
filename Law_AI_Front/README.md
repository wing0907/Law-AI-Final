# 🎨 LawAI Frontend

React 19와 TypeScript로 구축된 현대적인 AI 법률 자문 서비스 프론트엔드입니다. 직관적인 UI/UX로 사용자가 쉽게 법률 질문을 하고 답변을 받을 수 있습니다.

## 🛠️ 기술 스택

### 핵심 프레임워크
- **React 19.1.1** - 최신 React UI 라이브러리
- **TypeScript 5.8.3** - 타입 안정성 및 개발자 경험 향상
- **Vite 7.1.7** - 차세대 빠른 빌드 도구

### 라우팅 & 상태관리
- **React Router DOM 7.9.4** - 클라이언트 사이드 라우팅
- **LocalStorage** - 인증 토큰 관리

### HTTP 통신
- **Axios 1.12.2** - HTTP 클라이언트

### UI 라이브러리
- **FontAwesome 7.1.0** - 아이콘 라이브러리
  - `@fortawesome/fontawesome-svg-core`
  - `@fortawesome/free-solid-svg-icons`
  - `@fortawesome/react-fontawesome`

### 개발 도구
- **ESLint 9.36.0** - 코드 품질 검사
- **TypeScript ESLint 8.44.0** - TypeScript 린팅
- **Vite Plugin React 5.0.3** - React Fast Refresh

## 📁 프로젝트 구조

```
Law_AI_Front/
├── src/
│   ├── api/
│   │   └── askBackend.ts      # 백엔드 API 통신 함수
│   │
│   ├── components/
│   │   ├── Logo.tsx           # 로고 컴포넌트
│   │   ├── PatternLayer.tsx   # 배경 패턴
│   │   ├── SearchDrawer.tsx   # 검색 드로어 (법률 질문)
│   │   └── Topbar.tsx         # 상단 네비게이션 바
│   │
│   ├── pages/
│   │   ├── Landing.tsx        # 메인 페이지 (법률 질문)
│   │   ├── Login.tsx          # 로그인 페이지
│   │   └── Signup.tsx         # 회원가입 페이지
│   │
│   ├── hooks/
│   │   └── useLogo.ts         # 로고 애니메이션 훅
│   │
│   ├── assets/                # 이미지 및 정적 자원
│   ├── App.tsx                # 메인 앱 컴포넌트 (라우터)
│   ├── main.tsx               # 앱 엔트리포인트
│   ├── index.css              # 전역 스타일
│   ├── styles.css             # 커스텀 스타일
│   └── types.ts               # TypeScript 타입 정의
│
├── public/                     # 정적 파일
├── index.html                 # HTML 템플릿
├── package.json               # 의존성 관리
├── vite.config.ts             # Vite 설정
├── tsconfig.json              # TypeScript 설정
├── tsconfig.app.json          # 앱용 TS 설정
├── tsconfig.node.json         # Node용 TS 설정
├── eslint.config.js           # ESLint 설정
└── README.md                  # 이 파일
```

## 🚀 시작하기

### 1. 사전 요구사항

- **Node.js 16 이상** (권장: 18 이상)
- **npm** 또는 **yarn**
- **백엔드 서버** 실행 중 (`http://localhost:8000`)

### 2. 의존성 설치

```bash
cd Law_AI_Front
npm install
```

또는 yarn 사용:
```bash
yarn install
```

### 3. 개발 서버 실행

```bash
npm run dev
```

브라우저가 자동으로 열리며, 다음 주소에서 접근할 수 있습니다:
- http://localhost:5173

### 4. 프로덕션 빌드

```bash
# TypeScript 컴파일 및 Vite 빌드
npm run build

# 빌드 결과 미리보기
npm run preview
```

빌드된 파일은 `dist/` 폴더에 생성됩니다.

## 🎯 주요 기능

### 1. 인증 시스템
- **회원가입**: 이메일, 사용자명, 비밀번호로 계정 생성
- **로그인**: JWT 토큰 기반 인증
- **보호된 라우트**: 로그인하지 않은 사용자는 자동으로 로그인 페이지로 이동
- **토큰 관리**: LocalStorage에 `access_token` 저장

### 2. 법률 질문 인터페이스
- **검색 드로어**: 사용자 친화적인 질문 입력 UI
- **실시간 답변**: 백엔드 RAG 파이프라인을 통한 즉각적인 답변
- **출처 표시**: 답변과 함께 관련 법률 문서 출처 제공

### 3. 반응형 디자인
- 모바일, 태블릿, 데스크톱 모든 기기에서 최적화된 UI
- 현대적이고 깔끔한 디자인

## 🔐 인증 흐름

```typescript
// 로그인 상태 확인
const isAuthenticated = () => !!localStorage.getItem('access_token');

// 보호된 라우트
<Route
  path="/landing"
  element={
    <ProtectedRoute>
      <Landing />
    </ProtectedRoute>
  }
/>
```

### 로그인 프로세스
1. 사용자가 로그인 폼 제출
2. 백엔드 API로 인증 요청
3. JWT 토큰 수신
4. LocalStorage에 토큰 저장
5. 메인 페이지(`/landing`)로 리다이렉트

### 로그아웃
```typescript
localStorage.removeItem('access_token');
// 로그인 페이지로 이동
```

## 📡 API 통신

### askBackend.ts

백엔드 API와의 통신을 담당하는 모듈입니다.

```typescript
import axios from 'axios';

const API_BASE_URL = 'http://localhost:8000/api';

// 법률 질문 답변 요청
export const askQuestion = async (query: string) => {
  const token = localStorage.getItem('access_token');
  
  const response = await axios.post(
    `${API_BASE_URL}/answer`,
    { query },
    {
      headers: {
        'Authorization': `Bearer ${token}`,
        'Content-Type': 'application/json'
      }
    }
  );
  
  return response.data;
};
```

## 🎨 스타일링

### CSS 구조
- `index.css`: 전역 스타일, 리셋, 폰트
- `styles.css`: 컴포넌트별 커스텀 스타일

### 디자인 원칙
- **일관성**: 통일된 색상 팔레트 및 타이포그래피
- **접근성**: 명확한 대비와 읽기 쉬운 폰트 크기
- **반응형**: 모든 화면 크기에서 최적화된 레이아웃

## 🧩 주요 컴포넌트

### Logo.tsx
- 애니메이션 로고 컴포넌트
- 커스텀 훅(`useLogo`) 사용

### SearchDrawer.tsx
- 법률 질문 입력 인터페이스
- 답변 및 출처 표시
- 로딩 상태 관리

### Topbar.tsx
- 상단 네비게이션 바
- 로그아웃 버튼
- 사용자 정보 표시

### PatternLayer.tsx
- 배경 장식 요소
- 시각적 매력 향상

## 📱 라우팅 구조

```
/ (root)
├─ → /login (리다이렉트)
│
├─ /login          # 로그인 페이지
├─ /signup         # 회원가입 페이지
│
└─ /landing        # 메인 페이지 (보호됨)
   └─ 법률 질문 인터페이스
```

## 🔧 환경 설정

### Vite 설정 (`vite.config.ts`)
- React 플러그인 설정
- 빌드 최적화
- 개발 서버 설정

### TypeScript 설정
- `tsconfig.json`: 전역 TypeScript 설정
- `tsconfig.app.json`: 앱 코드용 설정
- `tsconfig.node.json`: Vite 설정 파일용

### ESLint 설정
- React Hooks 린팅
- React Refresh 린팅
- TypeScript 타입 체크

## 🐛 개발 팁

### 백엔드 연결 확인
백엔드가 `http://localhost:8000`에서 실행 중인지 확인하세요.

### CORS 에러 해결
백엔드의 CORS 설정에 프론트엔드 URL이 포함되어 있는지 확인:
```python
# backend/app/main.py
origins = [
    "http://localhost:5173",
    "http://127.0.0.1:5173",
]
```

### 토큰 만료 처리
API 요청 시 401 에러가 발생하면 토큰이 만료된 것입니다. 로그아웃 후 다시 로그인하세요.

### Hot Module Replacement (HMR)
Vite의 HMR로 코드 변경 시 자동으로 브라우저가 업데이트됩니다.

## 📦 빌드 및 배포

### 프로덕션 빌드
```bash
npm run build
```

### 빌드 결과
- `dist/` 폴더에 정적 파일 생성
- 최적화된 JavaScript, CSS
- 트리 쉐이킹으로 불필요한 코드 제거

### 배포
생성된 `dist/` 폴더를 다음 플랫폼에 배포할 수 있습니다:
- Vercel
- Netlify
- GitHub Pages
- AWS S3 + CloudFront
- Firebase Hosting

### 환경 변수 (프로덕션)
프로덕션 환경에서는 백엔드 API URL을 환경 변수로 관리하세요:

```typescript
const API_BASE_URL = import.meta.env.VITE_API_URL || 'http://localhost:8000/api';
```

`.env.production`:
```
VITE_API_URL=https://your-backend-api.com/api
```

## 🔗 관련 링크

- [React 공식 문서](https://react.dev/)
- [TypeScript 공식 문서](https://www.typescriptlang.org/)
- [Vite 공식 문서](https://vitejs.dev/)
- [React Router 공식 문서](https://reactrouter.com/)
- [Axios 문서](https://axios-http.com/)

## ⚠️ 주의사항

- LocalStorage에 저장된 토큰은 XSS 공격에 취약할 수 있습니다
- 프로덕션 환경에서는 HTTPS를 사용하세요
- 민감한 정보는 절대 클라이언트 사이드에 저장하지 마세요
- API_BASE_URL은 환경에 따라 변경하세요

## 🚧 향후 개선사항

- [ ] 토큰 자동 갱신 기능
- [ ] 질문 히스토리 저장
- [ ] 다크 모드 지원
- [ ] 소셜 로그인 (Google, Kakao 등)
- [ ] PWA (Progressive Web App) 지원
- [ ] 실시간 알림 기능

---

**개발 문의 및 버그 리포트는 이슈로 등록해주세요.**
