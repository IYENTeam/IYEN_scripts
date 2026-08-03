---
summary: 'steipete/agent-scripts에서 가져온 구성과 IYEN판 변경 원칙.'
read_when:
  - upstream 변경을 동기화하거나 라이선스와 출처를 확인할 때.
---
# Upstream adaptation

원본은 <https://github.com/steipete/agent-scripts>이며, 최초 이식 기준은 `c46ea65b6323e8a2b6f441f8b6449ae731bc8f81`입니다.

## 가져온 구성

- 문서 목록 및 스킬 검증 스크립트
- 스킬 동기화 구조
- `skill-cleaner` 분석기와 테스트
- `github-deep-review` 검토 방식
- maintainer 정책 회귀 테스트 패턴

## IYEN판 변경 원칙

- `steipete`, Peter 개인 계정, OpenClaw 운영 인프라를 기본값으로 사용하지 않습니다.
- 기본 GitHub 조직은 `IYENTeam`입니다.
- 저장소 경로를 하드코딩하지 않고 현재 checkout을 기준으로 동작합니다.
- 전역 지침 파일이나 기존 실제 스킬 디렉터리를 덮어쓰지 않습니다.
- URL 공유와 원격 변경 권한을 구분합니다.
- push, comment, merge, release 같은 공개 변경은 사용자 요청 범위 안에서만 수행합니다.
- 검증 결과와 원격 상태를 확인한 뒤 완료로 보고합니다.

upstream을 갱신할 때는 파일 전체를 덮어쓰지 말고 관련 변경을 검토하여 위 원칙을 유지합니다.

