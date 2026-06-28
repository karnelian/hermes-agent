# AI Workflows

AI 코딩, Rules MD, 리뷰어 에이전트, 게이트 운영처럼 프로젝트 전반에 반복 적용되는 작업 방식을 모아두는 공통 문서다. 개별 주제가 독립 문서로 흩어지기 전에 먼저 이 파일에 정리하고, 내용이 너무 커지거나 제품 문서로 승격될 때만 별도 문서로 분리한다.

## 문서 운영 규칙

- 공통 AI 작업 방식은 기본적으로 이 파일에 추가한다.
- 게임/웹/앱처럼 프로젝트별로 달라지는 규칙은 이 파일에 원칙과 템플릿만 두고, 실제 프로젝트에는 `docs/rules/` 아래에 별도 Rules MD를 생성한다.
- 하나의 주제가 길어져 독립 문서가 필요해지면 이 파일에는 요약과 링크를 남긴다.
- 리뷰어/구현자/수정자/코디네이터 같은 에이전트 운용 규칙은 이 파일을 기준으로 삼는다.

---

## Agentic Review Gates

AI 코딩에서 실수를 줄이기 위한 리뷰어 에이전트 운영 구조다. 핵심은 리뷰어를 “실수하지 않는 존재”로 믿는 것이 아니라, 구현물이 지나가야 하는 **검문소(gate)** 로 설계하는 것이다.

### 핵심 원칙

```text
메모리/MD = 규칙 저장소
테스트/빌드/lint = 기계적 검문소
리뷰어 에이전트 = 요구사항/규칙/위험 검문소
코디네이터 = 리뷰 결과 통합자
사람 = 수렴 실패 시 최종 판단자
```

리뷰어 에이전트는 품질을 높일 수 있지만, 리뷰어도 실수한다. 따라서 무한 리뷰 루프를 허용하지 않고, 기준·범위·반복 제한·탈출 조건을 명확히 둔다.

---

## 1. Rules MD와 Skill의 차이

```text
Skill
= 반복 가능한 작업 절차 / 에이전트 운용법 / 공통 워크플로우

Rules MD
= 특정 프로젝트에서 절대 어기면 안 되는 계약 / 제약 / 체크 기준
```

Rules MD는 게임, 웹, 앱, 도구, 백엔드 등 프로젝트 성격에 따라 생성되어야 한다.

예시 구조:

```text
/docs/rules/
  PROJECT_RULES.md
  GAME_RULES.md 또는 WEB_RULES.md 또는 APP_RULES.md
  CHECKS.md
  ACCEPTANCE_CRITERIA.md
  RISK_REGISTER.md
```

### PROJECT_RULES.md

- 프로젝트 타입
- 타깃 사용자
- 핵심 경험
- 절대 깨면 안 되는 기능
- 금지된 구현 방식
- 보안/성능/데이터 제약

### CHECKS.md

- 테스트 명령
- lint/typecheck/build 명령
- 수동 확인 항목
- smoke test 항목

### ACCEPTANCE_CRITERIA.md

- 기능 완료 기준
- 실패/예외 케이스 기준
- 릴리즈 가능 조건

---

## 2. 기본 작업 흐름

```text
Feature Request
  ↓
Rules / Acceptance Criteria 생성 또는 갱신
  ↓
Implementer Agent
  ↓
Automated Checks
  - test
  - lint
  - typecheck
  - build
  ↓
Reviewer Agents
  ↓
Review Coordinator
  ↓
PASS? ── yes → Commit / Push
  ↓ no
Fixer Agent
  ↓
Automated Checks
  ↓
Re-review
  ↓
PASS? ── yes → Commit / Push
  ↓ no
Escalate to Human
```

구현자, 리뷰어, 수정자는 역할을 분리한다.

```text
Implementer = 만든다
Reviewer = 의심한다
Coordinator = 리뷰 결과를 정리한다
Fixer = 정리된 must_fix만 고친다
Human = 수렴 실패 시 결정한다
```

---

## 3. 리뷰어 에이전트 역할 분리

리뷰어 여러 명이 모두 “전체 코드 리뷰”를 하면 충돌과 취향 싸움이 늘어난다. 역할별로 좁게 나누는 것이 좋다.

### Spec Reviewer

요구사항 충족 여부만 본다.

- 요청한 기능이 전부 구현됐는가?
- 빠진 조건은 없는가?
- 요청하지 않은 기능을 추가했는가?
- 파일/함수/인터페이스가 계획과 맞는가?

### Rules Reviewer

프로젝트 Rules MD 위반만 본다.

- PROJECT_RULES.md 위반이 있는가?
- GAME_RULES.md / WEB_RULES.md / APP_RULES.md 위반이 있는가?
- 금지된 구현 방식이 사용됐는가?
- 핵심 계약을 깨는가?

### Test Reviewer

테스트 충분성만 본다.

- 새 기능/버그 수정에 대응하는 테스트가 있는가?
- 실패해야 하는 테스트가 먼저 실패했는가?
- edge case 테스트가 있는가?
- 회귀 테스트가 통과했는가?

### Quality / Security Reviewer

코드 품질, 버그, 보안, 데이터 위험을 본다.

- 명백한 런타임 버그가 있는가?
- 예외 처리 누락이 있는가?
- 권한/인증 문제가 있는가?
- 데이터 손상 가능성이 있는가?
- secret, injection, unsafe eval 같은 보안 문제가 있는가?

---

## 4. 리뷰어 입력

리뷰어는 반드시 기준과 증거를 같이 받아야 한다.

```md
너는 독립 리뷰어다.
코드를 수정하지 말고 판정만 내려라.

[원래 요구사항]
...

[PROJECT_RULES.md]
...

[플랫폼별 Rules MD]
...

[ACCEPTANCE_CRITERIA.md]
...

[CHECKS.md]
...

[git diff]
...

[테스트/빌드/lint 결과]
...

판단할 것:
1. 요구사항 누락
2. 요구사항 밖 변경
3. Rules MD 위반
4. 테스트 부족
5. 기존 기능 깨질 위험
6. 보안/권한/데이터 손상 위험
7. PASS 또는 REQUEST_CHANGES
```

---

## 5. Blocking issue와 Suggestion 분리

리뷰어가 모든 의견을 blocking으로 걸면 무한 루프가 생긴다. 반드시 blocking issue와 non-blocking suggestion을 분리한다.

### Blocking issue 조건

아래 중 하나에 해당할 때만 수정 필수로 본다.

1. 요구사항 누락
2. 명시된 Rules MD 위반
3. 테스트/빌드/lint 실패
4. 보안/권한/데이터 손상 위험
5. 기존 public contract 파괴
6. 명백한 런타임 버그
7. 기존 핵심 기능 회귀 가능성이 높음

### Non-blocking suggestion 조건

아래는 기본적으로 참고 의견이다.

- 이름을 더 좋게 바꿀 수 있음
- 구조가 더 예뻐질 수 있음
- 성능을 더 최적화할 수 있음
- 취향에 가까운 리팩토링
- 현재 요구사항 밖의 개선

Fixer는 must_fix만 고치고 non-blocking suggestion은 건드리지 않는다.

---

## 6. 리뷰 결과 포맷

리뷰어 출력은 자유문보다 구조화된 판정표가 좋다.

```json
{
  "verdict": "REQUEST_CHANGES",
  "blocking_issues": [
    {
      "issue": "권한 없는 사용자의 접근 테스트가 없음",
      "basis": "WEB_RULES.md: auth/permission 변경 시 role별 테스트 필요",
      "risk": "high"
    }
  ],
  "non_blocking_suggestions": [
    {
      "issue": "함수명을 더 명확히 할 수 있음",
      "reason": "가독성 제안이며 현재 요구사항을 막지는 않음"
    }
  ],
  "unknowns": [],
  "summary": "권한 테스트가 없어 현재 상태로는 통과 불가"
}
```

---

## 7. Review Coordinator

리뷰어가 여러 명이면 코디네이터가 필요하다. 코디네이터는 코드를 고치지 않고 리뷰 결과만 통합한다.

역할:

- 중복 이슈 병합
- blocking / non-blocking 분리
- 서로 충돌하는 지적 표시
- 기준 문서에 근거 없는 지적 제거
- fixer에게 전달할 최종 수정 목록 생성

코디네이터 출력 예:

```json
{
  "final_verdict": "REQUEST_CHANGES",
  "must_fix": [
    {
      "issue": "권한 없는 사용자의 접근 테스트 추가",
      "source": "Test Reviewer",
      "basis": "WEB_RULES.md",
      "scope": "tests/auth 관련 파일만 수정"
    }
  ],
  "non_blocking": [
    {
      "issue": "함수명 개선 제안",
      "source": "Quality Reviewer",
      "reason": "취향/가독성 제안이므로 blocking 아님"
    }
  ],
  "conflicts": [
    {
      "issue": "API 응답 포맷 변경 여부",
      "resolution": "API_RULES.md의 기존 response shape 변경 금지 규칙을 우선 적용"
    }
  ]
}
```

---

## 8. 리뷰 충돌 해결 우선순위

리뷰어 의견끼리 충돌하면 다수결이 아니라 기준 문서로 판정한다.

우선순위:

```text
1. 명시된 사용자 요구사항
2. PROJECT_RULES.md / 플랫폼별 RULES.md
3. ACCEPTANCE_CRITERIA.md
4. 기존 테스트 / API contract / snapshot
5. 프로젝트 컨벤션
6. 리뷰어 의견
```

리뷰어 의견은 가장 아래다. 기준 문서에 어긋나는 리뷰 의견은 기각한다.

---

## 9. 무한 리뷰 루프 방지 규칙

리뷰 루프는 반드시 bounded revision loop여야 한다.

추천 규칙:

```text
최대 리뷰 라운드: 3회
동일 이슈 반복: 즉시 escalation 가능
이슈 수가 줄지 않음: stall로 보고 escalation
3회 후 blocking issue 남음: 사람에게 보고
```

### Round 1

전체 diff 검토 가능.

### Round 2

이전 must_fix 해결 여부와 수정된 부분 중심으로 검토.

### Round 3

blocking regression만 확인. 새로운 취향/리팩토링 제안 금지.

재리뷰 프롬프트:

```md
이번은 재리뷰다.
새로운 non-blocking suggestion을 만들지 마라.
이전 must_fix가 해결됐는지와, 수정으로 인해 생긴 명백한 blocking regression만 판단하라.
```

---

## 10. Fixer Agent 규칙

Fixer는 리뷰어가 아니다. must_fix만 좁게 고친다.

```md
아래 must_fix만 고쳐라.
non_blocking suggestion은 건드리지 마라.
새로운 리팩토링 금지.
요청된 수정 밖 파일 변경 금지.
수정 후 관련 테스트와 전체 체크를 실행하라.
```

Fixer가 모든 리뷰 의견을 고치려고 하면 새 문제가 생긴다.

```text
Reviewer = 넓게 의심
Coordinator = 좁게 정리
Fixer = 아주 좁게 수정
```

---

## 11. Gate taxonomy

리뷰 시스템은 네 종류의 gate로 나눠 설계한다.

### Pre-flight gate

작업 시작 전 조건 확인.

예:

- 요구사항이 있는가?
- Rules MD가 있는가?
- 테스트 명령이 정의되어 있는가?
- 작업 브랜치가 깨끗한가?

실패 시 작업을 시작하지 않는다.

### Revision gate

산출물 품질을 평가하고 부족하면 수정 루프로 보낸다.

예:

- 리뷰어가 must_fix를 반환
- 테스트가 실패
- acceptance criteria 미충족

최대 반복 횟수를 둔다.

### Escalation gate

자동으로 해결하기 어려운 충돌을 사람에게 올린다.

예:

- 리뷰 3라운드 후에도 수렴 실패
- 리뷰어 의견이 명시 요구사항과 충돌
- 두 설계 모두 합리적이고 선택이 제품 방향을 바꿈

### Abort gate

피해를 막기 위해 작업을 중단한다.

예:

- 승인되지 않은 destructive change 감지
- 민감 정보 노출 감지
- 작업 범위 밖 대규모 파일 변경
- 복구 불가능한 환경 문제

---

## 12. 프로젝트 타입별 리뷰 기준

### Game Reviewer Pack

- core loop를 깨지 않았는가?
- 조작감/카메라/입력에 영향이 있는가?
- 저장 데이터 호환성을 깨지 않았는가?
- 재화 source/sink 변화가 문서화됐는가?
- 목표 FPS나 성능에 영향이 있는가?
- 플레이 테스트 체크가 필요한가?

### Web Reviewer Pack

- API response shape가 바뀌었는가?
- auth/permission이 server-side에서 검증되는가?
- DB schema 변경에 migration이 있는가?
- loading/error/empty state가 있는가?
- 모바일 반응형이 깨질 수 있는가?
- XSS/SQL injection/secret 노출 위험이 있는가?

### App Reviewer Pack

- 권한 거부 상태에서도 앱이 동작하는가?
- 오프라인/네트워크 실패 처리가 있는가?
- 로컬 데이터 migration이 필요한가?
- 업데이트 후 기존 데이터가 유지되는가?
- 앱 시작/종료/뒤로가기 동작이 안전한가?
- 빌드/설치 smoke test가 필요한가?

---

## 13. 최소 운영안

처음부터 복잡하게 만들 필요는 없다. 최소형은 다음과 같다.

```text
1. PROJECT_RULES.md 작성
2. CHECKS.md 작성
3. Implementer가 기능 구현
4. scripts/verify.sh 실행
5. Reviewer가 요구사항 + rules + diff + verify 결과 검토
6. must_fix만 Fixer가 수정
7. 최대 3라운드 후에도 실패하면 사람에게 escalation
```

추천 파일 구조:

```text
/agents/
  implementer.md
  reviewer.md
  coordinator.md
  fixer.md

/docs/rules/
  PROJECT_RULES.md
  GAME_RULES.md 또는 WEB_RULES.md 또는 APP_RULES.md
  CHECKS.md
  ACCEPTANCE_CRITERIA.md
  RISK_REGISTER.md

/scripts/
  verify.sh
```

---

## 14. 한 줄 요약

리뷰어 에이전트를 여러 명 두는 것은 좋다. 하지만 여러 명이 계속 토론하게 두면 안 된다.

```text
리뷰어는 의견 생산자가 아니라 gate다.
게이트는 기준, 범위, 반복 제한, 탈출 조건이 있어야 한다.
```

가장 안전한 형태는 다음과 같다.

```text
Rules MD 기반 기준 설정
→ 구현
→ 자동 체크
→ 역할 분리된 리뷰어
→ 코디네이터 통합
→ must_fix만 수정
→ 제한된 재리뷰
→ 수렴 실패 시 사람에게 escalation
```
