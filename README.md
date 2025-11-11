# LawAI Project

FastAPI 기반 백엔드와 React 기반 프론트엔드를 함께 제공하는 LawAI 프로젝트입니다. 아래 안내를 통해 각각의 코드와 실행 방법을 확인할 수 있습니다.

## Repository Structure
- `Law_AI_Back/` – FastAPI, LangGraph, Ollama를 사용하는 백엔드 서비스
- `Law_AI_Front/` – Vite + React + TypeScript로 구현한 프론트엔드

## Quick Start
### Backend
1. `cd Law_AI_Back`
2. (선택) 가상환경 생성 후 활성화
3. `pip install -r requirements.txt`
4. `uvicorn app.main:app --reload`

### Frontend
1. `cd Law_AI_Front`
2. `npm install`
3. `npm run dev`

## Portfolio Links
- [Backend Portfolio](./Law_AI_Back)
- [Frontend Portfolio](./Law_AI_Front)
