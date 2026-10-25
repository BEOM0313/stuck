# 역발상 촉매 가치 점수 v2

가치투자 장부의 종목 추천 알고리즘이에요. 100점 만점이고 70점 이상은 추천, 55점 이상은 관찰, 그 아래는 제외예요.

## 점수 구성

| 항목 | 배점 | 기준 | 근거 |
|---|---|---|---|
| 촉매 | 25 | 12개월~3년 안에 수요를 바꿀 구체적 사건. 내구연한 도래, 발주·입찰 공고, 정책, 지정학. 날짜와 규모가 특정될수록 높게. | 대신증권(2025.11.04) |
| 가치 | 20 | P/CF·PER·PBR이 자기 과거 5~10년 평균과 업종 대비 얼마나 낮은지, 적정가치 대비 안전마진. 한국은 낮은 PBR이 낮은 ROE의 정당한 반영일 수 있어 ROE와 함께 봄. | Lakonishok·Shleifer·Vishny, 자본시장연구원 이슈보고서 24-31 |
| 비관 과잉 | 15 | 3~5년 누적 부진, 과거 저성장이 주가에 과하게 반영됐는지. 최근 몇 주의 급락만으로는 낮게 줌. | De Bondt·Thaler, Lakonishok·Shleifer·Vishny |
| 악재 성격 | 10 | 업황·거시·섹터 전체 악재처럼 회사 본질과 무관한 하락이면 높게, 소송·규제·실적 하향처럼 회사 고유의 악재가 이어지는 중이면 낮게. | 펜실베이니아대 와튼 재무학과 연구 |
| 재무 품질 | 15 | 피오트로스키 F-점수(0~9)를 15점으로 환산. 흑자, 영업현금흐름, 부채 감소, 마진 개선, 증자 없음. | Piotroski, Asness·Frazzini·Pedersen, Campbell·Hilscher·Szilagyi |
| 추세 확인 | 10 | 가격이 바닥을 다지고 돌아서는지, 이익 추정치가 상향되기 시작했는지. 떨어지는 칼날은 낮게. | Asness·Moskowitz·Pedersen |
| 습관 적합 | 5 | 이해하는 산업(인프라·운송·에너지·헬스케어·플랫폼) 가점, 같은 테마 보유 시 감점. | - |

## 먼저 거르는 조건

- 재무 부실 신호: 부채비율 200% 초과, 2년 이상 영업적자, 2년 연속 영업현금흐름 마이너스 (부실주는 장기 수익률이 낮음)
- F-점수 3 이하 (저점수 가치주는 상장폐지 확률이 5배 이상)
- 감사의견 비적정, 관리종목, 거래정지
- 일평균 거래대금 10억 원 미만
- 종목당 비중 상한 초과

## 분할 매수

- 70점 이상: 1차 40% 매수
- 촉매가 확인되거나 이익 추정치가 오르면 2차 30%
- 가격 추세가 돌아서면 3차 30%
- 종목당 최대 15%, 같은 테마 합계 최대 30%

## 재검토·매도

- 촉매가 취소되거나 1년 이상 밀리면 재검토
- F-점수가 4 이하로 떨어지면 비중 축소
- 악재가 회사 고유 문제로 바뀌면(소송·규제·회계) 재검토
- 안전마진이 0 이하가 되면(적정가치 도달) 분할 익절

지수 ETF 적립(나스닥100 등)은 점수와 무관하게 별도 규칙으로 계속 사 모아요.

## 근거 연구

### Contrarian Investment, Extrapolation, and Risk
Lakonishok·Shleifer·Vishny, 1994 (NBER WP 4360)

현금흐름 대비 주가가 낮고 과거 성장이 낮던 가치주가 인기주보다 연 8.7%p 높은 수익. 투자자가 과거 성장을 미래로 과하게 연장해서 생긴 현상이고 위험 보상이 아니었음.

→ 가치·비관 과잉 점수의 근거

[원문](https://www.nber.org/papers/w4360.pdf)

### Does the Stock Market Overreact?
De Bondt·Thaler, 1985

3년 누적 패자 종목이 승자 종목보다 이후 36개월간 24.6%p 높은 수익. 1년짜리 패자에서는 반전이 나타나지 않았음.

→ 최근 단기 급락보다 3~5년 부진을 비관 과잉으로 봄

[원문](https://alphaarchitect.com/quantitative-momentum-research-long-term-return-reversal/)

### Stock Returns After Major Price Shocks: The Impact of Information
펜실베이니아대 와튼 재무학과 연구

정보(애널리스트 의견 변화 등)를 동반한 급락은 같은 방향으로 계속 흐르고, 정보 없는 급락은 반전됨. 투자자는 펀더멘털 뉴스에는 덜 반응하고 그 밖의 충격에는 과잉 반응.

→ 악재 성격 점수의 근거. 회사 고유 악재 중이면 기다림

[원문](https://repository.upenn.edu/fnce_papers/387)

### Value Investing: The Use of Historical Financial Statement Information
Piotroski, 2000

고PBR 대비 저평가 종목 중 F-점수 8~9점은 시장 대비 +13.4%, 0~1점은 −9.6%로 연 23%p 차이. 저점수 기업은 실적 부진 상장폐지 확률이 5배 이상.

→ 재무 품질 점수와 F-점수 3 이하 제외 필터

[원문](https://www.chicagobooth.edu/review/separating-winners-losers)

### Quality Minus Junk
Asness·Frazzini·Pedersen, 2019

수익성·성장·안전성이 높은 우량주가 더 안전하면서도 수익률이 높음(미국 4요인 알파 월 0.60%, 24개국 중 23개국에서 양수). 가치와 음의 상관이라 함께 쓰면 가치 투자가 좋아짐.

→ 싸면서 우량한 종목(QARP)을 우선

[원문](https://research-api.cbs.dk/ws/portalfiles/portal/60211462/lasse_heje_pedersen_et_al_quality_minus_junk_publishersversion.pdf)

### In Search of Distress Risk
Campbell·Hilscher·Szilagyi, 2006 (NBER WP 12362)

부채가 많고 적자이며 변동성이 크고 현금이 적은 부실 종목은 1981년 이후 비정상적으로 낮은 수익. 싸다고 부실주를 사면 보상받지 못함.

→ 부실 신호 사전 제외 필터

[원문](https://www.nber.org/papers/w12362)

### Value and Momentum Everywhere
Asness·Moskowitz·Pedersen, 2013

가치와 모멘텀은 상관계수 약 −0.6. 미국 주식 샤프지수가 가치 0.26, 모멘텀 0.45에서 둘을 섞으면 0.86으로 높아짐. 한국 시장(2001~2014)에서도 두 전략이 음의 상관을 보임(고승의, 2015).

→ 추세 확인 점수. 싸더라도 하락 추세가 꺾일 때 분할 진입

[원문](https://w4.stern.nyu.edu/facdir/lpederse/papers/ValMomEverywhere.pdf)

### 국내 상장기업 저평가에 관한 고찰
자본시장연구원 이슈보고서 24-31, 2024

한국 저PBR의 본질은 낮은 수익력과 주주환원이 반영된 적정 평가에 가깝고, PBR 하나로 저평가를 판단하기 어려움.

→ 가치 점수에서 PBR을 ROE·주주환원과 함께 판단

[원문](https://www.kcmi.re.kr/report/report_view?report_no=1811)

### 증권사 리포트: 현대로템·S-Oil
대신증권(2025.11.04), 유진투자증권(2025.11.04), 하나증권(2026.08.04)

현대로템은 방산 수익성(영업이익률 30% 내외)과 국내외 고속철 양산이 실적을 끌고, S-Oil은 샤힌 프로젝트(2026년 6월 기계적 준공)와 정제마진 강세가 핵심 촉매로 제시됨.

→ 촉매 점수에서 날짜가 특정된 발주·준공 일정을 높게

[원문](https://file.alphasquare.co.kr/media/pdfs/company-report/55585_Rotem_Results_Comment_251104_fix.pdf)
