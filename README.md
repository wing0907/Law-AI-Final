# LawAI

LangGraph 기반 법률 리서치 어시스턴트 프로젝트입니다. FastAPI 백엔드와 React + TypeScript 프론트엔드를 한 저장소에서 관리하여 코드와 문서를 한눈에 볼 수 있도록 정리했습니다.

## Repository Structure
| Path | Description |
| --- | --- |
| [`Law_AI_Back/`](./Law_AI_Back) | LangGraph 기반 RAG 파이프라인과 인증 API를 제공하는 FastAPI 서버. [:link: 상세 문서](./Law_AI_Back/README.md) |
| [`Law_AI_Front/`](./Law_AI_Front) | 백엔드 API를 사용하는 React + Vite 싱글 페이지 애플리케이션. [:link: 상세 문서](./Law_AI_Front/README.md) |

## How to Explore
- **Backend 먼저 보기** → [`Law_AI_Back/app`](./Law_AI_Back/app)에 핵심 비즈니스 로직이 정리되어 있습니다.
- **Frontend 먼저 보기** → [`Law_AI_Front/src`](./Law_AI_Front/src)에서 UI 컴포넌트와 페이지 구성을 확인할 수 있습니다.
- 자세한 실행 방법과 환경 변수 설정은 각 폴더의 README를 참고하세요.

## Portfolio Quick Links
프로젝트를 포트폴리오에 소개할 때 아래 상대 경로를 그대로 사용하면 리뷰어가 곧바로 코드에 접근할 수 있습니다.
- Backend Source: `./Law_AI_Back/`
- Frontend Source: `./Law_AI_Front/`

필요시 이 README를 루트 인덱스로 링크하고, 세부 설명은 각 서브 README로 안내하면 깔끔하게 정리된 프로젝트 구조를 보여줄 수 있습니다.
