---
name: part1-sync
description: Heum 3시간 강의 Part 1 — MCP & Context Sync. MCP가 뭔지 배우고, Slack을 연결해 나만의 Context Sync 스킬을 만들기 시작한다. "파트1", "Part 1", "sync", "MCP" 요청에 사용.
---

# Part 1: MCP & Context Sync

이 스킬이 호출되면 아래 **STOP PROTOCOL**을 반드시 따른다.

---

## 용어 정리

| 용어 | 설명 |
|------|------|
| **MCP** | Model Context Protocol. AI와 외부 도구를 연결하는 오픈 표준. USB-C처럼 다양한 서비스를 하나의 규격으로 연결 |
| **Host / Client / Server** | MCP의 3요소. Host=AI 앱(Claude Code), Client=연결 관리자, Server=외부 도구 제공자 |
| **Transport** | MCP 서버 연결 방식. HTTP(클라우드 서비스)와 stdio(로컬 실행) 2가지 |
| **Connector** | claude.ai에서 제공하는 브라우저 기반 MCP 연결 방법 |
| **스킬(Skill)** | Claude Code에게 특정 작업 방법을 가르치는 문서 |
| **STUB** | 나중에 채울 빈칸. 스켈레톤 스킬에서 "여기에 내용이 들어갑니다"라는 표시 |
| **frontmatter** | 파일 맨 위에 `---`로 감싼 정보 영역. 스킬의 이름, 설명, 트리거 등을 적는 곳 |

---

## STOP PROTOCOL — 절대 위반 금지

> 이 프로토콜은 이 스킬의 최우선 규칙이다.
> 아래 규칙을 위반하면 수업이 망가진다.

### 각 블록은 반드시 2턴에 걸쳐 진행한다

```
┌─ Phase A (첫 번째 턴) ──────────────────────────────┐
│ 1. references/에서 해당 블록 파일의 EXPLAIN 섹션을 읽는다    │
│ 2. 기능을 설명한다                                        │
│ 3. references/에서 해당 블록 파일의 EXECUTE 섹션을 읽는다    │
│ 4. "지금 직접 실행해보세요"라고 안내한다                     │
│ 5. ⛔ 여기서 반드시 STOP. 턴을 종료한다.                    │
│                                                          │
│ ❌ 절대 하지 않는 것: 퀴즈 출제, QUIZ 섹션 읽기             │
│ ❌ 절대 하지 않는 것: AskUserQuestion 호출 (Block 6 제외)    │
│ ❌ 절대 하지 않는 것: "실행해봤나요?" 질문                   │
└──────────────────────────────────────────────────────────┘

  ⬇️ 사용자가 돌아와서 "했어", "완료", "다음" 등을 입력한다

┌─ Phase B (두 번째 턴) ──────────────────────────────┐
│ 1. references/에서 해당 블록 파일의 QUIZ 섹션을 읽는다       │
│ 2. AskUserQuestion으로 퀴즈를 출제한다                     │
│ 3. 정답/오답 피드백을 준다                                 │
│ 4. 다음 블록으로 이동할지 AskUserQuestion으로 묻는다         │
│ 5. ⛔ 다음 블록을 시작하면 다시 Phase A부터.                │
└──────────────────────────────────────────────────────────┘
```

### Phase A 종료 시 필수 문구

```
---
👆 위 내용을 직접 실행해보세요.
실행이 끝나면 "완료" 또는 "다음"이라고 입력해주세요.
```

### 공식 문서 URL 출력 (절대 누락 금지)

모든 블록의 Phase A 시작 시, 해당 reference 파일 상단의 `> 공식 문서:` URL을 반드시 출력한다.

---

## 소요 시간

| Block | 주제 | 예상 시간 |
|-------|------|----------|
| 0 | MCP 개념 | ~12분 |
| 1 | MCP 서버 추가 | ~13분 |
| 6 | Connector로 Slack 연결 + 스킬 STUB 채우기 | ~20분 |
| 10 | 전체 실행 & 마무리 | ~15분 |
| **합계** | | **~60분** |

> 원본 Day 2 커리큘럼(11개 블록, ~170분)에서 Heum 3시간 강의용으로 핵심 4개 블록만 엄선.
> 추가 도구 연결(Notion/Linear/Google)은 원본 커리큘럼에서 다룬다.

---

## 핵심 전략

### MCP 개념 이해 → Connector로 첫 연결 → 스킬로 통합

1. **Block 0**: MCP가 왜 필요한지, 어떤 구조인지 이해
2. **Block 1**: 실제로 `claude mcp add`로 서버 하나 추가해보기
3. **Block 6**: Claude.ai Connector로 Slack 연결 → `my-context-sync` 스킬의 Slack 소스 채우기
4. **Block 10**: 병렬 수집 + 출력 포맷 완성 → 실제로 실행해서 결과 확인

> **핵심 메시지**: "정보가 여러 도구에 흩어져 있다. MCP로 모두 연결해서 Claude가 한 번에 읽게 한다."

---

## Block 6 예외 규칙

Block 6의 Phase A는 **AskUserQuestion을 사용**한다. Slack 사용 여부와 연결 가능 여부를 확인해야 한다.

- Slack 사용 시: claude.ai/settings/connectors에서 Slack Connector 연결 → `/mcp` 등록 확인 → 테스트
- 회사 Slack 제한 시: 개인 workspace 또는 공동 세션 workspace 사용

## Block 10 예외 규칙

Block 10의 Phase A는 **AskUserQuestion을 사용**한다. Output format(Slack / Notion / 파일)을 선택한다.

---

## References 파일 맵

| 블록 | 파일 | 주제 |
|------|------|------|
| Block 0 | `references/block0-concept.md` | MCP 개념 이해 |
| Block 1 | `references/block1-add-server.md` | MCP 서버 추가 실습 |
| Block 6 | `references/block6-connector-slack.md` | Connector로 Slack 연결 + 스킬 소스 채우기 |
| Block 10 | `references/block10-finalize.md` | 병렬 수집 + 최종 실행 + 마무리 |

> 각 reference 파일은 `## EXPLAIN`, `## EXECUTE`, `## QUIZ` 섹션으로 구성된다.
> 원본 Day 2에서 block 2~5, 7~9는 제외되었다. 본 강의 후 추가 학습 시 원본 레포 참조.

---

## Templates 파일 맵

| 파일 | 용도 |
|------|------|
| `templates/context-sync.md` | Context Sync 스킬 기본 템플릿 (4개 소스 STUB 포함) |

> Heum 3시간 강의에서는 Slack 소스만 실제로 채운다. 나머지 STUB은 숙제로 남긴다.

---

## 시작

Part 1 시작 시 블록을 선택한다.

```
AskUserQuestion({
  "question": "Part 1: MCP & Context Sync\n\n어디서부터 시작할까요?",
  "header": "시작 블록",
  "options": [
    {"label": "Block 0: MCP 개념", "description": "MCP가 뭔지, 왜 필요한지부터"},
    {"label": "Block 1: 서버 추가", "description": "MCP 개념을 알고 있어서 실습부터"},
    {"label": "Block 6: Slack 연결", "description": "바로 Connector로 Slack 연결"},
    {"label": "Block 10: 전체 실행", "description": "연결은 끝났고 통합 실행만"}
  ],
  "multiSelect": false
})
```

> 공동 세션 강사(심근/문성훈/최의진)와 진행 중 방향이 바뀌면 블록 순서/깊이를 유연하게 조정한다.
