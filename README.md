# XR 공간 디자인 생성 AI 전문 시스템 디렉토리

프로젝트명: **Spatial Design Copilot for XR**  
한 줄 정의: 사용자가 실제 공간 위에 펜·손·음성으로 의도를 표현하면, AI가 **치수·충돌·스타일·예산·브랜드 카탈로그 제약**을 만족하는 3D 인테리어/전시/가구 배치안을 생성하고 견적·도면·BIM/CAD 내보내기까지 연결하는 B2B 전문 시스템.

---

## 0. 핵심 전환점

단순 MVP는 “방 스캔 → 선 그림 → 프롬프트 → 3D 모델 생성”입니다. 전문 시스템은 아래 기능까지 포함해야 합니다.

1. **공간 이해 엔진**: LiDAR/카메라 스캔, 평면·벽·창·문·전기 콘센트·동선·천장고 추론.
2. **스케치-제약 컴파일러**: 사용자의 3D 펜 선, 박스, 화살표, 말풍선, 음성을 치수·배치·스타일·기능 제약조건으로 변환.
3. **생성형 3D 오케스트레이터**: Text/Image/Sketch-to-3D 모델, 에셋 DB, CAD 라이브러리, 브랜드 카탈로그를 조합.
4. **공간 검증 레이어**: 충돌, 통로 폭, 시야, 인체공학, 피난/안전 룰, 설치 가능성, 예산 초과 여부 검증.
5. **협업·승인 워크플로우**: 디자이너, 고객, 시공사, 브랜드 담당자가 같은 XR 공간에서 버전별 코멘트와 승인을 남김.
6. **상업화 레이어**: 견적서, 자재/가구 주문, 프로젝트 단위 과금, 에셋 마켓플레이스, 브랜드 PPL/입점 수수료.

---

## 1. 디렉토리 구조

```text
XR_Spatial_Design_AI_Professional_System/
├── README.md
├── 01_strategy/
│   ├── product_brief.md
│   ├── personas_and_use_cases.md
│   ├── business_model.md
│   └── competitive_positioning.md
├── 02_system_architecture/
│   ├── system_overview.md
│   ├── reference_architecture.mmd
│   ├── component_matrix.csv
│   └── data_flow.md
├── 03_ai_pipeline/
│   ├── ai_pipeline.md
│   ├── prompt_constraint_schema.json
│   ├── model_generation_workflow.md
│   ├── evaluation_metrics.md
│   └── safety_quality_guardrails.md
├── 04_xr_client/
│   ├── interaction_design.md
│   ├── visionos_unity_client_spec.md
│   └── collaboration_spec.md
├── 05_spatial_engine/
│   ├── room_scan_bim_pipeline.md
│   ├── constraint_solver_and_collision.md
│   └── measurement_costing.md
├── 06_backend_platform/
│   ├── api_spec_openapi.yaml
│   ├── data_model.md
│   ├── security_privacy.md
│   └── deployment_architecture.md
├── 07_integrations/
│   ├── meshy_and_3d_model_providers.md
│   ├── cad_bim_exports.md
│   └── asset_marketplace.md
├── 08_operations/
│   ├── implementation_roadmap.md
│   ├── team_roles.md
│   ├── kpi_and_pricing.md
│   └── risk_register.md
├── 09_sales_demo/
│   ├── demo_script.md
│   └── proposal_template.md
└── 10_appendix/
    └── references.md
```

---

## 2. 전문 시스템 명칭 후보

- **RoomForge XR**: 공간을 “단조/제작”한다는 이미지.
- **Spatial Studio AI**: B2B 디자인 스튜디오형 SaaS.
- **FormaXR**: 형태·공간·제작을 포괄.
- **MuseRoom AI**: 펜 기반 XR 입력과 인테리어 도메인을 직관적으로 연결.

권장 명칭: **RoomForge XR**  
이유: 인테리어, 전시, 리테일, 게임 공간 제작까지 확장 가능하고 B2B 도구 느낌이 강함.

---

## 3. 핵심 사용자 여정

```text
현장 방문/스캔
→ 공간 자동 이해
→ XR에서 펜/손/음성으로 의도 입력
→ 제약조건 컴파일
→ 3D 생성/에셋 추천/카탈로그 매칭
→ 치수·충돌·예산·동선 검증
→ 고객 협업 리뷰
→ 견적·도면·BOM·렌더·BIM/CAD 내보내기
→ 계약/구매/시공 연동
```

---

## 4. 시스템의 차별점

기존 AI 인테리어 도구는 대개 2D 사진 기반 리렌더링이나 텍스트 기반 콘셉트 이미지 생성에 머뭅니다. 이 시스템은 **실제 공간 스케일**, **3D 배치 제약**, **B2B 견적/납품 워크플로우**를 통합합니다.

가장 중요한 차별점은 사용자의 대략적 스케치가 단순 참고 이미지가 아니라, 생성 모델을 통제하는 **실행 가능한 공간 제약조건**으로 바뀐다는 점입니다.
