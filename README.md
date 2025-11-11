# LawAI 프로젝트

법률 질의응답을 위한 AI 기반 웹 애플리케이션입니다. RAG(Retrieval-Augmented Generation) 기술을 활용하여 법률 문서를 검색하고 답변을 생성합니다.

## 📁 프로젝트 구조

```
Law-AI-Final/
├── Law_AI_Back/          # 백엔드 (FastAPI + LangGraph)
│   ├── app/
│   │   ├── auth/         # 인증 관련 모듈
│   │   ├── models/       # 데이터베이스 모델
│   │   ├── routers/     # API 라우터
│   │   ├── database.py  # 데이터베이스 설정
│   │   └── main.py      # FastAPI 앱 진입점
│   ├── requirements.txt # Python 의존성
│   └── README.md        # 백엔드 상세 문서
│
└── Law_AI_Front/        # 프론트엔드 (React + TypeScript + Vite)
    ├── src/
    │   ├── api/         # API 호출 모듈
    │   ├── components/  # React 컴포넌트
    │   ├── hooks/       # React 커스텀 훅
    │   ├── pages/       # 페이지 컴포넌트
    │   └── types.ts     # TypeScript 타입 정의
    ├── package.json     # Node.js 의존성
    └── README.md        # 프론트엔드 상세 문서
```

## 🚀 빠른 시작

### 백엔드 실행

```bash
cd Law_AI_Back
pip install -r requirements.txt
uvicorn app.main:app --reload
```

백엔드는 기본적으로 `http://localhost:8000`에서 실행됩니다.

### 프론트엔드 실행

```bash
cd Law_AI_Front
npm install
npm run dev
```

프론트엔드는 기본적으로 `http://localhost:5173`에서 실행됩니다.

## 📚 상세 문서

- [백엔드 문서](./Law_AI_Back/README.md) - FastAPI 백엔드 상세 가이드
- [프론트엔드 문서](./Law_AI_Front/README.md) - React 프론트엔드 상세 가이드

## 🛠 기술 스택

### 백엔드
- **FastAPI** - 웹 프레임워크
- **LangGraph** - RAG 파이프라인 구성
- **LangChain** - LLM 통합
- **ChromaDB** - 벡터 데이터베이스
- **Google Gemini** - LLM 모델
- **SQLAlchemy** - ORM

### 프론트엔드
- **React 19** - UI 라이브러리
- **TypeScript** - 타입 안정성
- **Vite** - 빌드 도구
- **React Router** - 라우팅
- **Axios** - HTTP 클라이언트

## 📝 주요 기능

- 사용자 인증 (회원가입/로그인)
- 법률 문서 검색 및 질의응답
- RAG 기반 답변 생성
- 문서 관련성 평가 및 필터링
