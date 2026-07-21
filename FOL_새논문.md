# 새 논문 FOL (구상)
### K-ETS의 효과 — 무상할당 여부 및 기업규모(시가총액) 이질성 분석
*기존 논문(Park, Khue & Lee 2024)의 S1을 해체하여 확장*

---

## 0. 술어(Predicate) 정의
논의 영역(domain): 한국 상장기업 f

**[기존 술어 계승]**

| 술어 | 의미 |
|---|---|
| `ETS(f)` | f가 K-ETS 대상 기업이다 |
| `FreeAlloc(f)` | f가 배출권을 무상할당 받았다 |
| `ReduceEmit(f)` | f가 실제 탄소배출을 유의하게 감축했다 |
| `Windfall(f)` | f가 잉여 배출권 매각/무상할당으로 초과이익을 얻었다 |
| `Profit↑(f)` | f의 단기 수익성(ROA)이 상승했다 |
| `Beta↑(f)` | f의 체계적 위험(β)이 상승했다 |
| `Value↓(f)` | f의 장기 기업가치(Tobin's Q)가 하락했다 |

**[신규 술어 — 이질성 도입]**

| 술어 | 의미 |
|---|---|
| `Large(f)` | f가 대형 기업이다 (시가총액 기준 상위) |
| `NetLong(f)` | f가 배출권 순잉여(할당 > 실배출) 상태다 |
| `NetShort(f)` | f가 배출권 순부족(할당 < 실배출) 상태다 |
| `PassThrough(f)` | f가 규제비용을 제품가격에 전가할 수 있다 |
| `Coverage↑(f)` | f가 애널리스트·기관투자자 커버리지가 높다 |

---

## 1. 최상위 FOL (한 문장)

> **∀f [ ETS(f) → ( Effect(f) = g( FreeAlloc(f), Large(f), NetLong(f) ) ) ]**
> 즉, **∀f [ ETS(f) → ¬( 효과가 동질적이다 ) ]**

"모든 ETS 대상 기업 f에 대하여, ETS의 효과는 균일하지 않으며 무상할당 여부·기업규모·배출권 순포지션의 함수로 이질적으로 나타난다."

→ 기존 논문의 `ETS(f) → FreeAlloc(f)` (동질 전제)를 **부정**하는 것이 출발점.

---

## 2. 서브 일차논리 (Sub-FOL) — 연역적 배열

| # | Sub-FOL | 의미 / 기존 대비 |
|---|---|---|
| S1′ | ∀f [ ETS(f) → ( FreeAlloc(f) ∨ ¬FreeAlloc(f) ) ] | **[S1 해체]** 대상 기업이 모두 무상 수혜는 아니다 |
| S2′ | ∀f [ ( FreeAlloc(f) ∧ NetLong(f) ) → Windfall(f) ] | 무상할당+순잉여일 때만 초과이익 발생 |
| S3′ | ∀f [ ( FreeAlloc(f) ∧ NetShort(f) ) → ¬Windfall(f) ] | 순부족 기업은 오히려 매입비용 부담 |
| S4′ | ∀f [ Windfall(f) → Profit↑(f) ] | 초과이익만 수익성을 높인다 (S2′·S3′에서 분기) |
| S5′ | ∀f [ Large(f) → PassThrough(f) ] | 대형 기업은 비용 전가력이 크다 |
| S6′ | ∀f [ Large(f) → Coverage↑(f) ] | 대형 기업은 투자자 관심·커버리지가 높다 |
| S7′ | ∀f [ ( Large(f) ∧ PassThrough(f) ) → ¬Value↓(f) ] | 전가력이 가치하락을 완충 (규모의 방어효과) |
| S8′ | ∀f [ Coverage↑(f) → Beta↑(f) ] | 커버리지 높을수록 미래리스크가 β에 더 빨리 반영 |
| S9′ | ∀f [ ( Beta↑(f) ∧ ¬PassThrough(f) ) → Value↓(f) ] | 전가 못하는 기업만 가치하락 |
| S10′ | ∀f [ ETS(f) → ( Value↓(f) ⇔ ( ¬Large(f) ∨ NetShort(f) ) ) ] | **[종합]** 가치하락은 소형·순부족 기업에 집중된다 |

---

## 3. 연역 구조 (Tree)

```
                        ETS(f)  [효과 이질적]
             ┌───────────────┴───────────────┐
       [S1′] 무상할당 여부                  규모(시총) 축
        ┌────────┴────────┐          ┌────────┴────────┐
   FreeAlloc          ¬FreeAlloc  Large(f)          ¬Large(f)
   ┌────┴────┐                    ├─[S5′]PassThrough  │
[S2′]NetLong [S3′]NetShort        ├─[S6′]Coverage↑    │
 Windfall    ¬Windfall            │                   │
   │            │           [S7′]¬Value↓        (완충 없음)
[S4′]Profit↑  (비용부담)   [S8′]Beta↑              │
                              └────────┬──────────────┘
                                  [S9′/S10′]
                          Value↓ ⇔ (¬Large ∨ NetShort)
                          (가치하락은 소형·순부족에 집중)
```

---

## 4. 최종 사슬(Chain)

> **ETS(f)**  *(효과가 동질적이라는 전제 기각)*
> **⟹[S1′]** ( FreeAlloc(f) ∨ ¬FreeAlloc(f) )  *— 무상 여부로 1차 분기*
> **⟹[S2′/S3′]** ( NetLong→Windfall ) ∨ ( NetShort→¬Windfall )  *— 순포지션으로 2차 분기*
> **⟹[S4′]** Windfall(f) ⟹ Profit↑(f)  *(잉여 기업만 수익 상승)*
> **∧[S5′,S6′]** Large(f) ⟹ ( PassThrough(f) ∧ Coverage↑(f) )  *— 규모의 이중효과*
> **⟹[S8′]** Coverage↑(f) ⟹ Beta↑(f)  *(대형일수록 리스크 반영 빠름)*
> **⟹[S7′,S9′]** ( PassThrough → ¬Value↓ ) ∧ ( ¬PassThrough ∧ Beta↑ → Value↓ )
> **⟹[S10′]** **Value↓(f) ⇔ ( ¬Large(f) ∨ NetShort(f) )**

### 압축된 한 줄
> **∀f: ETS(f) → [ Effect(f) 는 (무상할당 × 순포지션 × 규모) 의 함수 ] → ( Value↓(f) ⇔ 소형 ∨ 순부족 기업 )**

---

## 5. 기존 논문 대비 핵심 차별점

| 축 | 기존 논문 | 새 논문 |
|---|---|---|
| S1 전제 | ETS → 무상할당 (동질 가정) | 무상 여부·순포지션으로 **분기** |
| Windfall | 정황(conjecture)으로만 주장 | 순잉여/순부족 **변수화하여 실증** |
| 규모(Size) | control 변수로만 사용 | **조절변수(moderator)** 로 승격 |
| 가치하락 대상 | treated 전체 균일 | **소형·순부족 기업에 집중** 되는지 검증 |
