# Example Project Starter

## 예시 프로젝트
트레이딩용 매크로 정보판 웹앱

## 시작 상황
사용자가 말한다.
- “장전 브리핑, 장중 모니터링, 장후 리뷰에 쓸 매크로 정보판을 만들고 싶어.”

## 이 workflow의 반응
### 1. PM 인터뷰 시작
PM Agent는 아래를 먼저 묻는다.
- 가장 중요한 사용 시나리오는 무엇인가?
- 이번 1차 MVP 범위는 어디까지인가?
- 어떤 데이터 소스를 쓸 수 있는가?
- 웹앱인가, 봇인가, 둘 다인가?
- Telegram/알림이 필요한가?

### 2. 요구사항 요약
PM Agent는 답변을 받아 아래를 정리한다.
- Objective
- In Scope
- Out of Scope
- Definition of Done
- Open Risks

### 3. 조사 -> 설계 -> 구현
- Info Collector: 데이터/API/레퍼런스 조사
- Architect: 구조/인터페이스/폴더 설계
- Coder: 골격 생성 및 구현
- Reviewer: gap 확인
- QA Gate: MVP readiness 평가

## kickoff 예시 문장
```text
첨부한 `skills/multi-agent-dev/SKILL.md`를 상위 운영 규칙으로 사용해.
이번 작업은 `PROMPT_project_kickoff_v2.md`를 기준으로 시작해.
내가 만들고 싶은 것은 “트레이딩용 매크로 정보판 웹앱”이야.
부족한 정보가 있으면 PM Agent가 필요한 최소 질문부터 하면서 범위를 구체화해.
```

## refine 예시 문장
```text
첨부한 `skills/multi-agent-dev/SKILL.md`를 상위 운영 규칙으로 사용해.
이번 작업은 `PROMPT_iteration_refine_v2.md`를 기준으로 진행해.
현재 1차 버전은 완성됐지만, 데이터 신뢰성과 알림 중복 문제가 있다.
필요하면 PM Agent가 최소 질문으로 refine 범위를 좁힌 뒤 개선 계획을 세워.
```
