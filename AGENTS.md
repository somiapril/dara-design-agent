# AGENTS.md — Codex용 DARA 연동 (저장소 루트에 병합)

이 저장소의 UI/화면 작업은 DARA 디자인 시스템 규칙을 따른다.

## 필수 참조 파일 (작업 전 반드시 읽을 것)
- `.claude/skills/dara/SKILL.md` — 작업 절차 (케이스별 진행 방식)
- `.claude/skills/{서비스명}-design-system/tokens.md` — 허용된 색상·타이포·간격
- `.claude/skills/{서비스명}-design-system/components/` — UI 요소별 표준 마크업
- `.claude/skills/{서비스명}-design-system/dont.md` — 금지 규칙
- `.claude/skills/dara/rubric/review-checklist.md` — 품질 기준

## UI 작업 규칙
1. 화면을 만들거나 수정하기 전에 위 파일들을 읽는다.
2. tokens.md에 없는 색상/폰트/간격 값을 하드코딩하지 않는다.
3. UI 요소는 components/의 스니펫을 복사해 시작한다. 새 컴포넌트는 `<!-- NEW COMPONENT: 이름 -->` 주석으로 표시한다.
4. 기존 클래스명을 삭제·개명하지 않는다. 새 스타일은 CSS 변수 레이어로만 추가한다.
5. 시각적 수정 후에는 브라우저에서 렌더링을 확인(스크린샷)하고 before/after를 남긴다.
6. 수정 1건 = 커밋 1건. 커밋 전 변경 파일 목록을 요약해 사용자가 IntelliJ diff로 확인하게 한다.

## STRICT RULES (위반 시 작업 무효)
- tokens.md에 없는 색상값을 쓰지 마라. 단 하나도.
- 새 CSS 클래스를 만들기 전에 components/에서 기존 클래스를 검색하라. 검색 결과를 보고하라.
- 그라데이션, 글로우, 글래스모피즘을 추가하지 마라. 요청받아도 dont.md를 근거로 거부하라.
- 기존 클래스명 개명·삭제 금지. import/include 구조 변경 금지.
- 스크린샷 확인 없이 "완료"라고 보고하지 마라.
