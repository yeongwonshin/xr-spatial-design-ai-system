# AI Pipeline

## 1. 핵심 아이디어

RoomForge XR의 AI는 단순히 “텍스트로 3D 모델을 생성”하지 않는다. 사용자가 XR에서 남긴 공간 스케치와 음성을 조합해 **실행 가능한 공간 제약조건**을 만들고, 이를 기반으로 3D 생성·배치·검증을 수행한다.

## 2. 파이프라인 개요

```text
1. Spatial Capture
2. Sketch Parsing
3. Speech/Text Understanding
4. Constraint Compilation
5. Candidate Asset Retrieval
6. Generative 3D Creation
7. Asset Normalization
8. Layout Optimization
9. Spatial Validation
10. Human Review & Iterative Refinement
```

## 3. 모듈별 설계

### 3.1 Sketch Parser
입력:
- 3D stroke polyline.
- pressure/velocity/button state.
- temporal grouping.
- 주변 공간 객체.

출력:
- outline, volume, path, region, anchor, arrow, annotation.
- approximate size, orientation, intent confidence.

예:
- 바닥에 사각형: “배치 영역” 또는 “테이블/소파 후보 footprint”.
- 벽면 곡선: “선반/조명/사인 위치”.
- 화살표: “동선” 또는 “방향성”.

### 3.2 Voice/Text Intent Parser
추출 항목:
- object type: chair, sofa, counter, booth, shelf, lighting.
- style: Nordic, industrial, minimal, luxury, cozy.
- function: seating, display, storage, checkout, photo zone.
- constraints: budget, count, material, color, brand, clearance.
- exclusions: “입구를 막지 마”, “높은 가구는 쓰지 마”.

### 3.3 Constraint Compiler
Sketch Parser와 Intent Parser 결과를 합쳐 표준 스키마로 변환한다.

컴파일 전략:
1. 스케치가 정의한 위치·크기·방향을 우선.
2. 음성/텍스트가 정의한 의미·스타일·기능을 결합.
3. 실제 공간 그래프와 바인딩.
4. 충돌 가능성이 높은 제약은 soft constraint로 표시.
5. 안전/법규 관련 제약은 hard constraint로 표시.

### 3.4 Asset Retrieval & Generation
우선순위:
1. 브랜드 카탈로그 실제 판매 제품.
2. 승인된 고품질 에셋 라이브러리.
3. 생성형 3D 모델.
4. 디자이너 수동 업로드 모델.

### 3.5 Layout Optimizer
목표 함수:

```text
maximize DesignFitScore
= StyleMatch
+ FunctionalCoverage
+ SpatialFeasibility
+ BudgetFit
+ BrandPreference
+ UserIntentMatch
- CollisionPenalty
- ClearancePenalty
- OverBudgetPenalty
```

## 4. Human-in-the-loop UX

생성형 AI 결과는 항상 검토 가능해야 한다.

- 생성 결과별 신뢰도 표시.
- 왜 이 위치에 배치했는지 설명.
- 제약 위반 시 빨간 경고 표시.
- “이 의자는 850mm 통로 기준을 120mm 침범합니다”처럼 구체적 피드백.
- 디자이너가 수동 이동하면 해당 배치를 새 제약으로 학습/저장.

## 5. 데이터 축적 전략

| 데이터 | 활용 |
|---|---|
| 스케치-의도-최종결과 쌍 | 제약 컴파일러 개선 |
| 고객 승인/거절 로그 | 추천 랭킹 개선 |
| 실제 구매/시공 데이터 | 견적 정확도 개선 |
| 충돌/수정 로그 | 검증 엔진 룰 개선 |
| 스타일별 성공 프로젝트 | 템플릿/프리셋 상품화 |
