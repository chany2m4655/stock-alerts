# stock-alerts

KOSPI 지수저점 · S엔벨롭 · 테마주/주도주 **알림 실행기** (공개 저장소 → GitHub Actions 무료).
알림·시세 조회 전용이며 **주문 기능은 없습니다.**

- 코드·데이터·상태는 비공개 저장소(`S_envelope`, `theme_stock`)에 그대로 있고,
  이 저장소의 워크플로가 `PRIVATE_REPO_TOKEN` 으로 체크아웃 → 실행 → 상태/데이터를 그 저장소로 다시 커밋합니다.
- 비밀값은 모두 Actions Secrets 에만 둡니다: `PRIVATE_REPO_TOKEN`, `TELEGRAM_TOKEN`, `TELEGRAM_CHAT_ID`,
  `CLOUDFLARE_API_TOKEN`, `CLOUDFLARE_ACCOUNT_ID`.
- 실행은 cron-job.org 가 workflow_dispatch 로 호출합니다 (KST 평일).

| 워크플로 | 대상 | 일정 (cron-job.org) |
|---|---|---|
| `kospi.yml` | S_envelope 코스피 지수저점 감시 | 08–20시 매시 정각(hourly), 09:30(hold), 15:33(hourly) |
| `s_envelope.yml` | S_envelope 장중 갱신·보고 + s-envelope.pages.dev 배포 | 09:05–15:05 매시, 15:38 마감 |
| `theme.yml` | theme_stock 테마주/주도주 갱신·보고 + theme-stock.pages.dev 배포 | 17:25(theme), 20:05(leader) |

시험 실행: `kospi.yml` notify=false (dry-run), `s_envelope.yml` mode=sync, `theme.yml` part=deploy.
