# LawAI Backend

LangGraph 기반 RAG(ReTRieval-Augmented Generation) 파이프라인과 인증 기능을 제공하는 FastAPI 서비스입니다. 프론트엔드에서 법률 질의를 전송하면, 백엔드가 벡터 스토어에서 문서를 검색하고 Gemini 모델을 통해 답변을 생성합니다.

## Tech Stack
- Python 3.11+
- FastAPI, Uvicorn
- LangGraph, LangChain Core/Community
- HuggingFace `BAAI/bge-m3` 임베딩 + ChromaDB
- Google Generative AI `gemini-2.5-pro`
- SQLAlchemy + PostgreSQL
- bcrypt, python-jose (JWT)
- python-dotenv

## Prerequisites
1. **Python** 3.11 이상
2. **PostgreSQL** 인스턴스  
   기본 연결 정보는 `app/database.py`에 정의되어 있습니다. 실제 환경에 맞게 사용자, 비밀번호, 호스트, 포트를 수정하거나 환경 변수로 분리하세요.
3. **Google API Key**  
   LangGraph 파이프라인에서 `ChatGoogleGenerativeAI`를 사용하므로 `GOOGLE_API_KEY` 값을 `.env` 로 제공해야 합니다.
4. **Chroma 벡터 스토어**  
   `Law_AI_DB/data` 디렉터리에 사전 구축된 ChromaDB가 존재해야 합니다. 최초 실행 시에는 별도의 데이터 적재 스크립트로 해당 폴더를 구성하세요.

## Setup
```bash
cd Law_AI_Back
python -m venv .venv
source .venv/bin/activate  # Windows는 .venv\Scripts\activate
pip install --upgrade pip
pip install -r requirements.txt
```

루트에 `.env` 파일을 생성하고 Google API 키를 설정합니다.
```
GOOGLE_API_KEY=your-google-api-key
```

필요하다면 JWT `SECRET_KEY`, 데이터베이스 접속 정보 등 민감 값도 `.env` 로 이동해 관리하세요.

## Running Locally
```bash
uvicorn app.main:app --reload --port 8000
```

서버가 시작되면 기본 헬스 체크 엔드포인트는 `GET http://localhost:8000/` 입니다. 개발용 CORS 허용 도메인은 `http://localhost:5173` 으로 설정되어 있으며, 필요 시 `app/main.py` 에서 수정하세요.

## API Overview
- `GET /` – 애플리케이션 상태 확인
- `POST /api/answer` – LangGraph 파이프라인을 통해 답변과 근거 문서를 생성
- `POST /api/auth/register` – 신규 사용자 등록
- `POST /api/auth/login` – 로그인 및 JWT 발급

프론트엔드는 `/api/*` 경로를 Vite 프록시로 호출하며, 자세한 사용법은 프론트엔드 README를 참고하세요.

## Project Structure
```
Law_AI_Back/
├── app/
│   ├── auth/                # 비밀번호 해시 및 JWT 발급
│   ├── models/              # SQLAlchemy 모델 (예: User)
│   ├── routers/             # FastAPI 라우터 (answer, auth)
│   ├── database.py          # PostgreSQL 연결 설정
│   └── main.py              # FastAPI 앱 및 CORS 설정
├── requirements.txt
└── README.md
```

## Notes
- `secret` 값과 데이터베이스 자격 증명은 운영 환경에서 반드시 환경 변수로 분리하세요.
- GPU 환경이 있다면 `answer_router.py`에서 `HuggingFaceEmbeddings` 의 `model_kwargs` 값을 `{'device': 'cuda'}` 로 변경해 성능을 높일 수 있습니다.
- Ollama 기반 모델로 대체하려면 LangChain 관련 모듈을 교체하고 `langchain_community.llms.ollama` 등의 드라이버를 사용하도록 수정하세요.
