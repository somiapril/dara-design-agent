<!-- 이 파일은 서비스 디자인 시스템 Skill의 SKILL.md 템플릿이다. 생성 시 파일명을 SKILL.md로 저장한다. (DARA 패키지 안에서는 스킬 SKILL.md 중복을 피하려고 .template.md로 둔다.) -->
---
name: {서비스명}-design-system
description: {서비스명}의 디자인 시스템. 이 서비스의 화면을 만들거나 수정할 때 반드시 로드한다.
---

# {서비스명} 디자인 시스템

> 이 파일은 템플릿입니다. /dara-extract 결과 또는 기존 가이드로 {중괄호} 부분을 채우세요.

## 서비스 개요
- 목적: {예: 사내 배치 작업 모니터링}
- 사용자: {예: 운영팀 개발자, 하루 수십 회 접속}
- 톤앤매너: {예: 데이터 중심, 밀도 높음, 차분한 신뢰감}

## 기술 스택
- 템플릿: {예: JSP + 공통 include(header.jsp, footer.jsp)}
- 스타일: {예: /css/common.css + 화면별 CSS, CSS 변수 레이어는 /css/tokens.css}
- 스크립트: {예: jQuery 3.x}
- 컴포넌트 프리뷰: {예: preview.html (SSR — 실제 공통 CSS 링크) / React면 앱 내 /_design/preview 라우트 / Storybook 사용 시 해당 스토리}

## 사용 규칙 (에이전트 필독)
1. 모든 색상·폰트·간격은 [tokens.md](tokens.md)의 값만 사용한다.
2. UI 요소는 [components/](components/)의 스니펫을 복사해 시작한다. 없는 요소만 신규 제작하고 NEW COMPONENT로 표시한다. 표준 컴포넌트 커버리지는 [component-checklist.md](component-checklist.md)로 점검한다.
3. 화면 레이아웃은 [patterns.md](patterns.md)의 패턴 중에서 고른다.
4. [dont.md](dont.md)의 금지 규칙을 위반하지 않는다.
5. 기존 클래스명을 삭제·개명하지 않는다.
6. 컴포넌트를 눈으로 확인할 때는 프리뷰(위 "컴포넌트 프리뷰" 항목)를 연다. 컴포넌트를 추가·변경하면 프리뷰도 함께 갱신한다.
