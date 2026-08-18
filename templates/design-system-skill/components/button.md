# 버튼

> 실제 코드베이스의 마크업을 그대로 붙여넣으세요. 이것이 컴포넌트 문서의 핵심입니다.

## 변형

### Primary (주요 액션 — 화면당 1개 권장)
```html
{<button type="button" class="btn btn-primary">저장</button>}
```

### Secondary (보조 액션)
```html
{<button type="button" class="btn btn-default">취소</button>}
```

### Danger (삭제 등 파괴적 액션 — 확인 다이얼로그 필수)
```html
{<button type="button" class="btn btn-danger">삭제</button>}
```

## 상태
- disabled: {class에 `disabled` 추가 + disabled 속성}
- loading: {버튼 텍스트를 "처리 중..."으로, disabled 처리}

## 규칙
- 버튼 텍스트는 동사로 (예: "저장", "조회") — "확인/OK" 남용 금지
- 한 화면에 primary 버튼은 1개가 원칙
- 인라인 스타일 버튼 생성 금지 — 반드시 위 클래스 사용
