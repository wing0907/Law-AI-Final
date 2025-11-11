# LawAI Backend

FastAPI 기반의 법률 질의응답 백엔드 서버입니다. LangGraph를 활용한 RAG(Retrieval-Augmented Generation) 파이프라인을 구현했습니다.

## 🛠 기술 스택

### 웹 프레임워크
- **FastAPI** (v0.111.0) - 고성능 비동기 웹 프레임워크
- **Uvicorn** (v0.30.1) - ASGI 서버

### AI/ML 라이브러리
- **LangChain** (v0.2.7) - LLM 애플리케이션 개발 프레임워크
- **LangChain Core** (v0.2.11) - LangChain 핵심 기능
- **LangChain Community** (v0.2.6) - 커뮤니티 통합
- **LangGraph** - 상태 기반 워크플로우 구성

### 벡터 데이터베이스
- **ChromaDB** (v0.5.4) - 임베딩 벡터 저장 및 검색

### 문서 처리
- **Unstructured** (v0.14.7) - 문서 파싱 및 구조화
- **PyPDF** (v4.2.0) - PDF 처리
- **PDFMiner.six** (20231228) - PDF 텍스트 추출

### 데이터베이스 & ORM
- **SQLAlchemy** - Python ORM (requirements.txt에 명시되지 않았지만 사용 중)
- **Pydantic** (v2.8.2) - 데이터 검증 및 설정 관리

### 유틸리티
- **python-dotenv** (v1.0.1) - 환경 변수 관리

### LLM 모델
- **Google Gemini 2.5 Pro** - 답변 생성용 LLM
- **BAAI/bge-m3** - 임베딩 모델 (HuggingFace)

## 📁 프로젝트 구조

```
Law_AI_Back/
├── app/
│   ├── __init__.py
│   ├── main.py              # FastAPI 앱 진입점 및 CORS 설정
│   ├── database.py          # 데이터베이스 연결 설정
│   ├── auth/
│   │   ├── __init__.py
│   │   └── auth.py          # JWT 인증 및 비밀번호 해싱
│   ├── models/
│   │   ├── __init__.py
│   │   └── user.py          # 사용자 데이터베이스 모델
│   └── routers/
│       ├── __init__.py
│       ├── auth_router.py   # 인증 API (회원가입/로그인)
│       └── answer_router.py # RAG 파이프라인 API
├── requirements.txt
└── README.md
```

## 🚀 설치 및 실행

### 1. 환경 설정

```bash
# 가상 환경 생성 (선택사항)
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate

# 의존성 설치
pip install -r requirements.txt
```

### 2. 환경 변수 설정

`.env` 파일을 생성하고 다음 변수를 설정하세요:

```env
GOOGLE_API_KEY=your_google_api_key_here
DATABASE_URL=sqlite:///./law_ai.db
```

### 3. 데이터베이스 준비

ChromaDB 벡터 데이터베이스가 `Law_AI_DB/data` 경로에 있어야 합니다.
법률 문서가 임베딩되어 저장되어 있어야 합니다.

### 4. 서버 실행

```bash
uvicorn app.main:app --reload
```

서버는 `http://localhost:8000`에서 실행됩니다.

## 📡 API 엔드포인트

### 인증 API (`/api/auth`)

- `POST /api/auth/register` - 회원가입
- `POST /api/auth/login` - 로그인

### 답변 API (`/api`)

- `POST /api/answer` - 법률 질의응답

### 상태 확인

- `GET /` - 서버 상태 확인

## 🔄 RAG 파이프라인 흐름

1. **Query Rewriting** - 사용자 질문을 검색에 최적화된 형태로 재구성
2. **Retrieval** - ChromaDB에서 관련 문서 검색 (상위 5개)
3. **Grading** - 검색된 문서의 관련성 평가
4. **Generation** - 관련 문서를 바탕으로 최종 답변 생성
5. **Fallback** - 관련 문서가 없을 경우 대체 답변 제공

## 🔐 인증

JWT(JSON Web Token) 기반 인증을 사용합니다.
- 회원가입 시 비밀번호는 bcrypt로 해싱되어 저장됩니다.
- 로그인 시 JWT 토큰이 발급되며, 프론트엔드에서 `access_token`으로 저장됩니다.

## 📝 주요 기능

- 사용자 회원가입 및 로그인
- 법률 문서 벡터 검색
- LangGraph 기반 RAG 파이프라인
- 문서 관련성 자동 평가
- Google Gemini를 활용한 답변 생성
