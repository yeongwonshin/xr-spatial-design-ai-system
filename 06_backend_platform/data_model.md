# Data Model

## 1. ERD 개념

```text
Organization 1---N User
Organization 1---N Project
Project 1---N Space
Project 1---N LayoutVariant
Space 1---1 SpatialGraph
LayoutVariant 1---N PlacedAsset
Asset N---N ProductCatalogItem
LayoutVariant 1---N ValidationReport
LayoutVariant 1---N Quote
Project 1---N Comment
Project 1---N Approval
```

## 2. 주요 테이블

### organizations
| 필드 | 타입 | 설명 |
|---|---|---|
| id | uuid | 조직 ID |
| name | text | 회사명 |
| plan | enum | 구독 플랜 |
| region | text | 데이터 리전 |

### projects
| 필드 | 타입 | 설명 |
|---|---|---|
| id | uuid | 프로젝트 ID |
| organization_id | uuid | 소속 조직 |
| client_name | text | 고객명 |
| domain | enum | 주거/카페/전시 등 |
| status | enum | draft/review/approved/procurement |

### spaces
| 필드 | 타입 | 설명 |
|---|---|---|
| id | uuid | 공간 ID |
| project_id | uuid | 프로젝트 |
| scan_mesh_url | text | 원본/정리 메쉬 |
| room_graph_json | jsonb | 의미 공간 그래프 |
| accuracy_score | float | 스캔 신뢰도 |

### sketch_strokes
| 필드 | 타입 | 설명 |
|---|---|---|
| id | uuid | 스트로크 ID |
| space_id | uuid | 공간 |
| user_id | uuid | 작성자 |
| points | jsonb | 3D 포인트 배열 |
| semantic_type | enum | outline/path/region 등 |

### design_constraints
| 필드 | 타입 | 설명 |
|---|---|---|
| id | uuid | 제약 ID |
| project_id | uuid | 프로젝트 |
| type | enum | dimension/clearance/style/budget 등 |
| priority | enum | hard/soft |
| source | enum | sketch/voice/text/system |
| payload | jsonb | 제약 상세 |

### assets
| 필드 | 타입 | 설명 |
|---|---|---|
| id | uuid | 에셋 ID |
| source | enum | generated/catalog/uploaded/library |
| file_url | text | GLB/USDZ 등 |
| metadata | jsonb | 스타일/치수/소재 |
| license_status | enum | commercial/limited/unknown |

### placed_assets
| 필드 | 타입 | 설명 |
|---|---|---|
| id | uuid | 배치 ID |
| layout_id | uuid | 레이아웃 |
| asset_id | uuid | 에셋 |
| transform | jsonb | 위치/회전/스케일 |
| locked | boolean | 디자이너 잠금 여부 |

## 3. 저장소 전략

- PostgreSQL: 프로젝트, 권한, 버전, 견적 메타데이터.
- Object Storage: 메쉬, 텍스처, 렌더, export 파일.
- Vector DB: 스타일/에셋/프롬프트 임베딩 검색.
- Graph DB 선택사항: 공간 의미 그래프, 제품 관계, 규칙 추론.
- Cache: 생성 작업 상태, 세션 동기화, 프리뷰 에셋.
