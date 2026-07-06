# REPO_STRUCTURE_multi_agent_dev.md

## 목적
멀티 에이전트 개발 workflow를 GitHub repo에 저장하고 재사용하기 위한 추천 저장소 구조를 정의한다 [web:145][web:146][web:199].

## 추천 방식
### A. 공통 workflow 전용 repo
예: `agent-skills` 또는 `multi-agent-dev-workflows`

```text
multi-agent-dev-workflows/
├─ README.md
├─ skills/
│  └─ multi-agent-dev/
│     ├─ SKILL.md
│     └─ references/
│        ├─ PROMPT_project_kickoff_v2.md
│        ├─ PROMPT_iteration_refine_v2.md
│        ├─ MULTI_AGENT_GIT_OPERATING_RULES.md
│        └─ REPO_STRUCTURE_multi_agent_dev.md
├─ templates/
│  ├─ docs-prd-template.md
│  ├─ docs-architecture-template.md
│  ├─ docs-task-board-template.md
│  └─ docs-decision-log-template.md
└─ examples/
   └─ stock-dashboard-example.md
```

### B. 각 프로젝트 repo 안의 추천 구조
```text
project-repo/
├─ README.md
├─ docs/
│  ├─ prd.md
│  ├─ architecture.md
│  ├─ task-board.md
│  ├─ decision-log.md
│  └─ current-state.md
├─ reviews/
├─ qa/
├─ prompts/
├─ skills/
├─ src/
├─ tests/
└─ scripts/
```

## 운영 팁
- 공통 skill repo는 version tag를 붙여 관리
- 프로젝트 시작 시 어떤 skill version을 쓰는지 `docs/current-state.md`에 기록
- 대형 프로젝트는 module-level docs를 추가
- skill은 root prompt보다 folder-based reference 구조가 안정적 [web:145][web:146][web:199]
