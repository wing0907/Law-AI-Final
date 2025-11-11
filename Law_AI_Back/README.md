# LawAI Backend

FastAPI 기반으로 구축된 LawAI 백엔드는 LangGraph와 Ollama를 활용해 법률 질의응답 기능을 제공합니다. 인증, 사용자 관리, 문서 임베딩 등 핵심 기능을 포함하고 있습니다.

## Tech Stack
- **Language & Runtime:** Python 3.11+
- **Web Framework:** FastAPI, Uvicorn
- **AI Orchestration:** LangChain, LangGraph
- **LLM Runtime:** Ollama (예: `llama3`, `mistral` 등 사전 설치 필요)
- **Vector Store:** ChromaDB
- **Database & ORM:** PostgreSQL, SQLAlchemy
- **Authentication:** bcrypt, python-jose 기반 JWT
- **Document Processing:** Unstructured, PyPDF, pdfminer.six

## Prerequisites
- Python 3.11 이상
- PostgreSQL 실행 환경
- Ollama 설치 및 사용할 모델 다운로드

## Setup
```bash
cd Law_AI_Back
python -m venv .venv
source .venv/bin/activate  # Windows는 .venv\Scripts\activate
pip install -r requirements.txt
```

1. `.env` 파일을 생성해 데이터베이스, Ollama 등 민감 정보를 설정합니다.
2. PostgreSQL에 접속해 필요한 데이터베이스를 생성합니다.
3. Ollama에서 사용할 모델을 미리 pull 합니다. 예) `ollama pull llama3`.

## Run
```bash
uvicorn app.main:app --reload
```

- 기본 주소: `http://127.0.0.1:8000`
- API 문서: `http://127.0.0.1:8000/docs`

## Project Structure
- `app/main.py` – FastAPI 엔트리포인트 및 라우터 등록
- `app/routers/` – 인증 및 답변 API 라우터
- `app/models/` – SQLAlchemy 모델 정의
- `app/auth/` – JWT 인증, 비밀번호 해시 유틸리티
- `app/database.py` – 데이터베이스 및 세션 설정
