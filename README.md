# LawAI - 법률 AI 챗봇 프로젝트

[![GitHub Repository](https://img.shields.io/badge/GitHub-Repository-blue?logo=github)](https://github.com/wing0907/Law-AI-Final)

법률 문서를 기반으로 한 RAG(Retrieval-Augmented Generation) 기반 AI 챗봇 서비스입니다. LangGraph를 활용한 고급 RAG 파이프라인과 React 기반의 현대적인 웹 인터페이스를 제공합니다.

## 🔗 프로젝트 링크

- **GitHub Repository**: [https://github.com/wing0907/Law-AI-Final](https://github.com/wing0907/Law-AI-Final)

---

## 📋 프로젝트 개요

LawAI는 법률 관련 질문에 대해 정확하고 신뢰할 수 있는 답변을 제공하는 AI 챗봇입니다. ChromaDB 벡터 데이터베이스에 저장된 법률 문서를 검색하고, Google Gemini 모델을 활용하여 사용자 질문에 대한 답변을 생성합니다.

### ✨ 주요 기능

- 🔐 **사용자 인증** - JWT 기반 회원가입 및 로그인
- 🔍 **벡터 검색** - ChromaDB를 활용한 법률 문서 검색
- 🤖 **고급 RAG 파이프라인** - LangGraph 기반 지능형 답변 생성
- 💬 **실시간 상담** - 법률 질문에 대한 즉각적인 답변 제공
- 📱 **반응형 UI** - 모던하고 직관적인 웹 인터페이스

---

## 🏗️ 프로젝트 구조

```
Law-AI-Final/
│
├── Back/                    # FastAPI 백엔드
│   ├── app/                 # 애플리케이션 코드
│   ├── requirements.txt     # Python 의존성
│   └── README.md           # 백엔드 가이드
│
├── Front/                   # React 프론트엔드
│   ├── src/                 # 소스 코드
│   ├── package.json         # Node.js 의존성
│   └── README.md           # 프론트엔드 가이드
│
└── README.md               # 프로젝트 메인 문서
```

> 📖 각 폴더의 상세한 구조와 설명은 해당 폴더의 README.md를 참조하세요.

---

## 🚀 빠른 시작

### 사전 요구사항

- **Python** 3.10 이상
- **Node.js** 18 이상
- **PostgreSQL** 데이터베이스
- **Google Gemini API** 키
- **ChromaDB** 벡터 데이터베이스 (프로젝트 루트의 `Law_AI_DB/data` 디렉토리)

### 백엔드 실행

```bash
# 1. 백엔드 디렉토리로 이동
cd Back

# 2. 가상 환경 생성 및 활성화
python -m venv venv
# Windows
venv\Scripts\activate
# macOS/Linux
source venv/bin/activate

# 3. 의존성 설치
pip install -r requirements.txt

# 4. 환경 변수 설정 (.env 파일 생성)
echo GOOGLE_API_KEY=your_google_api_key_here > .env

# 5. 데이터베이스 설정 (app/database.py 수정)

# 6. 서버 실행
uvicorn app.main:app --reload --port 8000
```

📚 자세한 내용은 [Back/README.md](./Back/README.md)를 참조하세요.

### 프론트엔드 실행

```bash
# 1. 프론트엔드 디렉토리로 이동
cd Front

# 2. 의존성 설치
npm install

# 3. 개발 서버 실행
npm run dev
```

📚 자세한 내용은 [Front/README.md](./Front/README.md)를 참조하세요.

---

## 🛠️ 기술 스택

### 백엔드
| 기술 | 용도 |
|------|------|
| **FastAPI** | 고성능 Python 웹 프레임워크 |
| **LangChain** | LLM 애플리케이션 개발 프레임워크 |
| **LangGraph** | 상태 기반 워크플로우 관리 |
| **ChromaDB** | 벡터 데이터베이스 |
| **HuggingFace Embeddings** | 텍스트 임베딩 (BAAI/bge-m3) |
| **Google Gemini** | LLM 모델 (gemini-2.5-pro) |
| **PostgreSQL** | 관계형 데이터베이스 |
| **SQLAlchemy** | ORM |
| **bcrypt** | 비밀번호 해싱 |
| **python-jose** | JWT 토큰 처리 |

### 프론트엔드
| 기술 | 용도 |
|------|------|
| **React 19** | UI 라이브러리 |
| **TypeScript** | 타입 안정성 |
| **Vite** | 빌드 도구 및 개발 서버 |
| **React Router** | 클라이언트 사이드 라우팅 |
| **Axios** | HTTP 클라이언트 |
| **FontAwesome** | 아이콘 라이브러리 |

---

## 📚 주요 기능

### RAG 파이프라인

1. **Query Rewriting** - 사용자 질문을 검색에 최적화된 형태로 재구성
2. **Retrieval** - ChromaDB에서 관련 법률 문서 검색
3. **Grading** - 검색된 문서의 관련성 평가
4. **Generation** - 관련 문서를 바탕으로 최종 답변 생성

### 인증 시스템

- JWT 기반 토큰 인증
- bcrypt를 사용한 안전한 비밀번호 해싱
- 회원가입 및 로그인 기능

---

## 📝 API 엔드포인트

### 인증
- `POST /api/auth/register` - 회원가입
- `POST /api/auth/login` - 로그인

### 법률 상담
- `POST /api/answer` - 법률 질문에 대한 답변 생성

---

## 🔧 환경 설정

### 백엔드 환경 변수
```env
GOOGLE_API_KEY=your_google_api_key_here
```

### 데이터베이스 경로
- **ChromaDB**: 프로젝트 루트의 `Law_AI_DB/data` 디렉토리
- **PostgreSQL**: `Back/app/database.py`에서 설정

---

## 📖 문서

- [백엔드 가이드](./Back/README.md) - 백엔드 상세 설정 및 API 문서
- [프론트엔드 가이드](./Front/README.md) - 프론트엔드 상세 설정 및 컴포넌트 설명

---

## 📄 라이선스

이 프로젝트는 개인 포트폴리오 프로젝트입니다.

---

## 👤 작성자

프로젝트 개발자

---

<div align="center">

**⭐ 이 프로젝트가 도움이 되었다면 Star를 눌러주세요! ⭐**

[![GitHub Repository](https://img.shields.io/badge/GitHub-Repository-blue?logo=github)](https://github.com/wing0907/Law-AI-Final)

</div>
