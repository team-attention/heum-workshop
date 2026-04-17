# Heum 3시간 강의 — Claude Code 실전 (Sync / Clarify / Wrap)

> **AI Native Camp Camp-2(7일 커리큘럼)를 증류(distill)하여 3시간에 압축**한 Heum Labs 공동 세션용 레포.
>
> 원본 커리큘럼은 22블록 / 총 ~8시간 분량이며, 본 레포는 핵심 3종(sync/clarify/wrap)과 선택적 Extra 블록으로 축약했다.
>
> - 🌐 AI Native Camp 공식 사이트: https://ainativecamp-production.up.railway.app/
> - 💻 원본 Camp-2 커리큘럼 (GitHub): https://github.com/ai-native-camp/camp-2

## 강의 구성

| Part | 주제 | 소요 | 핵심 개념 |
|------|------|------|----------|
| Part 1 | **Sync** — MCP & Context Sync | ~60분 | MCP 개념, Connector, 스킬로 정보 통합 |
| Part 2 | **Clarify** — 모호함을 구조화 | ~60분 | AskUserQuestion, Hypothesis-as-Options, 나만의 Clarify 스킬 |
| Part 3 | **Wrap** — Multi-agent 세션 정리 | ~60분 | session-wrap 스킬 직접 작성, history-insight |
| Part Extra | Agent Teams / Hook / Plugin | 선택 | 시간이 남거나 질문이 나올 때 선택적으로 다룸 |

각 Part는 Phase A(설명+실행 안내 → Stop) → Phase B(퀴즈+피드백)의 **2턴 진행 프로토콜**로 운영된다. 자세한 내용은 각 스킬의 `SKILL.md` 참조.

## 공동 세션 안내

이번 세션은 Heum Labs 참가자 대표 3분과의 **공동 진행**으로 구성된다. 아래 세 분의 배경과 관심사를 기반으로 사전 커리큘럼 방향을 잡았지만, **강의 중 실제 수준과 관심사에 따라 방향을 유연하게 조정**한다.

| 공동 진행자 | 배경 | 사전 역량 / 관심 |
|-------------|------|-----------------|
| **심근** (운영 조율) | 비개발자 (인사), 업무 자동화 관심 | Python 기본, n8n, Claude Code로 단순 업무 자동화. 스크래핑 → Slack 공유 수준 |
| **문성훈** ("AI 용사") | 비개발자, 바이브코딩으로 프로덕트 빌드 | Claude Max, 스킬 직접 제작, 에이전트 군단, Figma MCP, GitHub Actions 배포 경험. 하네스/Ralph/OpenClaude 학습 중 |
| **최의진** ("초보자") | Tax Sales CSM/CX/AM, 비개발자 | 기획/문서 제작에 AI 활용, API 개념 이해 수준. Claude Code 첫 설치 예정. 목표: 고객 이탈 방지 체계(감지-판단-공유) 방향성 |

### 유연한 방향 조정

진행 중 다음 상황이 발생하면 **커리큘럼 순서/깊이를 즉시 조정**한다:

- **문성훈** 수준에서는 Part 1의 Block 0~1(MCP 개념/기본) 빠르게 넘기고 Block 6/10 심화 또는 Part Extra(Plugin 제작)로 우회
- **최의진** 수준에서는 Part 1 Block 0에서 충분히 체험 시간 확보, 필요 시 Part 2/3 중 하나 skip하고 이탈 방지 use case 실습으로 전환
- **심근** 질문이 "n8n vs Claude Code" 같은 비교 프레임으로 흐르면 Part Extra의 Hook/Agent Teams로 자연 연결

> 커리큘럼은 **뼈대**이고 공동 세션은 **살**이다. 참가자 눈빛이 바뀌는 순간을 따라간다.

## 설치

```bash
# 1. 이 레포를 clone한 프로젝트에서 실행
# 2. .claude/skills/ 아래 스킬이 자동 인식된다
# 3. Claude Code에서 "part1" 또는 "sync" 등으로 스킬 호출

# 기반이 되는 원본 커리큘럼(선택)
npx skills add ai-native-camp/camp-2
```

## 디렉토리 구조

```
heum-3h/
├── README.md                     # 본 문서
├── .gitignore
└── .claude/
    └── skills/
        ├── part1-sync/           # Part 1: MCP & Context Sync
        │   ├── SKILL.md
        │   ├── references/       # block 0, 1, 6, 10 (원본 Day 2에서 엄선)
        │   └── templates/
        ├── part2-clarify/        # Part 2: Clarify
        │   ├── SKILL.md
        │   ├── references/       # block 0, 1, 2 (원본 Day 3에서 엄선)
        │   └── templates/
        ├── part3-wrap/           # Part 3: Wrap
        │   ├── SKILL.md
        │   └── references/       # block 0, 1, 2, 3 (원본 Day 4에서 엄선)
        └── part-extra/           # Agent Teams / Hook / Plugin (선택)
            ├── SKILL.md
            └── references/       # block 3-5, 3-6, 3-7 (원본 Day 1에서 엄선)
```

## 원본 커리큘럼 출처 (Distillation Source)

본 3시간 강의는 **AI Native Camp Camp-2의 7일 커리큘럼을 증류(distill)**하여 핵심 블록만 엄선한 축약판이다.

- 🌐 AI Native Camp 공식 사이트: https://ainativecamp-production.up.railway.app/
- 💻 원본 Camp-2 GitHub: https://github.com/ai-native-camp/camp-2
- 로컬 참조 경로: `business/partners/delta/ai-native-camp/headquarters/camp-2/`

### 증류 매핑

| 본 레포 | ← 원본 Camp-2 | 축약 비율 |
|---------|---------------|----------|
| Part 1 (sync) | Day 2 — MCP & Context Sync | 11블록 → **4블록** |
| Part 2 (clarify) | Day 3 — Clarify & GitHub | 5블록 → **3블록** |
| Part 3 (wrap) | Day 4 — Wrap & Analyze | 6블록 → **4블록** |
| Part Extra | Day 1 — Onboarding (Agent Teams / Hook / Plugin) | 7블록 → **3블록** |

> 전체 커리큘럼(7일) 이수를 원하는 참가자는 원본 Camp-2 GitHub 레포에서 설치 가능:
> ```bash
> npx skills add ai-native-camp/camp-2
> ```

## Claude Code 사용 안내

강의 중 다음 명령어로 각 Part를 시작한다:

```
/part1  또는  "Part 1 시작"    → part1-sync 스킬 호출
/part2  또는  "Part 2 시작"    → part2-clarify 스킬 호출
/part3  또는  "Part 3 시작"    → part3-wrap 스킬 호출
"Part Extra"  또는  "Plugin"   → part-extra 스킬 호출
```

각 Part 시작 시 `AskUserQuestion`으로 시작할 블록을 선택할 수 있다.
