# Evaluation Metrics

## 1. 생성 품질 지표

| 지표 | 설명 | 목표 |
|---|---|---:|
| Intent Match Score | 사용자 프롬프트와 결과의 의미 일치도 | 0.80+ |
| Spatial Constraint Satisfaction | 위치, 크기, 방향, 통로 등 제약 충족률 | 0.90+ |
| Style Match Score | 스타일 키워드와 시각적 결과 일치도 | 0.75+ |
| Asset Usability Score | 메쉬 품질, 텍스처, 성능, 실제 배치 가능성 | 0.85+ |
| Catalog Match Rate | 생성 대신 실제 구매 가능 제품으로 대체 가능한 비율 | 0.60+ |

## 2. 공간 검증 지표

| 지표 | 설명 |
|---|---|
| Collision Count | 오브젝트 간/공간 구조물과의 충돌 수 |
| Clearance Violations | 통로 폭, 문 개폐, 좌석 간격 위반 수 |
| Walkability Score | 입구, 좌석, 카운터, 출구 간 이동성 |
| Visibility Score | 사인, 제품, 전시물의 시야 확보 정도 |
| Ergonomic Fit | 좌석 높이, 테이블 높이, 조작 거리 적합도 |

## 3. 비즈니스 지표

| 지표 | 목적 |
|---|---|
| Time to First Design | 고객 미팅에서 첫 디자인안까지 걸린 시간 |
| Revision Rounds | 계약 전 수정 횟수 |
| Proposal Conversion Rate | 제안서 → 계약 전환율 |
| Average Project Value | 평균 프로젝트 매출 |
| Quote Accuracy | 최초 견적과 최종 견적 차이 |
| Asset-to-Purchase Conversion | 배치된 제품의 실제 구매 전환율 |

## 4. UX 지표

- 첫 사용자가 공간 스캔과 첫 배치를 완료하는 시간.
- 스케치 입력의 오인식률.
- 음성 명령 재입력률.
- 디자이너가 AI 결과를 그대로 채택하는 비율.
- 고객이 “공간 이해가 쉬웠다”고 평가한 비율.

## 5. 운영 비용 지표

- 생성 1회당 외부 API 비용.
- 고품질 렌더 1장당 GPU 비용.
- 프로젝트당 평균 저장 용량.
- 모델 변환/검증 실패율.
- 사용자 세션당 XR 렌더링 성능.
