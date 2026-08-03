---
summary: '문서 목록, 스킬 동기화·검증·정리, GitHub 딥 리뷰 사용법.'
read_when:
  - 문서 또는 스킬을 추가하거나 정리할 때.
  - GitHub 이슈나 PR을 근거 중심으로 깊게 리뷰할 때.
---
# Agent tooling

## 문서 목록

```bash
npm run docs:list
```

`docs/**/*.md`의 front matter에서 `summary`와 `read_when`을 읽어 문서와 적절한 열람 시점을 출력합니다. `archive`와 `research` 디렉터리는 제외합니다.

## 스킬 동기화

```bash
npm run skills:sync
```

Codex에는 저장소의 `skills/` 전체를 하나의 링크로, Claude에는 각 스킬을 평탄화한 링크로 연결합니다. 기존 실제 파일이나 링크 자체인 스킬 루트는 건드리지 않습니다.

필요하면 설치 위치를 재정의할 수 있습니다.

```bash
CODEX_SKILLS_ROOT=/custom/codex/skills \
CLAUDE_SKILLS_ROOT=/custom/claude/skills \
npm run skills:sync
```

## 스킬 검증과 정리

```bash
npm run skills:validate
npm run skills:clean
npm run test:skill-cleaner
npm run test:orchestrator-policy
```

- `skills:validate`: 모든 `skills/*/SKILL.md`의 YAML, 이름, 설명과 중복 이름을 검사합니다.
- `skills:clean`: 현재 저장소의 스킬만 대상으로 설명 길이, 중복 이름·본문, 컨텍스트 예산을 분석합니다. 삭제는 하지 않습니다.
- `test:skill-cleaner`: 스킬 발견, 로그 증거 파싱, 설명 압축을 테스트합니다.
- `test:orchestrator-policy`: 오케스트레이터가 저장소별 단일 작업 소유권과 지원 전용 하위 에이전트 원칙을 유지하는지 검사합니다.

전역 Codex 스킬까지 분석하려면 직접 실행합니다.

```bash
node --experimental-strip-types \
  skills/skill-cleaner/scripts/skill-cleaner.ts
```

## GitHub deep review

먼저 GitHub CLI를 인증합니다.

```bash
gh auth login
```

스킬 동기화 후 새 Codex 세션에서 다음처럼 요청합니다.

```text
$github-deep-review https://github.com/OWNER/REPO/pull/123
원인, 회귀 provenance, 수정 위치, 누락된 테스트와 잔여 위험을 분석해줘.
```

이 스킬은 요청받지 않는 한 comment, approve, close, merge 또는 push하지 않습니다.

