# 기존 논문 FOL — Park, Khue & Lee (2024)
### "The effects of carbon emissions trading on profitability and value: Evidence from Korean listed firms"
*Journal of International Financial Management & Accounting*, 35(3), 760–799.

---

## 0. 술어(Predicate) 정의
논의 영역(domain): 한국 상장기업 f

| 술어 | 의미 |
|---|---|
| `ETS(f)` | f가 K-ETS 1차 대상(treated) 기업이다 |
| `FreeAlloc(f)` | f가 배출권을 100% 무상할당 받았다 |
| `ReduceEmit(f)` | f가 실제 탄소배출을 유의하게 감축했다 |
| `Disclose(f)` | f가 배출량을 의무 공시했다 |
| `Erating↑(f)` | f의 환경등급(E-score)이 상승했다 |
| `Windfall(f)` | f가 잉여 배출권 매각/무상할당으로 초과이익을 얻었다 |
| `Profit↑(f)` | f의 단기 수익성(ROA)이 상승했다 |
| `Beta↑(f)` | f의 체계적 위험(β)이 상승했다 |
| `FutureRisk(f)` | 미래 탄소가격·규제 강화에 대한 불확실성이 존재한다 |
| `Value↓(f)` | f의 장기 기업가치(Tobin's Q)가 하락했다 |

---

## 1. 최상위 FOL (한 문장)

> **∀f [ ( ETS(f) ∧ FreeAlloc(f) ) → ( ¬ReduceEmit(f) ∧ Erating↑(f) ∧ Profit↑(f) ∧ Beta↑(f) ∧ Value↓(f) ) ]**

"모든 기업 f에 대하여, f가 무상할당을 받은 ETS 대상 기업이라면, f는 배출을 감축하지 않고, 환경등급은 오르며, 단기 수익성은 상승하지만, 체계적 위험이 커져 장기 기업가치는 하락한다."

---

## 2. 서브 일차논리 (Sub-FOL) — 연역적 배열

| # | Sub-FOL | 의미 |
|---|---|---|
| S1 | ∀f [ ETS(f) → FreeAlloc(f) ] | 대상 기업은 무상할당을 받는다 |
| S2 | ∀f [ FreeAlloc(f) → ¬ReduceEmit(f) ] | 무상할당은 감축 유인을 제거한다 |
| S3 | ∀f [ ETS(f) → Disclose(f) ] | 대상 기업은 배출량 의무공시를 한다 |
| S4 | ∀f [ Disclose(f) → Erating↑(f) ] | 공시가 환경등급 상승을 낳는다 |
| S5 | ∀f [ FreeAlloc(f) → Windfall(f) ] | 무상할당은 초과이익을 창출한다 |
| S6 | ∀f [ Windfall(f) → Profit↑(f) ] | 초과이익은 단기 수익성을 높인다 |
| S7 | ∀f [ FreeAlloc(f) → FutureRisk(f) ] | 관대한 할당은 장래 축소 → 미래 리스크 발생 |
| S8 | ∀f [ FutureRisk(f) → Beta↑(f) ] | 미래 불확실성이 체계적 위험을 높인다 |
| S9 | ∀f [ Beta↑(f) → Value↓(f) ] | 체계적 위험 상승이 장기가치를 낮춘다 |
| S10 | ∀f [ ( Profit↑(f) ∧ Beta↑(f) ) → Value↓(f) ] | 단기수익 상승에도 리스크가 가치하락을 압도 |

---

## 3. 연역 구조 (Tree)

```
                     ETS(f)
        ┌──────────────┼──────────────┐
   [S1] FreeAlloc     [S3] Disclose   (동시 발생)
        │                  │
   ┌────┴─────┐       [S4] Erating↑   ← 환경등급 상승 갈래 (실질 감축과 분리)
   │          │
[S2]¬Reduce  [S5]Windfall
 (배출↓실패)      │
             [S6]Profit↑ ─────────┐
   [S7]FutureRisk                 │
        │                         │
   [S8]Beta↑ ────────┐            │
        │            └──[S10]───→ Value↓
   [S9]Value↓             (수익↑ ∧ β↑ ⇒ 가치↓)
```

---

## 4. 최종 사슬(Chain)

> **ETS(f)**
> **⟹[S1]** FreeAlloc(f)
> **⟹[S2]** ¬ReduceEmit(f)  *(배출 감축 실패)*
> **∧[S3→S4]** Disclose(f) ⟹ Erating↑(f)  *(그럼에도 환경등급은 상승)*
> **⟹[S5]** Windfall(f)
> **⟹[S6]** Profit↑(f)  *(단기 수익성 상승)*
> **∧[S7]** FutureRisk(f)
> **⟹[S8]** Beta↑(f)  *(체계적 위험 상승)*
> **⟹[S9]** Value↓(f)
> **⟹[S10]** ( Profit↑(f) ∧ Beta↑(f) ) ⟹ **Value↓(f)**

### 압축된 한 줄
> **∀f: ETS(f) → FreeAlloc(f) → [ (¬ReduceEmit ∧ Disclose→Erating↑) ∧ (Windfall→Profit↑) ∧ (FutureRisk→Beta↑) ] → Value↓(f)**
