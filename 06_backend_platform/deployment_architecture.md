# Deployment Architecture

## 1. 권장 클라우드 아키텍처

```text
Client Apps
→ API Gateway
→ Auth Service
→ Project Service
→ Constraint Compiler Service
→ Generation Orchestrator
→ Validation Service
→ Quote Service
→ Export Service
→ Collaboration Realtime Service
→ Storage / DB / Queue / Cache
```

## 2. 서비스 구성

| 서비스 | 역할 |
|---|---|
| API Gateway | 인증, rate limit, routing |
| Auth/RBAC | 조직/프로젝트 권한 관리 |
| Project Service | 프로젝트, 공간, 버전 관리 |
| Spatial Service | 룸 그래프, 메쉬 처리 |
| Constraint Compiler | 스케치/프롬프트 제약 변환 |
| Generation Orchestrator | 외부/내부 3D 생성 job 관리 |
| Asset Service | 에셋 저장, 검색, 변환, 라이선스 |
| Validation Service | 충돌, 동선, 규칙 검증 |
| Quote Service | 견적, BOM, 가격/재고 연동 |
| Export Service | GLB/USDZ/CAD/BIM/PDF 출력 |
| Collaboration Service | 실시간 세션, 코멘트, 승인 |
| Analytics Service | KPI, 비용, 사용량 분석 |

## 3. 비동기 작업

생성/렌더/export는 큐 기반으로 처리한다.

```text
Job Request → Queue → Worker Pool → External/Internal Model → Postprocess → Storage → Notification
```

## 4. 멀티테넌시

- Organization 단위 데이터 격리.
- Enterprise는 전용 스토리지 버킷/DB schema 옵션.
- 에셋 마켓플레이스는 public/private/team scope 구분.

## 5. 비용 최적화

- 프리뷰 모델과 고품질 모델 분리.
- 중복 프롬프트/에셋 캐싱.
- 카탈로그 검색 우선으로 생성 API 호출 감소.
- 사용량 기반 rate limit.
- 고비용 작업은 사용자에게 크레딧 차감 사전 표시.

## 6. 관측성

- Job duration.
- Model provider latency/failure.
- Generation cost per project.
- Validation error categories.
- XR client FPS/crash.
- Export success rate.
- Quote conversion.
