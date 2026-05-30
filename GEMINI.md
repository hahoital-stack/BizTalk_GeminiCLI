# 업무 말투 변환기 (BizTalk Tone Converter) 지침서

본 문서는 업무 말투 변환기 프로젝트의 구조, 기술 스택, 개발 원칙 및 Gemini CLI를 위한 작업 지침을 담고 있습니다.

## 🚀 프로젝트 개요

- **목적**: 일상적인 대화체를 격식 있는 비즈니스 언어로 자동 변환하여 원활한 직장 내 소통 지원
- **주요 기능**: 수신 대상(상사, 동료, 고객 등)의 특성에 맞춘 AI 기반 말투 변환
- **핵심 기술**: FastAPI(백엔드), Vanilla JavaScript(프론트엔드), Upstage Solar-Pro(LLM)

## 💡 바이브 코딩 3원칙 (개발 가이드라인)

모든 개발 작업 시 다음의 3원칙을 최우선으로 준수합니다.

1. **완료 기준 우선 정의**: "무엇을 구현하면 작업이 끝나는가?"에 대한 체크리스트를 먼저 작성합니다.
2. **조사 우선, 구현 나중**: API 연동이나 새로운 라이브러리 도입 전, 최신 사용법과 제약 사항을 먼저 파악합니다.
3. **버그 분석 우선, 수정 나중**: 에러 발생 시 즉시 코드를 고치기보다 에러의 근본 원인을 먼저 분석하고 설명합니다.

## 🛠 기술 스택 및 환경 설정

### 기술 스택
- **백엔드**: Python 3.11+, FastAPI, LangChain, `langchain-upstage`
- **프론트엔드**: HTML5, CSS3, JavaScript (ES6+)
- **AI 모델**: Upstage Solar-Pro (Solar-Pro2/3)
- **배포 및 관리**: GitHub, Vercel

### 환경 변수 설정 (`.env`)
```bash
UPSTAGE_API_KEY=발급받은_API_키
```
*주의: `.env` 파일은 보안을 위해 절대 소스 제어(Git)에 포함하지 않습니다.*

### 로컬 실행 방법
1. **필수 패키지 설치**:
   ```bash
   pip install fastapi uvicorn langchain python-dotenv langchain-upstage pydantic
   ```
2. **백엔드 서버 실행**:
   ```bash
   cd backend
   uvicorn main:app --reload --port 8000
   ```
3. **프론트엔드 확인**: `frontend/index.html` 파일을 브라우저에서 실행합니다.

## 📂 권장 프로젝트 구조

```
biztalk_gemini-cli/
├── backend/                # 백엔드 서버 로직
│   ├── main.py             # FastAPI 진입점 및 CORS 설정
│   ├── routers/            # API 엔드포인트 정의
│   ├── services/           # LLM 변환 핵심 로직
│   ├── prompts/            # 수신 대상별 프롬프트 템플릿
│   └── models/             # Pydantic 데이터 모델 (Schemas)
├── frontend/               # 프론트엔드 정적 파일
│   ├── index.html          # 메인 UI
│   ├── css/                # 스타일시트
│   └── js/                 # 클라이언트 사이드 스크립트
├── GEMINI.md               # 프로젝트 작업 지침 (본 파일)
├── PRD_업무말투변환기.md    # 제품 요구사항 명세서
└── 개요서_업무말투변환기.md # 프로젝트 개요 및 배경
```

## 📝 작업 및 소통 규칙

- **언어**: 모든 소통, 주석, 문서는 **한국어**를 원칙으로 합니다.
- **보안**: `@my-rules.md`에 정의된 금지 행동(민감 정보 노출, 파괴적 작업 등)을 엄격히 따릅니다.
- **문서 및 지침 동기화**: 
    - PRD나 개요서 등 주요 문서가 변경되면, `GEMINI.md`의 관련 지침도 즉시 업데이트하여 일관성을 유지합니다.
    - 실제 코드 구현이 변경되어 문서와 차이가 발생할 경우, 관련 MD 파일의 명세나 체크리스트를 즉시 현행화합니다.
- **보고**: 작업 시작 전 계획을 공유하고, 단계별 진행 상황을 명확히 전달합니다.
