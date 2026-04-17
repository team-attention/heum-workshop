# Block 3-7: Plugin

> **Phase A 시작 시 반드시 아래 형태로 출력한다:**
> ```
> 📖 공식 문서: https://code.claude.com/docs/ko/plugins
> 📖 마켓플레이스: https://code.claude.com/docs/ko/discover-plugins
> ```

## EXPLAIN

| 항목 | 내용 |
|------|------|
| 근본 원리 | **패키징과 배포** — 위의 기능들은 모두 개별 파일이다. Plugin은 이것들을 하나의 설치 단위로 묶어서, 한 줄로 팀 전체가 동일한 환경을 갖추게 한다 |
| 비유 | 종합 패키지 — 위의 모든 기능을 묶어서 팀에 공유 |
| 예시 | "마케팅 팀용 플러그인" 하나로 Skill + MCP + Hook + Agent 설치 |

```
개별 설치 (Plugin 없이)          Plugin (한 번에)
┌─────────┐                    ┌─────────────────┐
│ Skill A │ ← 수동 복사         │ marketing-plugin│
│ Skill B │ ← 수동 복사         │ ┌─ Skill A,B   │
│ MCP 설정 │ ← 수동 설정   vs   │ ├─ MCP 설정    │
│ Hook 설정│ ← 수동 설정         │ ├─ Hook 설정   │
│ Agent   │ ← 수동 설정         │ └─ Agent       │
└─────────┘                    └────────┬────────┘
  팀원 각자 반복                         │
                              claude plugin add
                                한 줄이면 끝
```

## EXECUTE

Plugin이 무엇인지 **"둘러보기"** 수준으로 체험한다. 본 3시간 강의에서는 별도 설치를 요구하지 않는다 — 핵심 스킬(clarify 계열, session-wrap 등)은 이미 이 레포(`heum-3h/`)에 직접 포함되어 있기 때문이다.

### 1단계: `/plugin` 명령어로 Plugin 둘러보기

Claude Code에는 공식 마켓플레이스가 있다. 명령어로 어떤 Plugin들이 있는지 둘러본다:

```
/plugin
```

> UI에서 공식/커뮤니티 Plugin 목록을 확인한다. **설치는 선택 사항**이고, 본 강의에서는 설치하지 않아도 된다.

### 2단계: 이 레포에 포함된 "Plugin 스타일" 구조 관찰

Plugin이 Skill + MCP + Hook + Agent의 묶음이라는 점은 레포 구조로도 관찰 가능하다:

```
heum-3h/.claude/
├── skills/          ← 여러 skill이 담긴 폴더 (clarify 계열, session-wrap 등)
├── agents/          ← session-wrap이 호출하는 전문 에이전트들
└── commands/        ← /wrap 같은 슬래시 명령어
```

> 이 구조가 사실상 "설치 안 된 Plugin의 해부도"다. 파일이 직접 노출되어 있어서 어떤 구성요소가 있는지 한눈에 볼 수 있다.

### 3단계: (선택) 외부 Plugin 설치해보기

교육 후 본인 프로젝트에서 Plugin 설치 자체를 체험하고 싶다면, 공식 문서(`/plugin`)의 마켓플레이스 UI를 참고하면 된다. 본 강의 진행 중에는 설치하지 않는다.

## QUIZ

```json
AskUserQuestion({
  "questions": [{
    "question": "Plugin은 뭘 묶은 것인가요?",
    "header": "Quiz 3-7",
    "options": [
      {"label": "Skill + MCP + Hook + Agent 등을 하나의 패키지로", "description": "여러 기능을 팀 단위로 배포"},
      {"label": "Skill만 묶은 것", "description": "Skill 외에도 MCP, Hook, Agent 포함"},
      {"label": "외부 도구만 묶은 것", "description": "내부 기능도 포함"}
    ],
    "multiSelect": false
  }]
})
```

정답: 1번.
