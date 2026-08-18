# Changelog

본 프로젝트는 [Semantic Versioning](https://semver.org/lang/ko/)을 따릅니다.

## [1.0.1] - 2026

### 문서
- SKILL.md에 **STEP 4 — 툴 선택 & 전환 시점(Cowork ↔ Claude Code)** 추가. 케이스별 주 사용 툴, Cowork로 넘어가는 시점, `tokens.md` 기준 핸드오프 규칙 명시.
- README에 "어느 툴로?" 섹션 추가.
- STEP 4 표를 **단계별 툴 + 추천 모델**로 확장 (기본 Sonnet · Opus는 품질/난이도 결정 단계만 · Haiku는 기계적 보조).
- README 설치 안내 명확화: `.claude/skills/dara/`는 **대상 프로젝트 레포**(또는 홈 `~`)에 설치. 전역 설치 옵션 추가, `AGENTS.md` 병합은 Codex용임을 명시.

## [1.0.0] - 2026

### 첫 정식 릴리즈
- 인테이크 플로우(`/dara`): 케이스 A/B/C 선택 + 케이스별 질문 + 반응형·다크모드 확정 → 실행 라우팅.
- 워크플로우 커맨드: extract · plan-review · build · review · learn · apply-legacy + 제작 전/후 공용 rubric.
- 서비스별 디자인 시스템 Skill 템플릿(tokens · components · patterns · dont · preview · component-checklist).
- 스타일 갤러리 통합(5방향 × 2밀도): 실물로 방향 선택 → 토큰 시드 매핑(차트 팔레트 · primary 파생 · 라디우스 스케일 · 라이트/다크 2벌). 정렬 가능한 데이터 테이블 샘플 포함.
- 렌더 라이브러리 기본값: 차트 ECharts · 데이터 테이블 Grid.js.
- Claude Cowork/Code 채팅 UX(클릭형 질문 · 갤러리 자동 렌더) + Codex(`AGENTS.md`) 병행.
