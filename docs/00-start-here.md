# 창립자 사용 설명서 (개발 몰라도 됩니다)

창립자가 할 일은 세 가지뿐이다. **말하기, 결정하기, 초록 버튼 누르기.**
코드, 배포, 파일 정리는 AI가 한다. 막히면 Claude에게 "무엇이 잘못됐는지 확인하고 고쳐 줘"라고 말하면 된다.

---

## 1. 처음 한 번 설정 (5분)

GitHub 웹사이트(github.com)에서 이 저장소(`jeondusan-cloud/quant`)를 열고 순서대로 누른다.
화면 문구는 영어다. 아래 따옴표 안의 글자를 찾아 누르면 된다.

### ① 저장소 공개로 바꾸기

1. 저장소 위쪽 메뉴의 **"Settings"** (톱니바퀴)
2. 왼쪽 메뉴 **"General"** → 페이지 맨 아래 빨간 상자 **"Danger Zone"**
3. **"Change visibility"** → **"Change to public"** → 안내에 따라 확인

공개하면 누구나 이 저장소의 문서를 볼 수 있다. 선언문과 전략을 공개하는 것은 "선언하라"와도 맞다.
단, **다른 사람의 개인정보(연락처, 비공개 꿈 선언서 등)는 절대 저장소에 올리지 않는다.**

### ② 기본 브랜치를 main으로 바꾸기

"브랜치"는 작업본이다. `main`이 정식본이고, AI들은 각자의 작업본에서 일한 뒤 정식본에 합친다.

1. **"Settings"** → **"General"** → **"Default branch"** 칸
2. 오른쪽의 화살표 두 개 모양 버튼(⇄) → **main** 선택 → **"Update"** → 확인

### ③ 웹사이트 켜기

1. **"Settings"** → 왼쪽 메뉴 **"Pages"**
2. **"Build and deployment"** 아래 **"Source"** 를 **"GitHub Actions"** 로 선택
3. 위쪽 메뉴 **"Actions"** → 왼쪽 **"사이트 배포"** → 오른쪽 **"Run workflow"** → 초록 **"Run workflow"**
4. 1~2분 뒤 초록 체크가 뜨면 완료. 주소: **https://jeondusan-cloud.github.io/quant/**

이후에는 `site/` 폴더가 바뀌어 `main`에 합쳐질 때마다 웹사이트가 자동으로 갱신된다.
(이름이 정해져서 저장소 이름을 바꾸면 주소도 바뀐다. 그때는 Claude에게 맡기면 된다.)

## 2. Claude에게 일 시키기

1. **claude.ai/code** 에서 저장소 `jeondusan-cloud/quant`를 골라 새 세션을 연다.
2. [`ai/PROMPTS.md`](../ai/PROMPTS.md)의 1번 프롬프트를 붙여 넣고 `T-___`에 작업 번호를 적는다.
3. 그냥 하고 싶은 말을 해도 된다. Claude가 규칙(`AGENTS.md`)에 맞게 정리한다.

Claude는 사용량이 적으니 **생각이 많이 필요한 일**(설계, 전략, 검토)에 쓴다.

## 3. Gemini(Antigravity)에게 일 시키기

1. Antigravity를 열고 에이전트 창에 [`ai/PROMPTS.md`](../ai/PROMPTS.md)의 **0번 프롬프트**(처음 한 번 설정)를 붙여 넣는다. 저장소를 내려받고 GitHub 로그인하는 과정을 에이전트가 한 단계씩 안내한다.
2. 그다음부터는 1번 프롬프트로 작업을 시킨다.

Gemini는 사용량 여유가 있으니 **분량이 많은 일**(화면 만들기, 자료 조사, 반복 작업)에 쓴다.

## 4. 초록 버튼: 작업 합치기 (Pull Request 병합)

AI가 작업을 끝내면 "Pull Request(PR)"라는 합치기 요청이 생긴다.

1. 저장소 위쪽 메뉴 **"Pull requests"** → 요청 하나를 연다.
2. 다른 AI의 리뷰가 "통과"인지 확인한다 (PR 댓글 또는 `ai/reviews/` 파일).
3. 초록 **"Merge pull request"** → **"Confirm merge"**

PR이 없고 브랜치만 있다는 안내를 받으면: 저장소 첫 화면에 뜨는 노란 띠의 초록 **"Compare & pull request"** → **"Create pull request"** 를 누르면 PR이 생긴다.

## 5. 하지 말아야 할 것

- 비밀번호, API 키, 다른 사람의 연락처를 채팅이나 저장소에 붙여 넣지 않는다.
- Settings의 모르는 버튼(특히 "Danger Zone")을 누르기 전에 Claude에게 먼저 묻는다.
- AI가 돈이 드는 서비스 가입을 권하면 바로 하지 말고 이유를 다시 물어본다.
