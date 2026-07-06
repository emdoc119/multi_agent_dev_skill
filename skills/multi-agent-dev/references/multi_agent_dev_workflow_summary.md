# multi-agent-dev workflow 총정리

## 핵심 파일
1. `SKILL_multi_agent_dev_v3.md`
2. `PROMPT_project_kickoff_v2.md`
3. `PROMPT_iteration_refine_v2.md`
4. `MULTI_AGENT_GIT_OPERATING_RULES.md`
5. `REPO_STRUCTURE_multi_agent_dev.md`

## 추천 운영 방식
### 1. 공통 repo에 저장
공통 skill/prompt/git rules/template은 별도 GitHub repo에 저장한다.

### 2. 프로젝트 시작 시
- `SKILL_multi_agent_dev_v3.md`를 상위 규칙으로 사용
- `PROMPT_project_kickoff_v2.md`를 실행 템플릿으로 사용
- PM 인터뷰를 통해 broad 요구를 구체화

### 3. 고도화 시
- `SKILL_multi_agent_dev_v3.md`를 상위 규칙으로 사용
- `PROMPT_iteration_refine_v2.md`를 실행 템플릿으로 사용
- Reviewer 관점 진단 + refine 계획 수립

### 4. Git 운영
- 프로젝트별 repo 분리
- 공통 skill repo 분리
- main 보호
- writer agent 1개 원칙
- 작은 PR과 canonical docs 유지

## 외부 에이전트에 전달하는 문장 예시
```text
첨부한 `SKILL_multi_agent_dev_v3.md`를 상위 운영 규칙으로 사용해.
이번 작업은 `PROMPT_project_kickoff_v2.md`를 기준으로 시작해.
Git 운영은 `MULTI_AGENT_GIT_OPERATING_RULES.md`를 따르고, repo 구조는 `REPO_STRUCTURE_multi_agent_dev.md`를 참고해.
먼저 PM 인터뷰 단계부터 진행하고, 충분한 정보가 모이면 Info Collector -> Architect -> Coder -> Reviewer -> QA Gate 순서로 진행해.
```
