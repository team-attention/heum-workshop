---
name: part-extra
description: Heum 3시간 강의 Part Extra — Agent Teams, Hook, Plugin. 3시간 강의에서 다 못 다룬 심화 개념(에이전트 팀, 훅, 플러그인)을 선택적으로 다룬다. "파트엑스트라", "Part Extra", "extra", "agent-teams", "hook", "plugin" 요청에 사용.
---

# Part Extra: Agent Teams, Hook, Plugin

> 3시간 강의에서 Part 1~3의 핵심(sync/clarify/wrap)을 다룬 후, 시간이 남거나 질문이 나왔을 때 선택적으로 진행하는 확장 블록.

이 스킬이 호출되면 아래 **STOP PROTOCOL**을 반드시 따른다.

---

## 용어 정리

| 용어 | 설명 |
|------|------|
| **Agent Teams** | 여러 전문 에이전트를 팀으로 구성해 복잡한 작업을 병렬 실행하는 패턴 |
| **Hook** | 특정 이벤트(tool 사용 전/후, 세션 시작/종료 등)에 자동 실행되는 스크립트 |
| **Plugin** | Skill + MCP + Hook + Agent를 묶은 설치 단위 |
| **TeamCreate** | Claude Code에서 팀 기반 병렬 실행을 시작하는 tool |
| **settings.json** | Hook 설정이 들어가는 Claude Code 설정 파일 |

---

## STOP PROTOCOL — 절대 위반 금지

각 블록은 반드시 2턴에 걸쳐 진행한다 (Phase A → Stop → Phase B).

```
┌─ Phase A (첫 번째 턴) ──────────────────────────────┐
│ 1. references/에서 해당 블록의 EXPLAIN 섹션을 읽는다      │
│ 2. 기능을 설명한다                                     │
│ 3. references/에서 EXECUTE 섹션을 읽는다                │
│ 4. "지금 직접 실행해보세요"라고 안내한다                  │
│ 5. ⛔ STOP. 턴 종료.                                    │
└──────────────────────────────────────────────────────────┘

  ⬇️ 사용자 "완료" / "다음"

┌─ Phase B (두 번째 턴) ──────────────────────────────┐
│ 1. QUIZ 섹션을 읽는다                                  │
│ 2. AskUserQuestion으로 퀴즈 출제                        │
│ 3. 정답/오답 피드백                                    │
│ 4. 다음 블록 이동 여부 확인                             │
└──────────────────────────────────────────────────────────┘
```

### Phase A 종료 시 필수 문구

```
---
👆 위 내용을 직접 실행해보세요.
실행이 끝나면 "완료" 또는 "다음"이라고 입력해주세요.
```

---

## 소요 시간

| Block | 주제 | 예상 시간 |
|-------|------|-----------|
| Extra-1 | Agent Teams — 병렬 전문가 팀 | ~15분 |
| Extra-2 | Hook — 자동화 이벤트 | ~15분 |
| Extra-3 | Plugin — 스킬/MCP/Hook/Agent 패키징 | ~15분 |
| **합계** | | **~45분** |

> 3개 블록 전부 진행 시 45분. 시간에 따라 1~2개만 선택적으로 진행.
> 원본은 Day 1의 Block 3-5, 3-6, 3-7에 해당한다.

---

## 핵심 전략

> **"핵심 3종(sync/clarify/wrap) 위에 얹는 가속 도구들"**

- **Agent Teams**: sync/clarify/wrap을 병렬로 돌릴 수 있게 되는 순간
- **Hook**: 명시적 명령 없이도 자동 실행되는 워크플로우
- **Plugin**: 본인이 만든 스킬/훅/에이전트를 팀에 배포하는 단위

3가지 개념은 독립적이므로 순서는 참가자 관심도에 따라 조정 가능.

---

## References 파일 맵

| 블록 | 파일 | 주제 |
|------|------|------|
| Extra-1 | `references/block3-5-agent-teams.md` | Agent Teams — 병렬 전문가 팀 |
| Extra-2 | `references/block3-6-hook.md` | Hook — 자동화 이벤트 |
| Extra-3 | `references/block3-7-plugin.md` | Plugin — 스킬/MCP/Hook/Agent 패키징 |

> 각 reference 파일은 `## EXPLAIN`, `## EXECUTE`, `## QUIZ` 섹션으로 구성된다.
> 원본 파일명은 Day 1의 Block 3-5/6/7이지만 본 스킬에서는 Extra-1/2/3으로 참조한다.

---

## 진행 규칙

- Part 1~3 완료 후 시간이 남거나, 참가자 질문이 이 영역에 닿을 때 호출
- 3개 블록 중 참가자 관심도가 높은 것부터 진행
- 전부 skip도 허용 — 본편은 Part 1~3이다

---

## 시작

Part Extra 시작 시 어떤 개념부터 다룰지 선택한다.

```
AskUserQuestion({
  "question": "Part Extra: 어떤 개념부터 볼까요?",
  "header": "시작 블록",
  "options": [
    {"label": "Extra-1: Agent Teams", "description": "여러 에이전트를 팀으로 병렬 실행"},
    {"label": "Extra-2: Hook", "description": "이벤트 기반 자동 실행 스크립트"},
    {"label": "Extra-3: Plugin", "description": "스킬/MCP/Hook/Agent 묶음 패키지"}
  ],
  "multiSelect": false
})
```

> 공동 세션 강사(심근/문성훈/최의진)와 진행 중 방향이 바뀌면 블록 순서/깊이를 유연하게 조정한다.
