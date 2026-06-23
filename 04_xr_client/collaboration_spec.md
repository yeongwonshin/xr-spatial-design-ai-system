# Collaboration Spec

## 1. 협업 목표

전문 공간 디자인 프로젝트는 혼자 완성되지 않는다. 고객, 디자이너, 시공사, 브랜드 담당자가 같은 공간 버전을 보고 논의해야 한다.

## 2. 협업 기능

### A. Shared XR Session
- 여러 사용자가 같은 방 모델을 XR에서 확인.
- 사용자별 아바타/커서/스케치 색상.
- 발화와 스케치가 타임라인에 기록.

### B. Comment Pins
- 공간 내 특정 위치에 코멘트 핀 추가.
- 오브젝트, 벽면, 동선, 예산 항목에 연결.
- resolved/unresolved 상태 관리.

### C. Version Control
- layout_variant별 버전 생성.
- “고객 미팅 v1”, “견적 조정 v2”, “시공 검토 v3”처럼 명명.
- 버전 간 추가/삭제/이동/가격 차이 비교.

### D. Approval Workflow
- 고객 승인.
- 디자이너 내부 승인.
- 시공 가능성 검토.
- 최종 견적 승인.

### E. Permission Model

| 역할 | 보기 | 코멘트 | 편집 | 생성 | 견적 | 승인 | 관리자 |
|---|---|---|---|---|---|---|---|
| Client | O | O | 제한 | X | 요약 | O | X |
| Designer | O | O | O | O | O | 요청 | X |
| PM | O | O | O | O | O | O | 제한 |
| Contractor | O | O | 제한 | X | 설치비 | 검토 | X |
| Admin | O | O | O | O | O | O | O |

## 3. 실시간 동기화 모델

- Scene graph operation 기반 동기화.
- Stroke event streaming.
- Asset transform delta sync.
- Conflict resolution: latest intent with role priority.
- 중요 작업은 optimistic update 후 서버 검증.

## 4. 감사 로그

저장해야 할 이벤트:
- 생성 요청.
- 제약조건 변경.
- 오브젝트 이동/삭제/교체.
- 가격 변경.
- 코멘트/승인/반려.
- export 생성.
- 외부 공유 링크 접근.

## 5. 고객 공유 형태

1. XR 공동 리뷰.
2. Web 3D viewer 링크.
3. iPad AR 미리보기.
4. PDF 제안서.
5. 짧은 walkthrough 영상.
