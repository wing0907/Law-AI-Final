# 🔧 LawAI Backend

FastAPI 기반의 AI 법률 자문 서비스 백엔드 서버입니다. LangGraph를 활용한 RAG(Retrieval-Augmented Generation) 파이프라인으로 법률 질문에 대한 정확한 답변을 생성합니다.

## 🛠️ 기술 스택

### 핵심 프레임워크
- **FastAPI 0.111.0** - 고성능 비동기 웹 프레임워크
- **Uvicorn 0.30.1** - ASGI 서버
- **Pydantic 2.8.2** - 데이터 검증 및 직렬화

### AI & Machine Learning
- **LangChain 0.2.7** - LLM 애플리케이션 개발 프레임워크
- **LangChain Core 0.2.11** - LangChain 핵심 컴포넌트
- **LangChain Community 0.2.6** - 커뮤니티 통합
- **LangGraph** - AI 워크플로우 오케스트레이션
- **Google Gemini 2.5 Pro** - 대규모 언어 모델 (API)

### 벡터 데이터베이스 & 임베딩
- **ChromaDB 0.5.4** - 벡터 데이터베이스
- **HuggingFace Embeddings** - BAAI/bge-m3 임베딩 모델

### 문서 처리
- **Unstructured 0.14.7** - 문서 파싱
- **PyPDF 4.2.0** - PDF 처리
- **PDFMiner-six 20231228** - PDF 텍스트 추출

### 기타
- **Python-dotenv 1.0.1** - 환경 변수 관리
- **SQLite** - 사용자 데이터베이스
- **JWT** - 인증 토큰

## 📁 프로젝트 구조

```
Law_AI_Back/
├── app/
│   ├── __init__.py
│   ├── main.py              # FastAPI 앱 엔트리포인트
│   ├── database.py          # SQLite 데이터베이스 설정
│   │
│   ├── auth/
│   │   ├── __init__.py
│   │   └── auth.py          # JWT 토큰 생성 및 검증
│   │
│   ├── models/
│   │   ├── __init__.py
│   │   └── user.py          # 사용자 모델 (SQLAlchemy)
│   │
│   └── routers/
│       ├── __init__.py
│       ├── answer_router.py # RAG 파이프라인 API
│       └── auth_router.py   # 인증 API
│
├── requirements.txt         # Python 의존성
└── README.md               # 이 파일
```

## 🚀 시작하기

### 1. 사전 요구사항

- **Python 3.8 이상**
- **Google API Key** (Gemini API 사용)
- **ChromaDB 벡터 데이터베이스** (사전 구축 필요)
  - 경로: `../Law_AI_DB/data/`
  - BAAI/bge-m3 임베딩으로 색인된 법률 문서

### 2. 환경 설정

프로젝트 루트에 `.env` 파일을 생성하고 다음 내용을 추가하세요:

```bash
GOOGLE_API_KEY=your_gemini_api_key_here
```

### 3. 의존성 설치

```bash
cd Law_AI_Back
pip install -r requirements.txt
```

### 4. 서버 실행

```bash
# 개발 모드 (자동 리로드)
uvicorn app.main:app --reload --host 0.0.0.0 --port 8000

# 또는
python -m uvicorn app.main:app --reload --host 0.0.0.0 --port 8000
```

서버가 실행되면 다음 주소에서 접근할 수 있습니다:
- API 서버: http://localhost:8000
- API 문서 (Swagger): http://localhost:8000/docs
- API 문서 (ReDoc): http://localhost:8000/redoc

## 📡 API 엔드포인트

### 인증 API

#### 회원가입
```http
POST /api/auth/signup
Content-Type: application/json

{
  "username": "user123",
  "email": "user@example.com",
  "password": "securepassword"
}
```

#### 로그인
```http
POST /api/auth/login
Content-Type: application/x-www-form-urlencoded

username=user123&password=securepassword
```

**응답:**
```json
{
  "access_token": "eyJhbGciOiJIUzI1NiIs...",
  "token_type": "bearer"
}
```

### 법률 질문 API

#### 답변 생성
```http
POST /api/answer
Content-Type: application/json
Authorization: Bearer {access_token}

{
  "query": "임대차 계약 해지는 어떻게 하나요?",
  "no_llm": false
}
```

**응답:**
```json
{
  "answer": "임대차 계약 해지는...",
  "retrieval": [
    {
      "content": "관련 법률 문서 내용...",
      "source": "민법 제635조"
    }
  ]
}
```

### 서버 상태 확인
```http
GET /
```

## 🔄 RAG 파이프라인 워크플로우

LangGraph를 사용한 체계적인 워크플로우:

```
1. Query Rewriter (쿼리 재구성)
   └─ 사용자 질문을 검색에 최적화된 형태로 변환
   
2. Retriever (문서 검색)
   └─ ChromaDB에서 관련 법률 문서 검색 (k=5)
   
3. Document Grader (문서 평가)
   └─ 검색된 문서의 관련성 평가
   
4. Generate (답변 생성) OR Fallback (대체 응답)
   ├─ 관련 문서 있음 → Gemini AI로 답변 생성
   └─ 관련 문서 없음 → 대체 메시지 반환
```

## 🔧 주요 컴포넌트

### 1. 임베딩 모델
- **모델**: BAAI/bge-m3 (HuggingFace)
- **디바이스**: CPU (GPU 사용 시 설정 변경 가능)
- **정규화**: 활성화

### 2. 벡터 데이터베이스
- **DB**: ChromaDB
- **검색 방식**: Similarity Search
- **검색 문서 수**: 5개 (k=5)

### 3. LLM
- **모델**: Google Gemini 2.5 Pro
- **Temperature**: 0 (일관된 답변)
- **용도**: 쿼리 재구성, 문서 평가, 답변 생성

## 🔐 인증 시스템

- **방식**: JWT (JSON Web Token)
- **토큰 만료**: 설정 가능
- **비밀번호**: Bcrypt 해싱
- **데이터베이스**: SQLite

## 🌐 CORS 설정

프론트엔드 개발 서버와의 통신을 위해 다음 origin이 허용됩니다:
- `http://localhost:5173`
- `http://127.0.0.1:5173`

프로덕션 환경에서는 `app/main.py`의 `origins` 리스트를 수정하세요.

## 📊 데이터베이스

SQLite 데이터베이스는 첫 실행 시 자동으로 생성됩니다.

**테이블:**
- `users`: 사용자 정보 (id, username, email, hashed_password)

## 🐛 디버깅

서버 로그에서 다음 정보를 확인할 수 있습니다:
- 임베딩 모델 로드 상태
- ChromaDB 연결 상태
- 각 RAG 파이프라인 노드 실행 로그
- 쿼리 재구성 결과
- 문서 평가 결과

## 📝 개발 참고사항

### ChromaDB 경로 설정
`answer_router.py`에서 ChromaDB 경로가 올바른지 확인하세요:

```python
db_path = Path(__file__).resolve().parents[3] / "Law_AI_DB" / "data"
```

### GPU 사용
GPU를 사용하려면 `answer_router.py`에서 다음을 수정하세요:

```python
embeddings = HuggingFaceEmbeddings(
    model_name="BAAI/bge-m3",
    model_kwargs={'device': 'cuda'},  # 'cpu' → 'cuda'
    encode_kwargs={'normalize_embeddings': True}
)
```

## 🔗 관련 링크

- [FastAPI 공식 문서](https://fastapi.tiangolo.com/)
- [LangChain 공식 문서](https://python.langchain.com/)
- [LangGraph 문서](https://langchain-ai.github.io/langgraph/)
- [Google Gemini API](https://ai.google.dev/)
- [ChromaDB 문서](https://docs.trychroma.com/)

## ⚠️ 주의사항

- `.env` 파일은 절대 Git에 커밋하지 마세요
- API Key는 안전하게 관리하세요
- 프로덕션 환경에서는 적절한 보안 설정을 추가하세요
- 이 서비스는 실제 법률 자문을 대체할 수 없습니다

---

**문의사항이나 버그 리포트는 이슈로 등록해주세요.**
