# visionOS / Unity Client Spec

## 1. 권장 클라이언트 전략

### Phase 1
- Apple Vision Pro native 또는 Unity PolySpatial 기반.
- iPad Pro LiDAR companion app.
- WebGL/Three.js 기반 고객 리뷰 뷰어.

### Phase 2
- Meta Quest 지원.
- Desktop Studio Editor.
- Mobile AR quick preview.

## 2. 주요 기능

| 기능 | 설명 |
|---|---|
| Room scan import | ARKit/RoomPlan 또는 자체 스캔 결과 로드 |
| Spatial drawing | 3D 펜/손/컨트롤러 입력으로 선·영역 생성 |
| Voice capture | 음성 명령 녹음, STT, intent update |
| Object manipulation | grab/move/rotate/scale/snap |
| Constraint overlay | hard/soft constraint 시각화 |
| Validation overlay | 충돌/통로/예산 경고 표시 |
| Multiplayer session | 공동 편집, 사용자별 색상, 라이브 커서 |
| Asset preview | 저해상도 프리뷰와 고품질 모델 교체 |

## 3. 성능 예산

| 항목 | 목표 |
|---|---:|
| XR 프레임 안정성 | 60fps 이상 권장 |
| 장면 내 활성 삼각형 수 | 디바이스별 LOD 자동 조정 |
| 동시 사용자 | 초기 4명, 엔터프라이즈 20명 목표 |
| 메쉬 스트리밍 | Progressive loading |
| 오브젝트 조작 지연 | 50ms 이하 목표 |

## 4. 로컬-서버 역할 분리

### 로컬 클라이언트
- 입력 캡처.
- 기본 스케치 렌더링.
- 저해상도 메쉬 표시.
- 간단한 충돌 프리체크.
- 오프라인 임시 저장.

### 서버
- 고품질 룸 그래프 생성.
- STT/NLU/제약 컴파일.
- 3D 생성 API 오케스트레이션.
- 최종 검증/견적.
- 버전 관리.

## 5. 좌표계 관리

- AR session origin과 room origin을 분리.
- 모든 에셋은 meter 단위로 정규화.
- export 시 mm/cm/m 단위 변환.
- 협업 세션에서는 anchor sync와 drift correction 필요.

## 6. 에러/피드백 UX

| 상황 | 사용자 피드백 |
|---|---|
| 스캔 신뢰도 낮음 | “이 벽면을 한 번 더 스캔해 주세요.” |
| 음성 의도 불명확 | “의자, 테이블, 선반 중 무엇을 원하시나요?” |
| 생성 지연 | 저해상도 placeholder 우선 표시 |
| 충돌 발생 | 충돌 부위 빨간 하이라이트와 수정 제안 |
| 예산 초과 | 대체 제품/소재 추천 |
