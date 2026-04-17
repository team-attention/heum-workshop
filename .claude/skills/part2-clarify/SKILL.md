---
name: part2-clarify
description: Heum 3시간 강의 Part 2 — Clarify. AskUserQuestion과 Clarify 플러그인으로 모호한 요구사항을 명확하게 만들고, 나만의 Clarify 스킬을 작성한다. "파트2", "Part 2", "clarify", "클래리파이" 요청에 사용.
---

# Part 2: Clarify

이 스킬이 호출되면 아래 **STOP PROTOCOL**을 반드시 따른다.

---

## 용어 정리

| 용어 | 설명 |
|------|------|
| **Clarify** | 모호한 요구사항을 명확하게 만드는 과정. Claude가 질문을 던져서 암묵지를 명시지로 변환한다 |
| **AskUserQuestion** | Claude가 사용자에게 구조화된 질문을 하는 도구. 선택지를 제시하여 인지 부하를 줄인다 |
| **Hypothesis-as-Options** | 열린 질문 대신 가설을 선택지로 제시하는 원칙. "뭘 원해요?" 대신 "A / B / C 중 어떤 건가요?" |
| **Before/After** | Clarify 전후의 요구사항을 비교하여 변화를 시각화하는 포맷 |
| **Plugin** | Skill + MCP + Hook + Agent를 하나의 설치 단위로 묶은 패키지 |

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
│ ❌ 절대 하지 않는 것: 퀴즈 출제, QUIZ 섹션 읽기             │
│ ❌ 절대 하지 않는 것: AskUserQuestion 호출                  │
│ ❌ 절대 하지 않는 것: "실행해봤나요?" 질문                   │
└──────────────────────────────────────────────────────────┘

  ⬇️ 사용자가 돌아와서 "했어", "완료", "다음" 등을 입력한다

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

### 블록 특수 규칙

- **Block 0 (Concept)**: 표준 Phase A/B. AskUserQuestion 체험이 EXECUTE의 핵심.
- **Block 1 (Experience Vague)**: **예외** — Phase A에서 Claude가 clarify-vague 프로토콜을 시연한다. 학생이 모호한 요구사항을 던지면 Claude가 AskUserQuestion으로 clarify한다. 학생은 "clarify 받는 사람" 역할.
- **Block 2 (Build Clarify)**: 표준이지만 EXECUTE에서 `.claude/skills/clarify-vague/SKILL.md`를 Read로 분석한 후, 템플릿 기반으로 나만의 스킬을 작성한다.

---

## 소요 시간

| Block | 주제 | 시간 |
|-------|------|------|
| 0 | Clarify 개념 + AskUserQuestion | ~15분 |
| 1 | clarify-vague 체험 | ~15분 |
| 2 | 나만의 Clarify 스킬 만들기 | ~30분 |
| **합계** | | **~60분** |

> 원본 Day 3(5 블록, ~95분)에서 핵심 3 블록만 엄선. Plugin 심화/Unknown/PRD는 본 강의 범위 외.

---

## 핵심 전략

> **"모호함을 구조화된 질문으로 변환하는 근육 만들기"**

```
Block 0:  AskUserQuestion 체험 → "아, 이렇게 질문하는 거구나"
   ↓
Block 1:  모호한 요청 던져보기 → clarify 플러그인이 어떻게 대응하는지 관찰
   ↓
Block 2:  나만의 Clarify 스킬 작성 → 내 워크플로우에 맞게 커스터마이즈
```

---

## References 파일 맵

| 블록 | 파일 |
|------|------|
| Block 0 | `references/block0-concept.md` |
| Block 1 | `references/block1-experience-vague.md` |
| Block 2 | `references/block2-build-clarify.md` |

> 각 reference 파일은 `## EXPLAIN`, `## EXECUTE`, `## QUIZ` 섹션으로 구성된다.
> 원본 Day 3의 Block 3(Plugin 심화 + Unknown), Block 4(PRD + GitHub)는 본 강의에서 제외되었다.

---

## Templates 파일 맵

| 파일 | 용도 |
|------|------|
| `templates/clarify-vague.md` | 나만의 Clarify 스킬 작성용 템플릿 |

---

## 시작

Part 2 시작 시 블록을 선택한다.

```
AskUserQuestion({
  "question": "Part 2: Clarify\n\n어디서부터 시작할까요?",
  "header": "시작 블록",
  "options": [
    {"label": "Block 0: Concept", "description": "Clarify 개념 + AskUserQuestion 체험"},
    {"label": "Block 1: Experience", "description": "clarify-vague 플러그인 체험"},
    {"label": "Block 2: Build", "description": "나만의 Clarify 스킬 만들기"}
  ],
  "multiSelect": false
})
```

> 공동 세션 강사(심근/문성훈/최의진)와 진행 중 방향이 바뀌면 블록 순서/깊이를 유연하게 조정한다.
