# 작업 보드

- 상태: `todo` → `doing` → `review` → `done` (막히면 `blocked`)
- 담당: `human` / `claude` / `gemini` / `미정`
- 규칙: 자기 작업 블록만 고치고 바로 커밋한다. 새 작업은 맨 아래에 다음 번호로 추가한다. → [AGENTS.md](../AGENTS.md)

---

### T-000 프로젝트 기반 세우기

- 담당: claude · 상태: review · 의존: 없음
- 내용: 선언문, 전략, 공동체 설계, MVP 초안, AI 협업 규칙, 랜딩 페이지
- 수락 기준: 사람이 읽고 방향에 동의한다

### T-001 프로젝트 이름 정하기

- 담당: human · 상태: todo · 의존: 없음
- 내용: 가칭 "원대"를 그대로 쓸지, 새 이름을 정할지 결정한다. 정해지면 `AGENTS.md` 0장, `README.md`, `site/index.html`의 이름을 바꾸는 작업을 gemini에게 준다.
- 수락 기준: `ai/DECISIONS.md` D-004가 `확정`으로 바뀐다

### T-002 창립자 꿈 선언서 쓰기

- 담당: human · 상태: todo · 의존: 없음
- 내용: `docs/templates/dream-declaration.md` 또는 랜딩 페이지 작성기로 나의 꿈(핵융합, 양자 등)을 선언한다. 첫 번째 예시가 된다.
- 수락 기준: `docs/dreams/founder.md`로 저장 (공개 여부는 본인 결정)

### T-003 첫 10명 섭외

- 담당: human · 상태: todo · 의존: T-002
- 내용: 후보 20명을 적고 1:1로 연락한다. 이공계와 다른 분야를 섞는다.
- 수락 기준: 첫 "어떻게의 밤" 참가 확정 8명 이상

### T-004 랜딩 페이지 배포와 참가 신청 연결

- 담당: human (+ gemini 보조) · 상태: todo · 의존: T-001
- 내용: 참가 신청 폼(Google Forms/Tally)을 만들고 `site/index.html` 상단 `CONFIG.joinUrl`에 넣는다. Netlify/Vercel/Cloudflare Pages 중 하나로 `site/` 폴더를 배포한다 (README의 배포 절 참고).
- 수락 기준: 휴대폰에서 공개 주소로 접속해 신청 버튼이 폼으로 연결된다

### T-005 랜딩 페이지 모바일 QA와 공유 미리보기

- 담당: gemini · 상태: todo · 의존: 없음
- 내용: 360px/768px/1280px에서 레이아웃 점검, 카카오톡 공유 시 보이는 미리보기 이미지(`site/og.png`, 1200x630)와 메타 태그 추가
- 수락 기준: 가로 스크롤 없음, 꿈 선언서 작성기의 복사 버튼이 iOS Safari·안드로이드 크롬에서 동작, 카카오톡 링크 미리보기에 제목·설명·이미지가 보임

### T-006 "어떻게의 밤" 인쇄물

- 담당: gemini · 상태: todo · 의존: 없음
- 내용: `docs/03-community-design.md`의 다섯 가지 규칙과 질문 사다리를 A6 카드 인쇄용 HTML(`print/cards.html`)로 만든다
- 수락 기준: 브라우저에서 인쇄하면 A4 한 장에 카드 4장씩, 흑백 인쇄에서도 읽힌다

### T-007 대한민국 문샷 지도 v0 틀

- 담당: claude · 상태: todo · 의존: T-003 (첫 모임 이후가 좋음)
- 내용: `docs/02-strategy.md` 7장의 분야별로 "세계 최전선 / 한국의 위치 / 병목 / 매달린 사람" 틀과 조사 질문을 만든다. 조사 자체는 gemini 작업으로 쪼갠다.
- 수락 기준: `docs/moonshot-map/README.md`와 분야별 빈 틀, gemini 조사 작업이 TASKS에 추가됨

### T-008 MVP 아키텍처 확정

- 담당: claude · 상태: blocked · 의존: Phase 0 졸업 (`docs/02-strategy.md` 4장)
- 내용: `docs/04-product-mvp.md`를 바탕으로 스키마, RLS 정책, 폴더 구조를 확정하고 구현 작업을 gemini용으로 쪼갠다
- 수락 기준: 사람이 승인한 설계 문서와 구현 작업 목록
