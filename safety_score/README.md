### 지역별 안전점수 산정

**🔎 목적**

- 서울특별시 각 동 단위로 범죄율, cctv 밀도, 귀갓길 안전시설 데이터를 통합하고, 기존 부동산 데이터에 반영하여 이용자 신뢰도를 높이는 목적의 정량 지표 제공 시스템 구현

---

**📍 Tech Stack**

| Component | Technology Used |
| --- | --- |
| Data Handling | pandas, numpy |
| Normalization | log1p, scikit-learn, MinMaxScaler |

---

**🔁 통합 안전지수 산출 로직**
| 항목 | 설명 | 처리 방법 | 가중치 |
| ---- | ---- | ---- | ---- |
| 범죄율 | 강력/폭력/절도/마약 범죄율(5대 범죄) 반영 | 범죄율이 낮을수록 높은 점수 부여 | 40 |
| CCTV 수량 | 지역별 인구당 CCTV 밀도 반영 | 인구대비 CCTV 수를 0~100점으로 정규화 | 40 |
| 안심귀갓길 존재 | 지역 내 귀갓길 수, 귀갓길에 설치된 시설 수 | 귀갓길 서비스 0~100점 정규화 | 20 |
- 범죄율과 cctv는 구 단위
- 귀갓길 점수는 동 단위

---

⇒ 실제 지역 안전지수나 cctv 설치 기준은 구 단위 공식 통계 기반

  (서울시와 경찰청 등의 안전정책 수립에도 주요 기준으로 채택)
  - 객관적 통계 기반의 항목에 균등 가중치(40%)를 부여
  - 체감 기반 지표인 귀갓길 시설 항목은 보조적 지표로 20% 가중치를 적용하여 **객관성 + 체감의 균형을 고려**한 점수 체계 설계
