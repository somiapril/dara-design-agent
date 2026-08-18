# DARA — Design Automation & Refinement Agent

> 디자이너 없이도, **기존 코드를 깨지 않고**, 일관된 화면을 설계·개선·퍼블리싱하는 Claude 스킬.
> A Claude skill that turns your existing UI code into a reusable design system, then designs and refines screens on top of it — no designer required.

DARA는 "챗봇 하나"가 아니라 **디자인 시스템 스킬(지식) + 워크플로우 커맨드(행동)** 의 묶음입니다. 전부 마크다운/HTML 기반이라 Claude 앱(Cowork)·Claude Code·Codex 어디서든 같은 자산을 재사용합니다.

**핵심 원칙 — 추출 우선(Extract-first):** 디자인 시스템을 새로 발명하지 않고 **기존 코드에서 추출·문서화**한 뒤 그 위에서 점진 개선합니다.

## 빠른 시작 (Claude Cowork/Code)

설치 후엔 프롬프트가 필요 없습니다. `/dara`를 치거나 *"새 대시보드 화면 만들래"* 처럼 하고 싶은 걸 말하면, DARA가 **인테이크(클릭형 질문) → 스타일 갤러리(채팅에 렌더) → 목업 → 토큰 시드**까지 이끕니다.

## 설치

> **중요:** 이 저장소(`dara-design-agent`)는 스킬의 **원본 창고**입니다. DARA를 실제로 쓰려면 이 파일들을 **DARA로 작업할 대상(당신의 서비스 코드베이스) 프로젝트**에 설치합니다. 이 저장소 자체를 고치는 게 아닙니다.

**A. Claude Cowork:**
[Releases](../../releases)에서 `dara.skill`을 내려받아 스킬로 저장 → 이후 아무 대화에서 `/dara`.

**B. Claude Code — 특정 프로젝트에만:**
DARA로 작업할 **대상 프로젝트 레포 루트**에 `.claude/skills/dara/`를 만들고 이 파일들을 복사합니다.
```bash
# 예: 대상 프로젝트가 ~/IdeaProjects/my-service 인 경우
mkdir -p ~/IdeaProjects/my-service/.claude/skills/dara
rsync -a --exclude '.git' <이_저장소>/ ~/IdeaProjects/my-service/.claude/skills/dara/
# 결과: my-service/.claude/skills/dara/SKILL.md ...
```
그 프로젝트에서 Claude Code를 켜면 `/dara`가 인식됩니다.

**C. Claude Code — 내 모든 프로젝트에서:**
프로젝트별 대신 **개인 전역 위치** `~/.claude/skills/dara/`에 두면 어느 레포에서든 `/dara`가 뜹니다.
```bash
mkdir -p ~/.claude/skills/dara
rsync -a --exclude '.git' <이_저장소>/ ~/.claude/skills/dara/
```

**D. Codex (GPT) — 선택:**
Codex도 같이 쓸 때만, **대상 프로젝트 레포 루트의 `AGENTS.md`**(스킬 폴더 안이 아님)에 이 저장소의 `AGENTS.md` 내용을 병합합니다. 순수 Claude Code/Cowork만 쓰면 이 단계는 불필요합니다.

> 요약: `.claude/skills/dara/`의 `.claude`는 **"고칠 서비스 프로젝트"의 루트**(또는 홈 `~`)에 생깁니다. 스킬 자동 로드·화면 렌더는 Claude 쪽이 가장 매끄럽습니다.

## 3가지 케이스

| Case | 상황 | 경로 |
|---|---|---|
| **A** | 완전히 새로운 플랫폼 (기존 코드 없음) | 스타일 갤러리로 방향 선택 → 목업 → 토큰 시드 |
| **B** | 운영 중 + 디자인 시스템 없음 (레거시) | `/dara-extract` 추출 → 정규화 → 자산화 → 개선 |
| **C** | 디자인 시스템 보유 + 신규 화면 | 시스템 로드 → plan-review → build → review → learn |

## 어느 툴로? (Cowork ↔ Claude Code)

원칙 — **방향 고르고 시안 만드는 단계 = Cowork, 실제 코드 만지고 커밋하는 단계 = Claude Code.** 세션은 이어지지 않아도 결정이 **`tokens.md`·Skill·목업 파일**에 남아 파일로 이어집니다(단일 진실의 원천 = `tokens.md`).

| Case | 단계 | 툴 | 추천 모델 |
|---|---|---|---|
| **A 신규** | 인테이크 · 갤러리 방향 선택 | Cowork | Sonnet |
| | 핵심 화면 목업 | Cowork | Sonnet (최종 품질 결정 시 Opus) |
| | 토큰 시드 | Cowork | Sonnet (기계적이면 Haiku) |
| | 앱 구현 | Code | Sonnet (복잡 아키텍처 Opus) |
| **B 레거시** | (선택) 리스타일 방향 | Cowork | Sonnet |
| | 추출·정규화 `dara-extract` | Code | Sonnet (대형·난전 Opus) |
| | 오버레이 적용 `dara-apply-legacy` | Code | Sonnet (specificity/hover 디버깅만 Opus) |
| | 리뷰 `dara-review` | Code | Sonnet (고위험 최종 Opus) |
| **C 시스템+신규** | plan-review · build · review | Code | Sonnet (복잡 화면·최종 리뷰만 Opus) |

모델 원칙: 기본 **Sonnet**, **Opus는 품질·난이도가 결정적인 단계만**, **Haiku는 기계적 보조만**.

- 정리/비일관성 수정만이면(새 룩 아님) 툴 전환 없이 **Code만**.
- Cowork 산출물(`tokens.md`·목업)은 **대상 레포에 저장** → 시안 확정 후 Code에서 오버레이 적용(B: `dara-apply-legacy`) → 검증 → 커밋.
- 세션 기억은 자동 동기화되지 않음 — 방향이 바뀌면 `tokens.md`부터 갱신.

## 구성

```
dara/
├── SKILL.md                       # /dara 진입점 — 케이스 선택 + 인테이크
├── commands/
│   ├── dara-extract.md            # 코드베이스 → 디자인 시스템 추출
│   ├── dara-plan-review.md        # 제작 전 계획 리뷰 (0–10 채점)
│   ├── dara-build.md              # 화면 설계·퍼블리싱
│   ├── dara-review.md             # 제작 후 감사 (스크린샷 + before/after)
│   ├── dara-learn.md              # 검증된 패턴을 시스템에 환류
│   └── dara-apply-legacy.md       # 레거시 적용 함정·검증 기법
├── rubric/review-checklist.md     # 제작 전/후 공용 채점 기준
├── style-gallery.html             # 스타일 방향 선택 갤러리 (5방향 × 2밀도)
├── templates/design-system-skill/ # 서비스별 디자인 시스템 Skill 템플릿
│   ├── SKILL.template.md          # (생성 시 SKILL.md로 저장)
│   ├── tokens.md · component-checklist.md · patterns.md · dont.md · preview.html
│   └── components/button.md
└── AGENTS.md                      # Codex 연동용
```

## 기본값

- 폰트: 미지정 시 **Pretendard**. 아이콘: **Tabler**(1.5 stroke).
- 렌더 라이브러리(신규/Case A 권장): 차트 **ECharts** · 데이터 테이블 **Grid.js**(경량·정렬). SSR 기존 `<table>` 강화는 Simple-Datatables. (B·C는 기존 라이브러리를 따름.)
- 밀도 프리셋: Comfortable(읽는 화면) / Compact(훑는 화면).

## 권장 실행 환경

문서·토큰·인테이크 중심이라 최상위 모델이 상시 필요하지 않습니다. **기본 Sonnet**(비용↓), 최종 시안·목업 품질이 중요한 단계에서만 상위 모델을 씁니다. 화면은 1개씩, 목업은 방향당 1장으로 스코프를 좁히면 효율적입니다.

## 라이선스

MIT — [LICENSE](LICENSE) 참조.
