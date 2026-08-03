# Loop Engineering Agent Toolkit

Codex와 Claude에서 함께 사용할 문서·스킬 관리 도구와 GitHub 리뷰 워크플로입니다.

## Quick start

```bash
npm run docs:list
npm run skills:validate
npm test
npm run skills:clean
```

스킬을 사용자 디렉터리에 연결하려면 다음을 실행합니다.

```bash
npm run skills:sync
```

이 명령은 현재 저장소의 `skills/`만 연결하며 전역 `AGENTS.md`나 기존 실제 파일을 덮어쓰지 않습니다. 자세한 내용은 `docs/tooling.md`를 참고하세요.

## Included skills

- `github-deep-review`: GitHub 이슈와 PR을 코드 경로, 원인, provenance, 테스트 증거 중심으로 리뷰합니다.
- `skill-cleaner`: 중복·저사용 스킬과 설명문 컨텍스트 비용을 분석합니다.
- `maintainer-orchestrator`: 저장소별 작업 소유권과 공개 변경 게이트를 정의합니다.

Upstream: <https://github.com/steipete/agent-scripts>

