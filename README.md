# 🏛️ LawAI - AI 법률 자문 서비스

LawAI는 **RAG(Retrieval-Augmented Generation)** 기술을 활용하여 법률 관련 질문에 정확한 답변을 제공하는 AI 기반 법률 자문 서비스입니다.

## 📋 프로젝트 개요

LawAI는 사용자의 법률 질문을 분석하고, 벡터 데이터베이스에서 관련 법률 문서를 검색한 후, Google Gemini AI를 활용하여 명확하고 이해하기 쉬운 답변을 생성합니다.

### 주요 기능

- 🤖 **AI 기반 법률 자문**: Google Gemini 2.5 Pro를 활용한 고품질 답변 생성
- 📚 **RAG 시스템**: ChromaDB 기반 벡터 검색으로 관련 법률 문서 검색
- 🔐 **사용자 인증**: JWT 기반 회원가입 및 로그인 시스템
- 🎨 **현대적인 UI/UX**: React 19 기반의 반응형 웹 인터페이스
- 🔄 **LangGraph 워크플로우**: 쿼리 재구성 → 문서 검색 → 평가 → 답변 생성의 체계적인 파이프라인

## 🗂️ 프로젝트 구조

```
/workspace
├── Law_AI_Back/          # FastAPI 백엔드 서버
│   ├── app/
│   │   ├── auth/         # JWT 인증 모듈
│   │   ├── models/       # 데이터베이스 모델
│   │   ├── routers/      # API 라우터
│   │   ├── database.py   # DB 연결 설정
│   │   └── main.py       # FastAPI 앱 엔트리포인트
│   ├── requirements.txt  # Python 의존성
│   └── README.md
│
├── Law_AI_Front/         # React 프론트엔드
│   ├── src/
│   │   ├── api/          # 백엔드 API 통신
│   │   ├── components/   # UI 컴포넌트
│   │   ├── pages/        # 페이지 컴포넌트
│   │   ├── hooks/        # 커스텀 React Hooks
│   │   └── App.tsx       # 메인 앱 컴포넌트
│   ├── package.json      # Node.js 의존성
│   └── README.md
│
└── README.md             # 이 파일
```

## 🛠️ 기술 스택

### Backend
- **FastAPI** - 고성능 Python 웹 프레임워크
- **LangChain & LangGraph** - AI 워크플로우 오케스트레이션
- **Google Gemini 2.5 Pro** - 대규모 언어 모델
- **ChromaDB** - 벡터 데이터베이스
- **HuggingFace Embeddings** - BAAI/bge-m3 임베딩 모델
- **SQLite** - 사용자 데이터 관리
- **JWT** - 토큰 기반 인증

### Frontend
- **React 19** - 최신 React UI 라이브러리
- **TypeScript** - 타입 안정성
- **Vite** - 빠른 빌드 도구
- **React Router DOM** - 클라이언트 사이드 라우팅
- **Axios** - HTTP 클라이언트
- **FontAwesome** - 아이콘 라이브러리

## 🚀 시작하기

### 사전 요구사항

- Python 3.8 이상
- Node.js 16 이상
- Google API Key (Gemini API)
- 사전 구축된 ChromaDB 벡터 데이터베이스

### 설치 및 실행

각 서브 프로젝트의 README를 참조하세요:
- [Backend 설정 가이드](./Law_AI_Back/README.md)
- [Frontend 설정 가이드](./Law_AI_Front/README.md)

## 📊 시스템 아키텍처

```
사용자 질문
    ↓
[Frontend] React + TypeScript
    ↓
[Backend] FastAPI
    ↓
[LangGraph Workflow]
    ├─ Query Rewriter: 질문 재구성
    ├─ Retriever: ChromaDB에서 문서 검색
    ├─ Grader: 문서 관련성 평가
    └─ Generator: Gemini AI로 답변 생성
    ↓
최종 답변 반환
```

## 📝 API 엔드포인트

- `POST /api/answer` - 법률 질문에 대한 답변 생성
- `POST /api/auth/signup` - 회원가입
- `POST /api/auth/login` - 로그인
- `GET /` - 서버 상태 확인

## 🔑 환경 변수

Backend에서 필요한 환경 변수:
```
GOOGLE_API_KEY=your_gemini_api_key_here
```

## 👨‍💻 개발자

이 프로젝트는 AI 기반 법률 자문 서비스를 구현하여 법률 정보 접근성을 향상시키기 위해 개발되었습니다.

## 📄 라이선스

이 프로젝트는 교육 및 포트폴리오 목적으로 제작되었습니다.

---

**Note**: 이 서비스는 실제 법률 자문을 대체할 수 없으며, 참고용으로만 사용되어야 합니다. 중요한 법률 문제는 반드시 전문 변호사와 상담하시기 바랍니다.
