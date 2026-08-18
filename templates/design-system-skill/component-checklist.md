# 기본 컴포넌트 체크리스트

> 디자인 시스템이 갖춰야 할 표준 컴포넌트 목록.
> - **Case B(추출)**: `/dara-extract` 시 "이 컴포넌트가 코드에 있나?"를 점검하는 체크표로 사용. 없거나 변형이 난립하면 정규화 대상.
> - **Case A(신규)**: "무엇을 만들어야 하나"의 로드맵. Tier 1부터 채운다.
> - **Case C(보유)**: 시스템에 이미 있는 것을 확인하고, 부족분은 rules(공유 자산 절차)로 추가 제안.
>
> 각 컴포넌트는 확정 시 `components/*.md`에 실제 마크업 스니펫과 상태(hover/disabled/focus)를 기록한다.
> 화면 성격(밀도 프리셋 Comfortable/Compact)에 따라 크기는 tokens.md를 따른다.

## Tier 1 — 거의 모든 화면에 필요 (최우선)

| 컴포넌트 | 포함 상태·변형 | 비고 |
|---|---|---|
| **Button** | primary / secondary / ghost·text / danger · hover/active/disabled/loading · size(sm/md) | 표준 1계열로 통일 (변형 난립 금지) |
| **Text input** | 기본 / 포커스 / 에러 / disabled / placeholder / with label | 필수 표시(*) 규칙 포함 |
| **Select / Dropdown** | 단일·다중 · 검색형 | 라이브러리 사용 시 스타일 래핑 |
| **Checkbox / Radio** | 기본 / 체크 / disabled | |
| **Toggle / Switch** | on/off · disabled | |
| **Label / Form field** | 레이블 + 입력 + 도움말/에러 메시지 묶음 | 폼의 최소 단위 |
| **Table** | 헤더 / 행 / 정렬 / 빈 상태 / 페이지네이션 | 데이터 화면 핵심 · **기본 Grid.js**(경량·정렬) — 아래 참조 |
| **Badge / Tag / Chip** | 상태색(성공/경고/위험/정보/중립) | 상태 표현 표준 |
| **Card / Panel** | 헤더 + 바디 + (푸터) · 보더/섀도 규칙 | 컨테이너 기본 |
| **Icon** | 세트·크기·stroke 규칙 (기본 Tabler 1.5) | tokens.md 참조 |

## Tier 2 — 대부분의 서비스에 필요

| 컴포넌트 | 포함 상태·변형 |
|---|---|
| **Tabs** | 기본 / 활성 · 하위 라우팅 |
| **Modal / Dialog** | 확인·경고·폼 모달 · close/scrim 종료 |
| **Toast / Snackbar** | 성공/에러/정보 · 자동 소멸 |
| **Tooltip / Popover** | hover·click |
| **Pagination** | 이전/다음 · 페이지 번호 · 페이지 크기 |
| **Breadcrumb** | 경로 표시 |
| **Empty / Loading / Error state** | 3상태 플레이스홀더 (스켈레톤·스피너·재시도) |
| **Alert / Inline message** | 배너형 안내·경고 |
| **Avatar** | 이미지·이니셜 · 크기 |
| **Progress** | 바 / 원형 · 퍼센트 |

## Tier 3 — 화면 유형에 따라 (대시보드·복잡 화면)

| 컴포넌트 | 비고 |
|---|---|
| **Stat / Metric card** | 지표 + 추세 + 뱃지 (대시보드 필수) |
| **Chart** | 라인·바·파이·게이지 (프리셋/래퍼로 표준화) · **기본 ECharts** — 아래 참조 |
| **Date / Date-range picker** | |
| **Filter bar** | 조회 화면의 검색·필터 묶음 |
| **Stepper** | 단계형 폼·마법사 |
| **Drawer / Side panel** | 상세·설정 슬라이드 |
| **Accordion / Collapse** | 접기·펼치기 |
| **Segmented control** | 뷰 전환(그래프/테이블 등) |

## 렌더 라이브러리 기본값 (차트·테이블)

DARA는 추출 우선이라 **B·C(기존 코드/시스템 보유)는 이미 쓰는 라이브러리를 그대로 따른다.** 새로 골라야 하는 **Case A(신규 플랫폼)** 나 기존에 없던 경우의 **권장 기본**:

- **차트 = ECharts** — 색은 `tokens.md`의 차트 팔레트(`--chart-*`) 토큰으로 통일.
- **데이터 테이블 = Grid.js** — 경량·zero-dependency, 정렬/검색/페이지네이션 내장, React/Vue/바닐라 공용.
  - 서버렌더(JSP/Jinja/PHP 등) **기존 `<table>` 마크업을 유지한 채 강화**만 할 땐 **Simple-Datatables**(정렬·검색, 진행적 향상)가 더 맞는다.
- 어떤 라이브러리를 쓰든 **시각(색·헤더·행·정렬 캐럿·패딩·라디우스)은 tokens/컴포넌트 표준을 따른다** — `dara/style-gallery.html`의 데이터 테이블 샘플이 그 시각 기준이다.
- 주의: 위는 **권장 기본**일 뿐, 실제 도입은 `dont.md` 규칙대로 **사용자 승인 후** 추가한다(임의 CDN·의존성 추가 금지).

## 사용 지침
- **Tier 1은 어떤 서비스든 사실상 필수** — Case A/B에서 최소 이 10개는 확보한다.
- 여기 없는 패턴이 필요하면 신규 컴포넌트로 만들되 `<!-- NEW COMPONENT -->` 표시 후 `/dara-learn`으로 등록.
- 같은 역할의 컴포넌트를 여러 변형으로 만들지 말 것 — 하나로 통일하고 수식자(variant)로 확장.
