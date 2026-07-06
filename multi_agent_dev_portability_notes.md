# multi_agent_dev_portability_notes.md

## 질문
이 3종 세트(`SKILL_multi_agent_dev_v2.md`, `PROMPT_project_kickoff_v2.md`, `PROMPT_iteration_refine_v2.md`)를 Antigravity, Codex, Claude 같은 다른 코딩 에이전트 환경에서도 쓸 수 있는가?

## 짧은 답
**네, 가능하다.** 다만 가장 안정적인 방식은 “그냥 붙여넣기”보다 **skill/markdown 파일로 함께 제공**하는 것이다 [web:145][web:146][web:150].

## 왜 가능한가
Claude Code는 SKILL.md 형태의 재사용 가능한 markdown workflow를 공식적으로 지원하며, 하나의 skill 디렉토리에 `SKILL.md`와 보조 reference 파일을 함께 둘 수 있다 [web:145][web:146]. 또한 최근에는 Agent Skills 같은 오픈 표준이 등장해 Claude Code 스타일의 skill markdown을 다른 에이전트에도 이식 가능하게 하는 흐름이 있다 [web:150][web:151].

Codex CLI나 다른 코딩 에이전트에서도 markdown 기반 절차 문서는 사실상 reusable prompt로 사용할 수 있다. 다만 프레임워크별 포맷 민감도와 실행 습관이 달라서, portable skill은 가능하지만 완전한 plug-and-play는 아니며 약간의 적응이 필요하다는 연구 결과가 있다 [web:149].

## 권장 사용 방식
### 1. 나와 같은 대화에서 사용할 때
- `SKILL_multi_agent_dev_v2.md`를 상위 규칙으로 간주
- 짧은 프로젝트 프롬프트만 던져도 됨

예시:
```text
multi-agent-dev skill v2를 사용해서 새 프로젝트 시작해.
내가 만들고 싶은 것은 X야.
부족한 정보가 있으면 PM Agent가 필요한 질문부터 하면서 계획을 구체화해.
```

### 2. Antigravity 같은 외부 자율 개발 환경
- 3개 파일을 모두 첨부
- kickoff 또는 refine 중 하나를 메인 프롬프트로 지정
- skill 파일을 상위 규칙으로 사용하라고 명시

예시:
```text
첨부한 `SKILL_multi_agent_dev_v2.md`를 상위 운영 규칙으로 사용해.
이번 프로젝트는 `PROMPT_project_kickoff_v2.md`를 기준으로 시작해.
먼저 PM 인터뷰 단계부터 진행하고, 충분한 정보가 모이면 계획을 구체화해.
```

### 3. Claude Code
Claude Code는 skill 디렉토리 구조를 지원하므로, 아래처럼 두는 것이 이상적이다 [web:145][web:146].

```text
multi-agent-dev/
  SKILL.md
  references/
    project-kickoff-v2.md
    iteration-refine-v2.md
    portability-notes.md
```

### 4. Codex / 기타 에이전트
- skill 파일을 markdown reference로 첨부
- 첫 줄에 “이 문서를 상위 규칙으로 사용하라”고 명시
- 필요시 에이전트별로 헤더/메타데이터만 약간 조정

## 실무 팁
- 같은 세션이면 짧은 프롬프트만으로 충분한 경우가 많다.
- 새 세션/새 도구/팀 공유라면 항상 파일도 함께 주는 편이 좋다 [web:150][web:154].
- 가장 좋은 구조는 `skill = 고정 운영 규칙`, `kickoff/refine = 프로젝트 실행 템플릿`이다 [web:154].
- 장기적으로는 레포 안에 versioned markdown skill 세트로 관리하는 것이 좋다 [web:146][web:153].
