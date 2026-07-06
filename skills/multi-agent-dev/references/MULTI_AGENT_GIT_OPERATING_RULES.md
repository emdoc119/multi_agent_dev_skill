# MULTI_AGENT_GIT_OPERATING_RULES.md

## 목적
이 문서는 멀티 에이전트 개발 workflow를 GitHub 기반으로 운영할 때 발생할 수 있는 충돌, 동시 수정, 오래된 branch, 잘못된 merge, 문맥 불일치 문제를 줄이기 위한 운영 규칙을 정의한다 [web:173][web:175][web:179].

## 기본 원칙
- 프로젝트별 repo 분리
- 공통 skill/template repo 분리
- main 보호
- 작은 branch, 작은 PR
- 한 repo 당 동시에 writer agent 1개 원칙

## Repo 운영
### 프로젝트 repo
- 각 프로젝트는 별도 GitHub repo 사용
- 코드, 문서, task board, decision log는 해당 repo 안에 둔다

### 공통 workflow repo
- reusable skill/prompt/template은 별도 repo 보관
- 예: `agent-skills`, `antigravity-workflows`
- 프로젝트 시작 전 최신 버전을 pull하여 참조

## Branch 규칙
- main 직접 push 금지
- feature/refine/review branch 사용
- branch는 목적이 드러나게 naming
- 오래된 branch는 rebase 또는 폐기

## 동시 작업 규칙
- 같은 repo에는 동시에 writer 1개만 허용
- 추가 agent는 review/proposal/doc-only 역할로 제한
- 같은 파일을 둘 이상 수정해야 하면 먼저 ownership 지정

## PR 규칙
모든 PR에는 아래를 포함한다.
- 목적
- 변경 범위
- 영향을 받는 모듈
- 테스트 여부
- known risk
- rollback 방법

## Sync 체크리스트
작업 시작 전:
- 최신 main pull/rebase
- 현재 branch 목적 확인
- canonical docs 확인

작업 종료 전:
- 변경 범위 문서화
- 테스트 실행
- PR 또는 patch 준비
- conflicts 여부 확인

merge 전:
- reviewer 승인
- main 최신 반영
- CI 또는 최소 테스트 확인

## canonical docs
아래 문서는 항상 최신 상태를 기준으로 삼는다.
- `docs/prd.md`
- `docs/architecture.md`
- `docs/task-board.md`
- `docs/current-state.md`
- `docs/decision-log.md`

## 금지 사항
- main 직접 수정
- reviewer의 코드 직접 수정
- architecture 승인 전 대규모 구현 시작
- secret/API key 커밋
- 충돌 해결 없이 강제 overwrite

## 추천 폴더
- `docs/`
- `reviews/`
- `qa/`
- `prompts/`
- `skills/`
- `scripts/`
