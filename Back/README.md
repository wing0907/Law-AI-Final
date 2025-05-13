# LawAI Backend

FastAPI 기반의 법률 AI 챗봇 백엔드 서버입니다. LangGraph를 활용한 고급 RAG 파이프라인과 사용자 인증 시스템을 제공합니다.

## 🛠️ 기술 스택

### 핵심 프레임워크
- **FastAPI 0.111.0** - 고성능 비동기 Python 웹 프레임워크
- **Uvicorn** - ASGI 서버

### AI/ML 라이브러리
- **LangChain 0.2.7** - LLM 애플리케이션 개발 프레임워크
  - `langchain-core 0.2.11` - 핵심 기능
  - `langchain-community 0.2.6` - 커뮤니티 통합
- **LangGraph** - 상태 기반 워크플로우 관리 및 RAG 파이프라인 구성
- **ChromaDB 0.5.4** - 벡터 데이터베이스 (법률 문서 임베딩 저장)
- **HuggingFace Embeddings** - 텍스트 임베딩 모델
  - 모델: `BAAI/bge-m3` (다국어 지원 임베딩 모델)
- **Google Gemini API** - LLM 모델
  - 모델: `gemini-2.5-pro` (고급 추론 능력)

### 데이터베이스
- **PostgreSQL** - 사용자 인증 및 관리용 관계형 데이터베이스
- **SQLAlchemy** - Python ORM
- **ChromaDB** - 벡터 검색을 위한 임베딩 저장소

### 문서 처리
- **unstructured 0.14.7** - 문서 파싱 라이브러리
- **pypdf 4.2.0** - PDF 처리
- **pdfminer-six** - PDF 텍스트 추출

### 인증 및 보안
- **bcrypt** - 비밀번호 해싱
- **python-jose** - JWT 토큰 생성 및 검증
- **python-dotenv 1.0.1** - 환경 변수 관리

### 유틸리티
- **Pydantic 2.8.2** - 데이터 검증 및 설정 관리

## 📁 프로젝트 구조

```
Back/
├── app/
│   ├── __init__.py
│   ├── main.py              # FastAPI 앱 진입점
│   ├── database.py          # PostgreSQL 연결 설정
│   │
│   ├── auth/
│   │   ├── __init__.py
│   │   └── auth.py          # 인증 유틸리티 (비밀번호 해싱, JWT)
│   │
│   ├── models/
│   │   ├── __init__.py
│   │   └── user.py          # User 데이터베이스 모델
│   │
│   └── routers/
│       ├── __init__.py
│       ├── auth_router.py   # 인증 API (회원가입, 로그인)
│       └── answer_router.py # 법률 상담 API (RAG 파이프라인)
│
└── requirements.txt          # Python 의존성 목록
```

## 🚀 설치 및 실행

### 1. 사전 요구사항

- Python 3.10 이상
- PostgreSQL 데이터베이스 서버
- Google Gemini API 키
- ChromaDB 벡터 데이터베이스 (프로젝트 루트의 `Law_AI_DB/data` 디렉토리)

### 2. 가상 환경 설정

```bash
# 가상 환경 생성
python -m venv venv

# 가상 환경 활성화
# Windows
venv\Scripts\activate
# macOS/Linux
source venv/bin/activate
```

### 3. 의존성 설치

```bash
pip install -r requirements.txt
```

**추가로 설치가 필요한 패키지:**
```bash
pip install sqlalchemy psycopg2-binary bcrypt python-jose[cryptography] langgraph langchain-google-genai langchain-huggingface langchain-chroma
```

### 4. 환경 변수 설정

프로젝트 루트에 `.env` 파일을 생성하고 다음 내용을 추가:

```env
GOOGLE_API_KEY=your_google_api_key_here
```

### 5. 데이터베이스 설정

`app/database.py` 파일에서 PostgreSQL 연결 정보를 수정:

```python
DB_USER = "postgres"
DB_PASS = "your_password"
DB_HOST = "localhost"
DB_PORT = "5432"
DB_NAME = "postgres"
```

### 6. ChromaDB 경로 확인

`app/routers/answer_router.py`에서 ChromaDB 경로가 올바른지 확인:
- 기본 경로: 프로젝트 루트의 `Law_AI_DB/data` 디렉토리

### 7. 서버 실행

```bash
uvicorn app.main:app --reload --port 8000
```

서버가 성공적으로 실행되면 다음 주소에서 확인할 수 있습니다:
- API 문서: http://localhost:8000/docs
- 서버 상태: http://localhost:8000/

## 🔌 API 엔드포인트

### 인증 API (`/api/auth`)

#### 회원가입
```http
POST /api/auth/signup
Content-Type: application/json

{
  "email": "user@example.com",
  "password": "password123"
}
```

#### 로그인
```http
POST /api/auth/login
Content-Type: application/json

{
  "email": "user@example.com",
  "password": "password123"
}
```

응답:
```json
{
  "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "token_type": "bearer"
}
```

### 법률 상담 API (`/api`)

#### 답변 생성
```http
POST /api/answer
Content-Type: application/json

{
  "query": "계약서를 작성할 때 주의해야 할 사항은?",
  "no_llm": false
}
```

응답:
```json
{
  "answer": "계약서 작성 시 주의해야 할 사항은...",
  "retrieval": [
    {
      "content": "계약서 관련 법률 조항...",
      "source": "민법 제105조"
    }
  ]
}
```

## 🔄 RAG 파이프라인 구조

LangGraph를 사용한 고급 RAG 워크플로우:

1. **Query Rewriting** (`rewrite_query`)
   - 사용자 질문을 벡터 검색에 최적화된 형태로 재구성

2. **Retrieval** (`retrieve`)
   - ChromaDB에서 관련 법률 문서 검색 (상위 5개)

3. **Document Grading** (`grade_documents`)
   - 검색된 문서의 관련성 평가
   - 관련성이 있는 문서만 필터링

4. **Generation** (`generate`)
   - 관련 문서를 바탕으로 최종 답변 생성

5. **Fallback** (`fallback`)
   - 관련 문서가 없을 경우 대체 메시지 제공

## 🔐 인증 시스템

- **비밀번호 해싱**: bcrypt를 사용한 안전한 비밀번호 저장
- **JWT 토큰**: python-jose를 사용한 토큰 기반 인증
- **토큰 만료 시간**: 60분 (설정 가능)

## 📝 주요 설정

### CORS 설정
`app/main.py`에서 프론트엔드 주소를 허용 목록에 추가:
```python
origins = [
    "http://localhost:5173",
    "http://127.0.0.1:5173",
]
```

### 임베딩 모델 설정
`app/routers/answer_router.py`에서 GPU 사용 시:
```python
embeddings = HuggingFaceEmbeddings(
    model_name="BAAI/bge-m3",
    model_kwargs={'device': 'cuda'},  # 'cpu' → 'cuda'
    encode_kwargs={'normalize_embeddings': True}
)
```

## 🐛 문제 해결

### ChromaDB 경로 오류
- `Law_AI_DB/data` 디렉토리가 존재하는지 확인
- 프로젝트 루트에서 상대 경로가 올바른지 확인

### Google API 키 오류
- `.env` 파일이 올바른 위치에 있는지 확인
- 환경 변수가 제대로 로드되는지 확인

### 데이터베이스 연결 오류
- PostgreSQL 서버가 실행 중인지 확인
- `database.py`의 연결 정보가 올바른지 확인

## 📚 참고 자료

- [FastAPI 공식 문서](https://fastapi.tiangolo.com/)
- [LangChain 공식 문서](https://python.langchain.com/)
- [LangGraph 공식 문서](https://langchain-ai.github.io/langgraph/)
- [ChromaDB 공식 문서](https://docs.trychroma.com/)
