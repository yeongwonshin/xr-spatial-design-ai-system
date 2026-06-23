# Meshy & 3D Model Provider Integrations

## 1. 통합 원칙

외부 3D 생성 서비스는 제품의 핵심 경험을 빠르게 구현하는 데 유용하지만, 전문 시스템에서는 벤더 종속을 피해야 한다.

## 2. Provider Abstraction

```text
GenerationProvider Interface
├─ create_text_to_3d_job(prompt, constraints)
├─ create_image_to_3d_job(image, prompt, constraints)
├─ get_job_status(job_id)
├─ download_asset(job_id)
├─ estimate_cost(request)
└─ get_capabilities()
```

## 3. 지원해야 할 기능

| 기능 | 설명 |
|---|---|
| Text-to-3D | 스타일/객체 프롬프트 기반 모델 생성 |
| Image-to-3D | 레퍼런스 이미지에서 모델 생성 |
| Sketch-to-3D | 공간 스케치를 구조 제약으로 사용 |
| Texture generation | 재질/색상/PBR 텍스처 생성 |
| Retopology | XR용 경량화 |
| Format conversion | GLB/USDZ/FBX/OBJ 변환 |

## 4. 데이터 최소화

외부 제공자에게는 가능한 한 다음만 전달한다.

- 객체 단위 프롬프트.
- 필요한 대략 치수.
- 스타일/소재 키워드.
- 익명화된 스케치 구조.

원본 방 스캔, 고객명, 주소, 견적, 내부 코멘트는 전달하지 않는다.

## 5. 품질 비교 기준

- 생성 속도.
- 치수 제어력.
- 메쉬 품질.
- 텍스처 품질.
- 상업 사용 정책.
- API 안정성.
- 비용.
- 출력 포맷.

## 6. fallback 전략

1. 외부 생성 실패 시 유사 카탈로그 에셋 추천.
2. 저품질 생성 시 placeholder + 디자이너 수동 보정 요청.
3. 고비용 작업은 배치 작업으로 전환.
4. 특정 제공자 장애 시 다른 제공자로 라우팅.
