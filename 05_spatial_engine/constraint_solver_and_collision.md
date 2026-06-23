# Constraint Solver & Collision Engine

## 1. 목적

생성 결과가 “보기 좋은 3D 이미지”에서 끝나지 않고 실제 공간에 놓일 수 있는지 검증한다.

## 2. 제약조건 종류

### Hard Constraints
반드시 지켜야 한다.

- 문/비상구/소화전 앞 비워두기.
- 벽, 바닥, 천장과 물리적 충돌 금지.
- 최소 통로 폭.
- 지정 예산 상한.
- 브랜드/고객이 금지한 소재.

### Soft Constraints
가능하면 지킨다.

- 스타일 일관성.
- 창가 선호.
- 대칭 배치.
- 고객 선호 브랜드.
- 따뜻한 조명 분위기.

## 3. 충돌 검증

### 데이터 구조
- AABB: 빠른 1차 검사.
- OBB: 회전된 가구 검사.
- Convex hull: 복잡한 에셋 근사.
- Mesh collider: 최종 정밀 검사.

### 체크 항목
| 체크 | 설명 |
|---|---|
| Object-object | 의자와 테이블, 소파와 선반 충돌 |
| Object-room | 벽/창/문/천장과 충돌 |
| Door swing | 문 개폐 반경 침범 |
| Human clearance | 통로, 의자 후퇴, 카운터 작업 공간 |
| Ceiling clearance | 조명/행잉 구조물 높이 |

## 4. 동선 검증

- 입구에서 주요 좌석/카운터/출구까지 경로 탐색.
- 장애물 기반 navigation mesh 생성.
- 최소 통로 폭 기준 적용.
- 병목 구간 표시.

## 5. 배치 최적화

### 목적 함수 예시

```text
score =
  0.25 * intent_match
+ 0.20 * clearance_score
+ 0.15 * style_score
+ 0.15 * budget_score
+ 0.10 * catalog_availability
+ 0.10 * visibility_score
+ 0.05 * symmetry_score
- 1.00 * hard_violation_count
```

### 최적화 방식
- 규칙 기반 초기 배치.
- 후보 샘플링.
- 제약 충족 필터링.
- 점수 기반 랭킹.
- 디자이너 선택/수정 피드백 반영.

## 6. 검증 리포트 예시

```json
{
  "layout_id": "variant_004",
  "status": "needs_review",
  "score": 0.78,
  "violations": [
    {
      "severity": "high",
      "type": "clearance",
      "message": "입구 동선 폭이 820mm로 목표 900mm보다 80mm 부족합니다.",
      "object_ids": ["chair_03", "door_entrance"]
    }
  ],
  "suggestions": [
    "chair_03을 오른쪽으로 120mm 이동",
    "테이블 폭 700mm 제품으로 교체"
  ]
}
```
