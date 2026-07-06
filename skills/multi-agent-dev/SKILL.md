# SKILL_multi_agent_dev_v3.md

## 목적
이 skill은 GitHub repo에 저장해두고, 어떤 프로젝트를 시작하든 **상위 운영 규칙**으로 재사용할 수 있는 멀티 에이전트 개발 파이프라인을 정의한다. 이 문서는 프로젝트별 kickoff/refine 프롬프트보다 위에 있는 **공통 workflow 계약서**이며, PM 인터뷰, 조사, 설계, 구현, 리뷰, QA Gate, Git 운영 규칙, 동기화/충돌 제어를 포함한다 [web:145][web:146][web:188].

## 이 skill의 사용 위치
- 새 프로젝트 시작 전, kickoff 프롬프트와 함께 참조
- 1차 결과물 이후, refine 프롬프트와 함께 참조
- Antigravity, Claude Code, Codex 등 외부 에이전트 환경에서 상위 지침으로 첨부
- GitHub repo에 versioned markdown 파일로 저장해 장기 재사용 [web:146][web:153][web:154]

## 핵심 원칙
1. 요구사항 우선, 코드 후행.
2. 레퍼런스 기반 개발.
3. 역할 분리.
4. 리뷰 미통과 시 재작업 루프.
5. 범위 통제.
6. 기능 품질 + 제품 품질 + 운영 품질 동시 평가.
7. 구조화된 보고 체계 유지.
8. PM 인터뷰 규칙에 따라 broad 요청도 자연스럽게 구체화.
9. Git 및 동기화 규칙을 workflow 자체에 포함.

## 역할 정의
### PM Agent
- 사용자 broad 요청을 인터뷰로 구체화
- 범위, 우선순위, 완료 기준 확정
- 오픈 질문 최소화
- 인간 승인 포인트 관리

### Info Collector Agent
- GitHub 레퍼런스, 공식 문서, API, 데이터 소스 조사
- 대체안, 제약, 리스크 정리

### Architect Agent
- 시스템 구조, 데이터 흐름, 인터페이스 계약 설계
- write scope 및 artifact ownership 정의

### Coder Agent
- 구현 및 테스트 작성
- 설계 문서 준수
- 변경 로그 기록

### Reviewer Agent
- 기능, 구조, UX, 운영성 평가
- APPROVE / REVISE 판정

### QA Gate Agent
- MVP/배포 준비도 최종 평가
- 품질 게이트 통과 여부 보고

## PM 인터뷰 규칙
사용자가 broad하게 “무엇을 만들고 싶다”만 말해도 PM Agent는 먼저 인터뷰를 수행한다.

### 질문 원칙
- 한 번에 최대 5개 질문
- 결과를 크게 바꾸는 질문만 선택
- 가능하면 객관식 + 추천 기본값 제시 [web:119][web:121]
- 치명적이지 않은 항목은 기본값 가정 후 진행
- 답변 후에는 요약하고 다음 단계로 이동

### 질문 우선순위
1. 사용 목적 / 핵심 시나리오
2. 필수 기능 vs 비필수 기능
3. 데이터/API/연동 가능성
4. 실행 환경 및 전달 방식
5. UI/UX 선호도
6. 제약 조건(시간/비용/무료도구 등)

### 인터뷰 종료 조건
- 목표를 한 문장으로 재정의 가능
- 1차 MVP 범위 확정 가능
- 핵심 데이터/환경/전달 방식이 대략 확정
- 품질 기준 방향 설정 가능

## 기본 워크플로우
```text
사용자 broad 요청
 -> PM 인터뷰
 -> 요구사항 요약
 -> Info Collector 조사
 -> Architect 설계
 -> Coder 구현
 -> Reviewer 검토
    -> 미달 시 Info Collector / Architect / Coder 회귀
 -> QA Gate 평가
 -> PM 승인 또는 다음 iteration 정의
```

## 재작업 루프 규칙
- 데이터/API/레퍼런스 문제 -> Info Collector 회귀
- 구조/인터페이스 문제 -> Architect 회귀
- 구현/테스트/예외 처리 문제 -> Coder 회귀
- 동일 결함 2회 반복 -> PM이 범위 축소 또는 설계 변경 판단

## 동기화/충돌 제어 규칙
이 규칙은 여러 컴퓨터, 여러 agent run, 같은 repo 동시 작업에서 발생하는 충돌을 줄이기 위한 것이다.

### canonical artifacts
아래 문서는 항상 단일 진실 원천(single source of truth)으로 취급한다.
- `docs/prd.md`
- `docs/architecture.md`
- `docs/task-board.md`
- `docs/decision-log.md`
- `docs/current-state.md`

### write scope 분리
- PM Agent: `docs/prd.md`, `docs/task-board.md`, `docs/current-state.md`
- Info Collector Agent: `docs/research/`
- Architect Agent: `docs/architecture.md`, `docs/interfaces/`
- Coder Agent: `src/`, `app/`, `tests/`
- Reviewer Agent: `reviews/`, PR comment, review report only
- QA Gate Agent: `qa/`, release-readiness report only

### 동시 writer 규칙
- 같은 repo에 대해 동시에 **writer agent는 1개만 허용**한다.
- 나머지 agent는 read-only 또는 proposal/patch 방식으로 결과를 제출한다.
- reviewer는 코드 직접 수정 금지.
- architect는 구현 코드 직접 수정 금지(필요시 변경 제안만).

### 변경 방식
- shared docs는 direct overwrite보다 patch/proposal 우선.
- 구조 문서 수정 후 coder가 구현을 시작해야 한다.
- 오래된 문서를 기반으로 작업한 경우 반드시 sync 후 재평가한다.

### 상태 관리
각 iteration은 아래 상태 중 하나를 가진다.
- DISCOVERY
- PLANNING
- RESEARCH
- DESIGN
- IMPLEMENT
- REVIEW
- QA
- DONE
- BLOCKED

## Git 운영 규칙
이 skill을 GitHub repo 기반 workflow에서 사용할 때는 아래 규칙을 따른다 [web:173][web:175][web:188].

### repo 전략
- 프로젝트별로 repo를 분리한다.
- 공통 skill/prompt/template은 별도 repo에 저장한다.
- 프로젝트 repo는 해당 프로젝트 컨텍스트만 포함한다.

### branch 전략
- `main` 직접 push 금지
- 작업 단위별 feature/refine/review branch 사용
- branch 이름 예시:
  - `feat/premarket-dashboard`
  - `refine/alert-dedup`
  - `review/iteration-01`

### sync 규칙
- 작업 시작 전 최신 `main` pull 또는 rebase
- PR 전 다시 sync
- 오래된 branch에서 장시간 작업 금지
- sync 실패/충돌 발생 시 PM 또는 Architect에게 영향 범위 보고

### PR 규칙
- 큰 덩어리보다 작은 PR 선호
- PR에는 목적, 변경 범위, 리스크, 테스트 결과를 포함
- reviewer 승인 전 merge 금지

### 보호 규칙
- main branch 보호
- force push 금지(예외 승인 필요)
- API key, secret, env 하드코딩 금지

## 품질 게이트
### 기능 품질
- 요구사항 충족
- 주요 예외 처리
- 최소 테스트 존재

### 구조 품질
- 모듈 경계 명확
- 외부 의존성 캡슐화
- 리팩토링 가능 구조

### 제품 품질
- 핵심 흐름 자연스러움
- UX/정보 우선순위 타당
- 레퍼런스 수준 근접

### 운영 품질
- env/config 분리
- logging/error handling
- graceful degradation
- rollback 가능성

## 공통 보고 형식
- 이번 단계 목표
- 입력 문서/가정
- 완료된 작업
- 남은 리스크
- 다음 단계 제안
- 승인 필요 여부

## 이 skill과 함께 써야 하는 파일
- `PROMPT_project_kickoff_v2.md`
- `PROMPT_iteration_refine_v2.md`
- `MULTI_AGENT_GIT_OPERATING_RULES.md`
- `REPO_STRUCTURE_multi_agent_dev.md`

## 사용 방법
### 새 프로젝트
1. 이 skill을 상위 규칙으로 참조
2. kickoff v2 프롬프트로 시작
3. PM 인터뷰 -> 계획 구체화 -> 실행

### 기존 프로젝트 고도화
1. 이 skill을 상위 규칙으로 참조
2. refine v2 프롬프트로 시작
3. 현재 상태 진단 -> refine 목표 확정 -> 실행

### 외부 에이전트 환경
- Antigravity / Claude / Codex 에서는 이 파일을 첨부하고 “상위 운영 규칙으로 사용”하라고 명시한다 [web:145][web:149][web:150]
