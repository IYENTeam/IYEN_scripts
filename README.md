# IYEN Scripts

IYENTeam에서 사용하는 Codex·Claude 공통 문서, 스킬, 검증 도구 모음입니다. GitHub 이슈와 PR을 근거 중심으로 리뷰하고, 스킬 품질과 컨텍스트 비용을 지속적으로 관리하는 데 초점을 둡니다.

## 포함된 도구

- `docs-list.ts` — 문서의 요약과 `read_when` 조건을 한 번에 출력합니다.
- `sync-skills` — 현재 저장소의 스킬을 Codex와 Claude 검색 경로에 안전하게 연결합니다.
- `validate-skills` — 스킬 front matter, 필수 필드, 중복 이름을 검사합니다.
- `test-maintainer-orchestrator-policy` — IYEN 유지보수 정책의 핵심 안전 규칙을 회귀 검사합니다.
- `skill-cleaner` — 중복·저사용 스킬과 설명문 컨텍스트 비용을 분석합니다.
- `github-deep-review` — GitHub 이슈와 PR의 원인, provenance, 최선의 수정과 검증 공백을 분석합니다.
- `maintainer-orchestrator` — IYENTeam 저장소 유지보수를 권한과 증거 중심으로 조율합니다.

## 빠른 시작

요구사항은 Node.js 22.6 이상입니다. GitHub 리뷰에는 인증된 GitHub CLI가 필요합니다.

```bash
node --version
gh auth login

npm run docs:list
npm run skills:validate
npm test
npm run skills:clean
```

스킬을 Codex와 Claude에 연결합니다.

```bash
npm run skills:sync
```

이 명령은 기존 실제 파일이나 전역 `AGENTS.md`를 덮어쓰지 않습니다. 새 세션부터 연결된 스킬이 검색됩니다.

## 사용 예

```text
$github-deep-review https://github.com/IYENTeam/REPOSITORY/pull/123
원인, 회귀 provenance, 수정 위치, 누락된 테스트와 잔여 위험을 분석해줘.
```

```text
$maintainer-orchestrator
IYENTeam의 이 저장소에서 열린 이슈와 PR을 분류하고, 아직 원격 변경은 하지 마.
```

자세한 명령은 [`docs/tooling.md`](docs/tooling.md)를 참고하세요.

## 출처와 라이선스

이 프로젝트는 Peter Steinberger의 [steipete/agent-scripts](https://github.com/steipete/agent-scripts)에서 영감을 받고 일부 MIT 라이선스 코드를 바탕으로 IYENTeam 환경에 맞게 수정했습니다. 원저작권 고지와 변경 내역은 [`LICENSE`](LICENSE)와 [`docs/upstream.md`](docs/upstream.md)에 보존합니다.

