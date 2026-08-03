# IYEN Scripts

IYENTeam용 Codex·Claude 공통 스킬과 검증 도구입니다. [`steipete/agent-scripts`](https://github.com/steipete/agent-scripts)의 운영 원칙을 유지하면서 개인 계정·호스트·OpenClaw 전용 경로만 제거했습니다.

## 도구

- `docs-list.ts`: 문서 요약과 읽을 시점 출력
- `sync-skills`: Codex·Claude 스킬 링크 동기화
- `validate-skills`: 스킬 메타데이터 검사
- `skill-cleaner`: 중복·사용량·컨텍스트 비용 분석
- `github-deep-review`: 원인·provenance·최선의 수정·검증 공백 중심 PR/이슈 리뷰
- `maintainer-orchestrator`: 작업 보존, 단일 저장소 소유권, live proof, CI, dependency, release 게이트

## 사용

```bash
npm run docs:list
npm run skills:validate
npm test
npm run skills:clean
npm run skills:sync
```

Node.js 22.6 이상이 필요하며 GitHub 작업에는 인증된 `gh`가 필요합니다. 자세한 명령은 [`docs/tooling.md`](docs/tooling.md)를 참고하세요.

MIT License. 원저작권 고지는 [`LICENSE`](LICENSE)에 보존되어 있습니다.

