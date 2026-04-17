---
name: part3-wrap
description: Heum 3시간 강의 Part 3 — Wrap. session-wrap 스킬을 직접 만들고, 만든 스킬을 실행하고, history-insight로 세션을 분석한다. "파트3", "Part 3", "wrap", "세션 래핑", "session wrap" 요청에 사용.
---

# Part 3: Wrap

이 스킬이 호출되면 아래 **STOP PROTOCOL**을 반드시 따른다.

---

## 용어 정리

| 용어 | 설명 |
|------|------|
| **session-wrap** | 코딩 세션이 끝날 때 작업을 정리하고 문서화하는 스킬. "퇴근 전 책상 정리" |
| **multi-agent** | 여러 에이전트가 동시에 일하는 패턴. "회의에서 각 팀장에게 동시에 보고 받기" |
| **병렬(Parallel)** | 여러 작업을 동시에 처리하는 것. 반대는 순차 |
| **2-Phase Pipeline** | 먼저 분석(Phase 1, 병렬) → 다음 검증(Phase 2, 순차) |
| **frontmatter** | 스킬 파일 맨 위에 `---`로 감싸서 적는 "이름표" |
| **history-insight** | 과거 세션 기록을 분석해 인사이트를 추출하는 스킬 |

---

## STOP PROTOCOL — 절대 위반 금지

> 이 프로토콜은 이 스킬의 최우선 규칙이다.

### 각 블록은 반드시 2턴에 걸쳐 진행한다

```
┌─ Phase A (첫 번째 턴) ──────────────────────────────┐
│ 1. references/에서 해당 블록 파일의 EXPLAIN 섹션을 읽는다    │
│ 2. 기능을 설명한다                                        │
│ 3. references/에서 해당 블록 파일의 EXECUTE 섹션을 읽는다    │
│ 4. "지금 직접 실행해보세요"라고 안내한다                     │
│ 5. ⛔ 여기서 반드시 STOP. 턴을 종료한다.                    │
│                                                          │
│ ❌ Phase A에서 AskUserQuestion 호출 금지                    │
│ ❌ Phase A에서 퀴즈 출제 금지                               │
└──────────────────────────────────────────────────────────┘

  ⬇️ 사용자가 "완료" / "다음" 입력

┌─ Phase B (두 번째 턴) ──────────────────────────────┐
│ 1. references/에서 해당 블록 파일의 QUIZ 섹션을 읽는다       │
│ 2. AskUserQuestion으로 퀴즈를 출제한다                     │
│ 3. 정답/오답 피드백을 준다                                 │
│ 4. 다음 블록으로 이동할지 AskUserQuestion으로 묻는다         │
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
|-------|------|-----------|
| 0 | 개념 이해 (multi-agent + session-wrap) | ~10분 |
| 1 | 스킬 만들기 | ~25분 |
| 2 | 실행 & 검증 | ~15분 |
| 3 | History Insight | ~10분 |
| **합계** | | **~60분** |

> 원본 Day 4(6 블록, ~105분)에서 핵심 4 블록 엄선. Session-Analyzer, Content-Digest는 본 강의 범위 외.
> Block 1이 가장 길고 핵심 — 완료 후 "여기까지 잘 따라오셨습니다!" 격려 필요.

---

## 핵심 전략: 원본 스킬을 해체하며 배우기

```
Block 0:  session-wrap 구조 + multi-agent 원리 이해
   ↓
Block 1:  SKILL.md를 Step-by-Step으로 직접 작성 (가장 긴 블록)
   ↓
Block 2:  만든 스킬 실행 → 결과 확인
   ↓
Block 3:  history-insight로 오늘 세션 자체를 분석 (메타 인지)
```

> session-wrap 원본은 플러그인에 설치되어 있다. 참가자는 이를 참고하면서 자기만의 버전을 만든다.

---

## References 파일 맵

| 블록 | 파일 | 주제 |
|------|------|------|
| Block 0 | `references/block0-concept.md` | Multi-agent 패턴 + session-wrap 개념 |
| Block 1 | `references/block1-build-session-wrap.md` | session-wrap 스킬 직접 만들기 |
| Block 2 | `references/block2-run-session-wrap.md` | 만든 스킬 실행 + 검증 |
| Block 3 | `references/block3-history-insight.md` | history-insight 실습 |

> 각 reference 파일은 `## EXPLAIN`, `## EXECUTE`, `## QUIZ` 섹션으로 구성된다.
> 원본 Day 4의 Block 4(Session Analyzer)와 Block 5(Content Digest)는 본 강의에서 제외되었다.

---

## 시작

Part 3 시작 시 블록을 선택한다.

```
AskUserQuestion({
  "question": "Part 3: Wrap\n\n어디서부터 시작할까요?",
  "header": "시작 블록",
  "options": [
    {"label": "Block 0: 개념 이해", "description": "Multi-agent 패턴과 session-wrap 개념부터"},
    {"label": "Block 1: 스킬 만들기", "description": "바로 SKILL.md 작성하기"},
    {"label": "Block 2: 실행 & 검증", "description": "이미 만들었으니 실행만"},
    {"label": "Block 3: History Insight", "description": "세션 히스토리 분석부터"}
  ],
  "multiSelect": false
})
```

> 공동 세션 강사(심근/문성훈/최의진)와 진행 중 방향이 바뀌면 블록 순서/깊이를 유연하게 조정한다.
