# ZETTY 보안 백엔드

로컬 Docker Compose 환경에서 인증·인가, 접근 회수, 보안 이벤트의 전달·재처리를 검증한다. 현재 구성은 Java 21·RS256·BFF/Auth/API·MySQL·Redis·로컬 KMS·Elasticsearch다.

## 요청과 감사 경로

```text
브라우저 → nginx HTTPS → BFF → Auth / API
Auth/API → MySQL Outbox → Redis Streams → event-indexer → Elasticsearch
```

브라우저에는 세션 쿠키를 주고 AT/RT는 BFF 서버에 보관한다. Auth만 서명 권한을 가진다. API는 서명과 발급·사용자 상태를 확인하고 객체 소유권을 별도로 검사한다.

## 저장소별 책임

| 저장소 | 책임 | 진입점 |
|---|---|---|
| backend | 인증·인가·토큰 발급·회수·BFF | [인증 구조](https://github.com/ZETTY-ZEROTRUST/backend/blob/develop/docs/auth-token-architecture.md) |
| log-pipeline | 이벤트 계약·Outbox·Streams·ES·재처리 | [공통 계약](https://github.com/ZETTY-ZEROTRUST/log-pipeline/blob/develop/contracts/README.md) |
| attack-simulation | 로컬 모의 계정의 공격·정상 대조군 | [시나리오](https://github.com/ZETTY-ZEROTRUST/attack-simulation/blob/develop/README.md) |
| zero-trust-architecture | Compose·TLS·네트워크·실행 복구 | [실행 안내](https://github.com/ZETTY-ZEROTRUST/zero-trust-architecture/blob/develop/compose/README.md) |

링크는 이번 변경을 담은 저장소별 develop 브랜치를 가리킨다.

## 다음 작업

[현재 네 시나리오](https://github.com/ZETTY-ZEROTRUST/attack-simulation/blob/develop/README.md)의 공격·정상 대조군과 필요한 관측을 기준으로 재설계한다. 직접 머신러닝 학습 코드와 과거 평가 자료는 삭제했다. 목표는 backend 보안 이벤트를 log-pipeline에서 집계하고, uba-analyzer의 Jev가 평가·보고서를 작성해 Slack에 알리는 구조다. PostgreSQL 전환과 새 분석·알림 경로는 설계 단계이며 실제 연동·성능 검증 완료를 뜻하지 않는다.

실행은 승인된 로컬 대상과 모의 계정에서 진행한다. 시나리오 초안·mock 결과를 실제 사고 방어 성능이나 AI 탐지 실측으로 표현하지 않는다.
