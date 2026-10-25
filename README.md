# 전명준

**AI 서비스 개발 · Python 백엔드**

AI 기능을 API와 사용자 화면까지 연결합니다. Python·FastAPI 기반 기능 구현, 구조화된 LLM 응답, 데이터 저장과 예외 처리를 다뤘습니다. 게임 QA 실무에서 쌓은 오류 재현·로그 분석 경험을 개발과 검증에 활용합니다.

## 프로젝트 한눈에 보기

- **도담 정책 AI 요약** · 교육 팀 프로젝트 · 2026.06.09–07.01<br>
  정책 API·AI 요약·비동기 화면 연동<br>
  [팀 백엔드](https://github.com/bistel-mini-2/bistel-mini-2-backend) · [팀 프론트엔드](https://github.com/bistel-mini-2/bistel-mini-2-frontend)
- **재무 RAG·BI 기업 비교** · 교육 팀 프로젝트 · 4인 · 2026.07.27–09.11<br>
  기업 비교 API·재무 지표·순위·화면·테스트, 상태 저장 오류 수정, 평가 자료 설계·검증 참여<br>
  [팀 원본](https://github.com/bist-mini-final/bist-mini-final)
- **AVERA:404 리듬게임** · 1인 개발 · 2026.07–진행 중<br>
  웹 게임·API·DB 연동, 채보 이력 보존, 성적 중복 저장 방지, DSP/CNN 비교<br>
  비공개 저장소 · 아래에 구현 범위 정리

팀 프로젝트는 원본 저장소를 연결했습니다. 아래에는 팀 전체 서비스와 제가 담당한 기능을 나누고, 본인 구현을 확인할 수 있는 커밋을 함께 정리했습니다.

## 도담 정책 AI 요약

가족·육아 복지 정책을 탐색하고 추천·분석·질의응답을 제공하는 팀 서비스입니다.

**제가 담당한 기능**

- 정책 검색·필터·페이지네이션과 관심 정책 API 및 화면 연동
- 정책 조건과 검색 근거를 입력으로 구성하고, LangChain 구조화 출력으로 요약과 근거를 분리해 반환
- 생성 결과 캐시와 조건 변경 확인, AI 호출 시간 제한, 호출 실패 시 정책 정보에 근거한 대체 요약
- Next.js 화면의 생성 대기·완료·실패·재시도 처리, 화면 이탈 시 요청 취소와 타이머 정리
- 캐시 재사용·조건 변경·대체 응답을 확인하는 테스트 작성

**본인 구현 근거**

- [정책 요약 API·LangGraph·캐시·테스트](https://github.com/bistel-mini-2/bistel-mini-2-backend/commit/180fdbda8c3e121c0b258c14bc9678859c426241)
- [요약 화면 연동·상태 조회·재시도·요청 정리](https://github.com/bistel-mini-2/bistel-mini-2-frontend/commit/d06e7712692d5fccff88c1c16459b5593166bce5)

**사용 기술:** Python · FastAPI · SQLAlchemy · PostgreSQL · LangChain · LangGraph · Next.js

## 재무 RAG·BI 기업 비교

Excel 재무 데이터를 조회하고 근거를 확인하는 RAG·BI 팀 서비스입니다. 4인 팀에서 기업 비교 기능과 검증을 담당했습니다.

**제가 담당한 기능**

- 기업 비교 API와 응답 모델, 재무 지표 계산 및 순위·정렬 화면 구현
- 저장 데이터와 응답 타입의 호환성 처리, 원본 데이터 보존을 확인하는 테스트 관리
- Windows에서 상태 파일 교체가 일시적으로 실패하는 문제에 재시도·임시 파일 정리 적용
- 파일 교체 실패를 의도적으로 재현하고 저장 성공·임시 파일 정리를 확인하는 회귀 테스트 작성
- 질문·기대 답변·Excel 참조 셀을 연결한 평가 자료와 재무 합성 데이터의 설계·검증 참여

**본인 구현 근거**

- [기업 비교 API·계산·React 화면·테스트](https://github.com/bist-mini-final/bist-mini-final/commit/08bbeaca1066bc33e3389692893967f44968a1cf)
- [Windows 상태 저장 재시도·정리·회귀 테스트](https://github.com/bist-mini-final/bist-mini-final/commit/ec689216d25d4cfc53a95af554c41cdd5d38617b)
- [팀 프로젝트 정리](https://github.com/bist-mini-final/bist-mini-final/blob/main/docs/PROJECT_SUMMARY.md)
- [시연 범위와 챕터 안내](https://github.com/bist-mini-final/bist-mini-final/blob/main/docs/assets/demo/README.md)

**사용 기술:** Python · FastAPI · Pydantic · React · TypeScript · pytest

## AVERA:404 리듬게임

플레이·이야기·해금·성적 저장·기록·랭킹을 연결하는 1인 개발 프로젝트입니다.

**구현과 검증**

- 웹 플레이와 FastAPI·PostgreSQL 저장 흐름 연결
- 채보 ID·버전·SHA256 해시를 관리해 채보 수정 후에도 과거 성적 이력 보존
- 제출 ID·내용 해시와 DB 고유 제약을 결합해 중복 성적 저장 방지
- 동일 내용 재요청·다른 내용 충돌·동시 요청을 실제 DB 조건에서 검증
- 피아노 두 곡의 합계 120초, 허용 오차 ±60ms 조건에서 DSP/CNN onset 검출 비교: F1 0.96639 / 0.84058
- 비교 결과를 바탕으로 해당 조건에서는 DSP를 유지하고 CNN 채택을 보류

**진행 상태:** 2026.10.23 로컬 구현 기준 6곡·54모드입니다. 저장소는 비공개이며, 외부 배포·정식 릴리스는 보류 중입니다. 위 수치는 제한된 두 곡의 비교 결과입니다. 실제 화면·코드 발췌·테스트 조건은 지원용 포트폴리오에 정리했습니다.

개발과 미디어 제작에 AI 도구를 활용했으며, 직접 구현한 범위·실험 조건·개발 중인 항목을 구분해 기록합니다.

## 사용 기술

- **백엔드:** Python · FastAPI · SQLAlchemy · Pydantic · PostgreSQL
- **AI 기능:** LangChain · LangGraph · 구조화 출력 · RAG 평가 자료 · DSP/CNN 비교 실험
- **화면·검증:** JavaScript · TypeScript · React · Next.js · pytest · Git · Docker
