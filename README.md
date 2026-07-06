# Multi-Agent Dev Workflow Repo

이 저장소는 여러 프로젝트에서 재사용할 수 있는 **멀티 에이전트 개발 workflow 세트**를 담는다.
핵심 목적은 다음과 같다.

- broad한 프로젝트 아이디어를 PM 인터뷰를 통해 구체화
- Info Collector -> Architect -> Coder -> Reviewer -> QA Gate 흐름 고정
- Git 기반 repo 운영 규칙과 동기화/충돌 제어 내장
- kickoff / refine / 문서 템플릿을 재사용 가능한 형태로 제공

## 포함 파일

### skills
- `skills/multi-agent-dev/SKILL.md`
- `skills/multi-agent-dev/references/PROMPT_project_kickoff_v2.md`
- `skills/multi-agent-dev/references/PROMPT_iteration_refine_v2.md`
- `skills/multi-agent-dev/references/MULTI_AGENT_GIT_OPERATING_RULES.md`
- `skills/multi-agent-dev/references/REPO_STRUCTURE_multi_agent_dev.md`
- `skills/multi-agent-dev/references/multi_agent_dev_workflow_summary.md`

### templates
- `templates/docs-prd-template.md`
- `templates/docs-architecture-template.md`
- `templates/docs-task-board-template.md`
- `templates/docs-decision-log-template.md`
- `templates/docs-current-state-template.md`

### examples
- `examples/example-project-starter.md`

## 권장 사용 방식

### 1. 새 프로젝트 시작
아래 문서들을 참조하게 한다.
- `skills/multi-agent-dev/SKILL.md`
- `skills/multi-agent-dev/references/PROMPT_project_kickoff_v2.md`

실행 예시:

```text
첨부한 `skills/multi-agent-dev/SKILL.md`를 상위 운영 규칙으로 사용해.
이번 작업은 `PROMPT_project_kickoff_v2.md`를 기준으로 시작해.
먼저 PM 인터뷰 단계부터 진행하고, 충분한 정보가 모이면 Info Collector -> Architect -> Coder -> Reviewer -> QA Gate 순서로 진행해.
```

### 2. 기존 프로젝트 고도화
아래 문서들을 참조하게 한다.
- `skills/multi-agent-dev/SKILL.md`
- `skills/multi-agent-dev/references/PROMPT_iteration_refine_v2.md`
- `templates/docs-current-state-template.md`

### 3. Git 운영
모든 프로젝트 repo는 아래 규칙을 따른다.
- 프로젝트별 repo 분리
- main 보호
- writer agent 1개 원칙
- 작은 branch / 작은 PR
- canonical docs 유지

세부 규칙은 `MULTI_AGENT_GIT_OPERATING_RULES.md` 참고.

## 추천 repo 구조

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
│        ├─ REPO_STRUCTURE_multi_agent_dev.md
│        └─ multi_agent_dev_workflow_summary.md
├─ templates/
│  ├─ docs-prd-template.md
│  ├─ docs-architecture-template.md
│  ├─ docs-task-board-template.md
│  ├─ docs-decision-log-template.md
│  └─ docs-current-state-template.md
└─ examples/
   └─ example-project-starter.md
```

## GitHub에 올릴 때 중요한 점
- GitHub는 **폴더 구조를 자동으로 재배치해주지 않는다**.
- 즉, **로컬에서 폴더 구조를 만든 뒤 그대로 commit/push** 해야 한다.
- 웹에서 파일만 하나씩 올리면 가능은 하지만, 폴더 구조를 직접 관리해야 해서 비추천이다.
- 가장 좋은 방법은 로컬에서 폴더를 만든 뒤 `git add . && git commit && git push` 하는 것이다.

## Claude Code용 팁
Claude Code는 skill 폴더 구조를 잘 활용할 수 있으므로, 이 repo의 `skills/multi-agent-dev/` 폴더를 그대로 재사용하기 좋다.
필요하면 `~/.claude/skills/`에 복사하거나 symlink로 연결해도 된다.
