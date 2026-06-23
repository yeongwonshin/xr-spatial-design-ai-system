# System Overview

## 1. 전체 아키텍처

RoomForge XR는 7개 주요 레이어로 구성된다.

```text
[XR Client]
  ├─ Vision Pro / Quest / iPad LiDAR / Web Viewer
  ├─ 3D Pen / Hand / Voice / Text Input
  └─ Real-time Collaboration UI

[Spatial Capture & Understanding]
  ├─ Room scan mesh
  ├─ Plane/wall/floor/ceiling detection
  ├─ Object and fixture detection
  └─ Semantic room graph

[Prompt & Constraint Compiler]
  ├─ Sketch parser
  ├─ Voice/text intent parser
  ├─ Style/functional constraints
  ├─ Dimension and placement constraints
  └─ Constraint JSON schema

[Generation Orchestrator]
  ├─ Text-to-3D / Image-to-3D / Sketch-to-3D
  ├─ Asset retrieval from marketplace
  ├─ Brand catalog matching
  ├─ Variant generation
  └─ Retopology / PBR / LOD

[Spatial Validation Engine]
  ├─ Collision detection
  ├─ Clearance and path checking
  ├─ Ergonomic and business rules
  ├─ Budget check
  └─ Installability scoring

[Project Platform]
  ├─ Versioning
  ├─ Review and approval
  ├─ BOM / quotation
  ├─ CAD/BIM export
  └─ Analytics

[Commerce & Integrations]
  ├─ Furniture/product catalog
  ├─ Inventory / pricing / lead time
  ├─ CAD/BIM tools
  ├─ CRM / proposal tools
  └─ Payment / procurement
```

## 2. 핵심 데이터 객체

| 객체 | 설명 |
|---|---|
| Project | 고객/현장/팀/버전 정보를 포함하는 최상위 단위 |
| SpaceScan | 스캔 메쉬, 평면, 치수, 좌표계, 신뢰도 |
| SpatialGraph | 방, 벽, 창문, 문, 설비, 기존 가구의 의미 그래프 |
| SketchStroke | 펜/손으로 그린 3D 선, 박스, 영역, 화살표 |
| PromptIntent | 음성/텍스트에서 추출한 스타일, 기능, 제약 |
| DesignConstraint | 생성 모델과 배치 엔진이 실행할 수 있는 정규화된 제약 |
| Asset | 생성/검색/브랜드 카탈로그에서 온 3D 에셋 |
| LayoutVariant | 특정 버전의 가구/오브젝트 배치안 |
| ValidationReport | 충돌, 치수, 동선, 예산, 설치성 결과 |
| Quote | 제품, 수량, 단가, 시공비, 납기, 마진 포함 견적 |

## 3. 운영 모드

### A. Live Co-design Mode
현장 미팅에서 고객과 디자이너가 XR로 함께 디자인한다. 빠른 생성과 피드백이 중요하다.

### B. Studio Refinement Mode
디자이너가 사무실에서 생성안을 정리하고, 치수와 견적을 세밀하게 조정한다.

### C. Client Review Mode
고객이 링크나 Vision Pro/iPad/Web으로 결과를 보고 코멘트/승인한다.

### D. Procurement Mode
확정된 디자인안을 제품 발주, 자재 견적, 시공 일정으로 전환한다.

## 4. 시스템 SLA 목표

| 기능 | 목표 |
|---|---:|
| 공간 스캔 후 기본 룸 그래프 생성 | 30~90초 |
| 간단한 에셋 생성 프리뷰 | 20~60초 |
| 카탈로그 기반 배치 추천 | 5~15초 |
| 충돌/통로/예산 검증 | 3~10초 |
| 고품질 렌더/텍스처 생성 | 비동기 작업 |
| CAD/BIM 출력 | 프로젝트 복잡도별 비동기 |

주의: 실제 제품에서는 생성형 3D 모델의 품질과 속도 편차가 크므로, 즉석 미팅에는 “저해상도 프리뷰 → 백그라운드 고품질화” 파이프라인을 제공해야 한다.
