# Room Scan & BIM Pipeline

## 1. 공간 스캔 목표

단순 시각화가 아니라, 생성형 3D 디자인을 제약하고 검증할 수 있는 구조화된 공간 데이터를 만든다.

## 2. 입력 소스

| 입력 | 활용 |
|---|---|
| LiDAR/Depth scan | 방 메쉬, 치수, 평면 추정 |
| RGB camera | 객체/재질/설비 인식 |
| Existing floor plan | 스캔 보정, 벽/문/창 위치 확인 |
| BIM/IFC file | 전문 프로젝트의 기준 데이터 |
| Manual calibration | 기준 길이, 수평/수직 보정 |

## 3. 공간 이해 파이프라인

```text
Raw Scan
→ Mesh cleanup
→ Plane detection
→ Wall/floor/ceiling segmentation
→ Door/window/opening detection
→ Fixture detection
→ Coordinate calibration
→ Semantic spatial graph
→ Design-ready room model
```

## 4. Semantic Spatial Graph 예시

```json
{
  "room": {"type": "cafe", "area_m2": 38.2, "ceiling_height_mm": 2700},
  "surfaces": [
    {"id":"wall_north", "type":"wall", "width_mm":6200, "height_mm":2700},
    {"id":"floor_main", "type":"floor", "area_m2":38.2}
  ],
  "openings": [
    {"id":"door_entrance", "type":"door", "width_mm":1200, "swing":"inward"},
    {"id":"window_01", "type":"window", "width_mm":3000}
  ],
  "fixtures": [
    {"id":"outlet_01", "type":"power_outlet", "position":[1.2,0.4,0.3]},
    {"id":"sprinkler_01", "type":"sprinkler"}
  ]
}
```

## 5. BIM/CAD 연동

### 가져오기
- IFC: 공간, 벽, 문, 창, 구조체.
- DWG/DXF: 평면도 레이어.
- SKP/Revit export: 기존 3D 모델.

### 내보내기
- 컨셉 모델: GLB/USDZ.
- 디자이너 후작업: FBX/OBJ.
- CAD 협업: DWG/DXF 2D layout.
- BIM 협업: IFC object placement.
- 견적: CSV/XLSX/PDF.

## 6. 정확도 관리

| 항목 | 방법 |
|---|---|
| 치수 오차 | 기준 길이 입력, 스캔 보정, 여러 각도 스캔 |
| 드리프트 | AR anchor 재보정, 룸 기준 좌표계 사용 |
| 객체 오인식 | 사용자 확인 UI, 수동 라벨 수정 |
| 벽/문 누락 | 평면도 업로드와 병합 |
| BIM 충돌 | 전문 BIM 도구 검토 필요 라벨 표시 |
