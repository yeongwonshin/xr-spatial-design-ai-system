# Measurement & Costing

## 1. 견적 엔진 목표

디자인안을 고객이 구매/계약할 수 있는 견적으로 전환한다.

## 2. 견적 구성

| 항목 | 설명 |
|---|---|
| Product cost | 가구, 조명, 소품, 전시 모듈 |
| Material cost | 목재, 금속, 패브릭, 페인트, 필름 |
| Labor cost | 시공, 설치, 전기, 도장, 철거 |
| Logistics | 배송, 반입, 양중, 보관 |
| Design fee | 설계/디자인 수수료 |
| Contingency | 예비비 |
| Margin | 업체 마진 |
| Tax | 부가세 등 |

## 3. 수량 산출

- 바닥 면적 기반: 마감재, 카펫, 타일.
- 벽면 면적 기반: 페인트, 필름, 사인.
- 길이 기반: 선반, 조명 레일, 카운터.
- 개수 기반: 가구, 조명, 소품.
- 공정 기반: 철거, 전기, 설비, 설치.

## 4. 예산 최적화

사용자가 “예산 800만 원 이하”라고 하면:

1. 필수 기능 유지.
2. 고가 에셋을 대체 상품으로 교체.
3. 커스텀 제작을 기성 제품으로 변경.
4. 소재 등급 조정.
5. 시공 범위 축소안을 제안.

## 5. 견적 신뢰도

| 상태 | 의미 |
|---|---|
| Estimated | AI 또는 룰 기반 추정 |
| Catalog Verified | 제품 단가 확인 |
| Vendor Quoted | 협력사 견적 반영 |
| Contract Ready | 고객 승인 가능 |

## 6. 출력 예시

```json
{
  "quote_id":"quote_2026_00041",
  "currency":"KRW",
  "subtotal":8200000,
  "tax":820000,
  "total":9020000,
  "confidence":"catalog_verified",
  "items":[
    {"name":"Nordic chair", "qty":12, "unit_price":135000, "total":1620000},
    {"name":"Oak table", "qty":6, "unit_price":280000, "total":1680000},
    {"name":"Pendant light", "qty":4, "unit_price":190000, "total":760000}
  ]
}
```
