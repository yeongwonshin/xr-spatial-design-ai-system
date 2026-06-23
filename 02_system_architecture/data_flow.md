# Data Flow

## 1. 입력 단계

### 1.1 공간 스캔 입력
- 카메라 프레임
- Depth/LiDAR 포인트 클라우드
- AR 세션 좌표계
- 평면 추정 결과
- 사용자가 수동 지정한 기준점

### 1.2 사용자 의도 입력
- 3D 펜 스트로크: 위치, 방향, 압력, 시간, 사용자 ID.
- 손 제스처: 선택, 이동, 회전, 스케일, 삭제.
- 음성: 원문 오디오, STT 결과, 언어, 신뢰도.
- 텍스트: 스타일, 기능, 예산, 브랜드, 금지 조건.

## 2. 정규화 단계

```text
Raw Input
→ Coordinate Normalization
→ Stroke Segmentation
→ Semantic Intent Extraction
→ Spatial Reference Binding
→ Constraint JSON Generation
```

예:  
사용자 발화: “창가 쪽에 북유럽풍 2인석을 3개 놓고, 입구 동선은 막지 마.”  
스케치: 창가 주변에 3개 사각형 표시.  
정규화 결과:

```json
{
  "objects": [
    {"type":"dining_set", "quantity":3, "seating":2, "style":"nordic"}
  ],
  "placement": {
    "near":"window_zone",
    "avoid":"entrance_path",
    "clearance_min_mm":900
  }
}
```

## 3. 생성 단계

1. 제약조건 분석.
2. 카탈로그 우선 검색.
3. 부족한 에셋은 3D 생성 API 호출.
4. 생성 결과를 스케일 정규화.
5. PBR 재질, LOD, 콜라이더 생성.
6. 룸 그래프에 배치.

## 4. 검증 단계

- 오브젝트-오브젝트 충돌.
- 오브젝트-벽/문/창/설비 충돌.
- 통로 폭과 회전 반경.
- 좌석 수, 수납량, 사용 목적 충족도.
- 예산과 납기.
- 브랜드 카탈로그 실제 판매 여부.

## 5. 출력 단계

- XR 실시간 미리보기.
- 고객 리뷰 링크.
- 견적서/BOM.
- GLB/USDZ/FBX.
- CAD/BIM 변환 파일.
- 프레젠테이션 렌더.
