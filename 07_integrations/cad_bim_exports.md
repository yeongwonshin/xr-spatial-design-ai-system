# CAD/BIM Export Strategy

## 1. 목적

XR 생성 결과를 전문 설계·시공 워크플로우로 연결한다.

## 2. 출력 포맷

| 포맷 | 용도 |
|---|---|
| GLB | Web/Unity/Three.js 3D 뷰어 |
| USDZ | Apple AR/XR 미리보기 |
| FBX | DCC/게임 엔진 후작업 |
| OBJ | 범용 3D 교환 |
| DWG/DXF | 2D 평면 배치도 |
| IFC | BIM 협업 |
| PDF | 고객 제안서/견적서 |
| CSV/XLSX | BOM/견적/발주 리스트 |

## 3. Export 레벨

### Concept Export
- 빠른 공유용.
- 실제 치수 신뢰도 중간.
- 렌더/프레젠테이션 중심.

### Design Development Export
- 치수와 배치 검증 완료.
- CAD/BIM 후작업 가능.
- 제품 SKU/BOM 포함.

### Procurement Export
- 구매 가능 제품과 가격/납기 연결.
- 발주/계약에 사용 가능.

## 4. BIM 매핑

| RoomForge 객체 | BIM 매핑 |
|---|---|
| wall | IfcWall |
| door | IfcDoor |
| window | IfcWindow |
| furniture | IfcFurniture 또는 IfcFurnishingElement |
| lighting | IfcLightFixture |
| display fixture | IfcFurniture/IfcElementAssembly |
| zone | IfcSpace/IfcZone |

## 5. 전문 도구 연동

- Revit: IFC 또는 add-in 장기 개발.
- Rhino/Grasshopper: geometry export/API.
- SketchUp: SKP/DAE/GLB import 경로.
- Blender: FBX/GLB 후작업.
- AutoCAD: DWG/DXF 2D layout.

## 6. Export 검증

- 단위 변환 오류 확인.
- 원점/좌표계 확인.
- 오브젝트 피벗 확인.
- 레이어/카테고리 매핑.
- 제품 메타데이터 유지.
- 라이선스/워터마크 적용.
