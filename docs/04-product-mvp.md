# 제품 MVP: 꿈 아카이브 (Phase 1)

> **지금 만들지 않는다.** Phase 0에서 "어떻게의 밤"이 작동한다는 것이 확인된 뒤에 만든다. (→ D-001)
> 이 문서는 그때 AI들이 바로 작업을 시작할 수 있도록 미리 써 둔 설계 초안이다.

---

## 1. 무엇을 위한 제품인가

오프라인 모임에서 일어나는 일(선언 → 질문 → 도움 → 원정대)을 **모임과 모임 사이에도 이어지게** 만드는 것.
새로운 SNS를 만드는 것이 아니다.

## 2. 설계 원칙

1. **모바일 우선.** 한국 사용자는 대부분 휴대폰으로 들어온다.
2. **비교 장치를 만들지 않는다.** 좋아요 수, 팔로워 수, 인기순 정렬, 랭킹 없음. (→ D-003)
3. **주목받지 못한 꿈을 위로.** 기본 정렬은 "아직 질문이 적은 꿈"이 먼저 보이게 한다.
4. **기여를 눈에 띄게.** 프로필의 중심은 "내 성과"가 아니라 "내가 도운 꿈"이다.
5. **질문은 질문답게.** 꿈 선언에 다는 댓글은 기본적으로 "어떻게?" 질문 형식으로 안내한다.

## 3. 기능 범위

### 꼭 필요한 것 (Must)

| ID | 기능 | 설명 |
| --- | --- | --- |
| M1 | 로그인·프로필 | 카카오 로그인. 프로필 = 이름, 전문 분야(복수), 한 줄 소개, 내가 도울 수 있는 것 |
| M2 | 꿈 선언 | [꿈 선언서](templates/dream-declaration.md) 항목을 그대로 구조화. 공개 범위: 전체 / 회원만 / 비공개 |
| M3 | "어떻게?" 질문 | 꿈 선언에 질문을 남기고, 선언자가 답한다 |
| M4 | 도움 제안·기여 기록 | "나는 ~로 도울 수 있다" 제안 → 선언자가 "실제로 도움 받음" 표시 → 양쪽 프로필에 기록 |
| M5 | 원정대 | 꿈에서 원정대 만들기, 대원 참여, 2주 진척 로그, 90일 보고 |

### 있으면 좋은 것 (Should)

| ID | 기능 | 설명 |
| --- | --- | --- |
| S1 | 전문가 찾기 | 전문 분야로 사람 검색 ("플라즈마 아는 사람?") |
| S2 | 문샷 지도 | 분야별로 꿈과 원정대를 모아 보는 화면 |
| S3 | 모임 관리 | 어떻게의 밤 일정, 신청, 다음 걸음 기록 |

### 만들지 않는 것 (Won't)

- 좋아요·추천 수 공개, 팔로워 수, 순위
- 무한 스크롤 피드, 알고리즘 추천
- 투자·펀딩 기능

## 4. 화면

1. **홈**: 아직 질문이 적은 꿈 / 최근 원정대 진척 / 다가오는 모임
2. **꿈 상세**: 선언 내용 → "어떻게?" 질문과 답 → 도움 제안 → 연결된 원정대
3. **꿈 쓰기**: 선언서 단계별 입력 (한 화면에 한 질문)
4. **원정대 상세**: 헌장 → 진척 로그 타임라인 → 도운 사람들
5. **프로필**: 전문 분야 → 내가 도운 꿈 → 내 꿈 → 참여한 원정대
6. **문샷 지도** (S2)

## 5. 데이터 모델 (초안)

```text
profiles       id, display_name, bio, can_help_with, created_at
expertises     id, profile_id, field                # 한 사람이 여러 분야
dreams         id, author_id, title, success_state, why, frontier, insight,
               bottleneck, first_step, help_needed, visibility, created_at
how_questions  id, dream_id, asker_id, body, answer, answered_at, created_at
help_offers    id, dream_id, helper_id, body, status(offered|accepted|done), created_at
expeditions    id, dream_id, name, goal, frontier_benchmark, starts_on, report_on,
               status(active|reported|closed), report
expedition_members  expedition_id, profile_id, role, weekly_hours
progress_logs  id, expedition_id, author_id, done, blocked, next, created_at
```

기여 기록은 `help_offers.status = done`을 모아서 보여 준다. 별도 점수는 만들지 않는다.

## 6. 기술 스택 (잠정, → D-005)

| 영역 | 선택 | 이유 |
| --- | --- | --- |
| 프레임워크 | Next.js (App Router) + TypeScript | Claude와 Gemini 모두 가장 익숙한 스택, 자료가 많다 |
| 스타일 | Tailwind CSS | AI가 일관되게 다루기 쉽다 |
| DB·인증 | Supabase (Postgres + Auth) | 무료 티어, 카카오 로그인 지원, Row Level Security |
| 배포 | Vercel | 무료 티어, 비공개 저장소 연결 가능 |

비용 목표: 사용자 수백 명까지 **월 0원**.

## 7. 개발 순서 (AI 분담 예시)

| 단계 | 작업 | 담당 제안 |
| --- | --- | --- |
| 1 | 아키텍처·스키마·RLS 정책 확정 | Claude (설계) → 사람 승인 |
| 2 | 프로젝트 뼈대, 로그인, 프로필 (M1) | Gemini (구현) → Claude (리뷰) |
| 3 | 꿈 선언 쓰기·보기 (M2) | Gemini → Claude |
| 4 | 질문·도움 제안·기여 기록 (M3, M4) | Gemini → Claude |
| 5 | 원정대 (M5) | Gemini → Claude |
| 6 | 보안 점검 (RLS, 개인정보) | Claude |
| 7 | 첫 모임 참가자 10명과 사용성 테스트 | 사람 |

작업은 `ai/TASKS.md`에 하나씩 올리고, 협업 규칙은 [`AGENTS.md`](../AGENTS.md)를 따른다.
