---
layout: default
title: "Rams와 mirror-mind의 직접 접점"
---

# Rams와 mirror-mind의 직접 접점

이 문서는 Dieter Rams의 10원칙(Vitsoe 정본)과 그 배후의 책임 어휘를 mirror-mind 사상·agentic-engineering 운영·lighthouse 설계와 교차검증한다. Rams 쪽 기준은 honest, unobtrusive, environmentally-friendly, as little design as possible, useful, understandable, aesthetic, innovative, long-lasting, thorough down to the last detail이다. mirror-mind 쪽 기준은 `mirror-mind-principle.md`(4대 원칙·Co-actor), `agentic-engineering-principles.md`, lighthouse 정본(`projects/lighthouse/docs/principles.md` 외), 그리고 라인업 메모(frontier-watch, soulmate, co-agents, agentic-base)다.

핵심 결론을 먼저 말한다. Rams는 mirror-mind에 새 책임 차원을 추가한다. 인터페이스 표면이 시스템 내부 상태를 어떻게 정직하게 드러내는지에 대한 책임이다. 이 책임을 본문에서는 **표면 책임**이라 부른다. Engelbart는 작업 시스템의 회로(Artifacts·Language·Methodology·Training)를 정의했고, 이케다 료지는 미감·지각의 입자(layout·timing·system)를 정의했다. Rams는 그 사이에서 표면이 사용자에게 무엇을 말하고 무엇을 감추는지를 정의한다. 세 사람은 형제 관계가 아니라 직교 축이다. mirror-mind 라인업은 세 축 중 어디에 무게가 실리느냐에 따라 인스턴스가 달라진다.

같은 결론을 부정형으로 다시 말한다. Rams 원칙을 mirror-mind에 적용한다는 말은 "더 미니멀한 UI를 만든다"는 뜻이 아니다. 표면에서 시작해 시스템의 자원·시간·신뢰 마모까지 한 평면에 놓고 설계 책임을 진다는 뜻이다. Engelbart의 C activity(B를 개선하는 활동)가 자원을 무한히 쓰지 않을 책임, lighthouse propose 카드가 모르는 것을 모른다고 말할 책임, soulmate가 사용자 일상에 끼어드는 빈도를 스스로 제어할 책임이 모두 같은 명제의 변주다.

## 1. 삼각 모델 — 이케다·Engelbart·Rams의 직교 배치

세 인물 리서치를 같은 평면에 놓는다. 각자가 mirror-mind에 기여하는 입자가 다르고, 그 입자가 직교하기 때문에 한 인스턴스(예: lighthouse)에 셋이 동시에 들어갈 수 있다.

| 축 | 인물 | mirror-mind 기여 입자 | 주요 어휘 | 빠진 자리 |
|---|---|---|---|---|
| 미감·지각 | 이케다 료지 | 시각층·상호작용층·시스템층의 표현 변주 | 신호/노이즈, 미시/거시 동시 노출, 임계점 자극 | 시스템 운영·책임 |
| 작업 시스템 | Douglas C. Engelbart | H-LAM/T 4 결합, A·B·C 3층, Bootstrap, Co-evolution | Artifacts·Language·Methodology·Training | 표면 책임, LLM 비결정성 |
| 인터페이스 책임 | Dieter Rams | 표면 정직성·비침해성·환경성·최소성 | honest, unobtrusive, environmentally-friendly, as little design as possible | LLM 비결정성, 도구-주체 전이 |

세 축이 직교한다는 사실은 운영에서 한 가지 결과를 낳는다. 한 인스턴스를 평가할 때 세 축을 별개 차원으로 분리해 본다. lighthouse의 propose 카드 하나를 놓고도 이케다 축(밀도·타이밍·대비), Engelbart 축(어떤 activity층의 도구인가, B인가 A인가), Rams 축(이 카드가 모르는 것을 모른다고 말하는가, 사용자 주의를 침해하는가)을 따로 점검한다. lighthouse의 release verdict가 Intent·AC trace·Aspect 세 차원을 분리해 표시하는 패턴과 같다. 결합된 한 줄로 환원하지 않는다.

이 세 축이 한 라인업에 어떻게 분산 적용되는지의 첫 매핑은 다음과 같다.

| 라인업 | 미감 축 (이케다) | 시스템 축 (Engelbart) | 책임 축 (Rams) |
|---|---|---|---|
| lighthouse | propose 카드 밀도, reaction 타이밍 | Story Chain·Evidence Ledger·A/B/C 운영 | confidence indicator, A activity 주권 보존 |
| frontier-watch | signal/event/thread 입자 표시 | thread = B activity 도구 후보 | 검증/추측 표면 구분 |
| soulmate | 대화 리듬, 침묵의 사용 | 사용자의 일상이 곧 사용자의 A activity | unobtrusive — 끼어드는 빈도·강도 제어 |
| co-agents | 다수 에이전트 표시의 일관성 | 좁은 자기개선 하네스의 집합 | as little design as possible — 개별 하네스 경량 |
| agentic-base | 시드의 미감 (도메인-중립) | C activity 도구의 시드 | as little design as possible — `.mjs` 유지, 의존성 최소 |

이 표는 단정 매핑이 아니라 첫 좌표 제안이다. 라인업이 자라면 다른 칸이 채워진다.

## 2. Engelbart × Rams 접점 — 같은 곳을 가리키는 4 명제

두 사람은 같은 시대(20세기 후반) 사람이지만 직접 만나지 않았다. 그러나 mirror-mind를 한 평면에 놓고 보면 네 곳에서 명확히 만난다. 각 접점에 대해 (a) 공명, (b) 충돌, (c) 빈자리 세 항목으로 정리한다. Engelbart 리서치 `04-mirror-mind-connections.md`의 패턴을 따른다.

### 2.1 Evidence ledger × honest design — 신뢰 지표의 디자인 책임

#### 공명

Engelbart의 Evidence Ledger는 "약속이 실제 runtime에서 달성된다는 증거를 ledger에 적어 둔다"는 운영 명제다. Rams의 honest는 "제품이 자기가 무엇인지를 표면에서 거짓말하지 않는다"는 디자인 명제다. SK 4(Phonosuper, 1956)의 투명 아크릴 덮개가 사상적 참조점이다. 턴테이블 기구의 작동을 가리지 않고 그대로 보여준다. 사용자가 기계를 신뢰할 근거를 표면이 직접 제공한다.

같은 명제의 lighthouse 인스턴스가 confidence indicator다. AI가 생성한 propose 카드 옆에 그 출처(어떤 evidence가 backing인가), 확신도(높음/모름/낮음), 검증 상태(verified/pending/unknown)를 사용자 표면에 그대로 노출한다. 그러면 Evidence Ledger의 내부 진실이 사용자 화면까지 그대로 옮겨진다. 두 사람은 같은 곳을 가리킨다. 시스템 내부의 신뢰 근거가 사용자 화면에서 끊기지 않고 그대로 보여야 한다.

#### 충돌

충돌은 honesty의 단위에서 생긴다. Rams는 산업 제품을 다루기 때문에 한 제품의 정직성을 출고 시점에 한 번 만들고 끝낸다. SK 4의 덮개는 출고 후 거짓말하지 않는다. mirror-mind의 LLM 출력은 매 turn 새로 생성된다. 같은 입력에 다른 출력이 나올 수 있고 confidence 자체가 비결정적이다. honest의 표현을 매 turn 다시 산출해야 한다.

lighthouse가 verdict trichotomy(met/not-met/unknown)를 두는 이유가 이 비결정성에 대한 응답이다. unknown은 중립이 아니라 blocking이다. 모름을 모름으로 표면에 표시해야 honest가 성립한다. Rams의 honest를 그대로 가져오면 "확신 있는 것만 말한다"로 약하게 읽힌다. mirror-mind의 honest는 더 강하다. 모르는 것을 모른다고 말한다. 표현 단위가 출고 시점 1회가 아니라 매 turn 반복이다.

#### 빈자리

confidence indicator의 디자인 언어가 mirror-mind에 아직 정의되어 있지 않다. unknown verdict의 시각 어휘, "AI가 모른다"의 사용자-facing 표현, 부분적 확신의 표시 방법을 정한 문서가 없다. lighthouse propose 카드에서 unknown verdict가 어떻게 보이는지에 대한 design contract가 없으면, 운영 측 verdict trichotomy를 아무리 엄격히 돌려도 사용자 화면까지 닿지 않는다. 후속 작업 1순위가 이 빈자리다.

### 2.2 A activity 주권 보존 × unobtrusive — 같은 명제의 두 어휘

#### 공명

Engelbart의 A·B·C 모델에서 lighthouse는 "A activity는 사용자가 시작한다"고 결정했다. 사용자가 검색·문서 열기·후속 액션을 시작하고, 에이전트는 현재 문서와 이벤트에 반응한다. 이렇게 A activity의 주권을 연구자에게 남기는 설계다(Engelbart 04 §2 공명점).

Rams의 unobtrusive("좋은 디자인은 침해하지 않는다")가 같은 곳을 가리킨다. 제품은 사용자가 자기 의도를 표현하는 도구다. 사용자의 의도 자체를 대신 만드는 주체가 아니다. 606 Universal Shelving은 벽에 박혀 있지만 사용자의 책과 물건을 위한 배경으로 사라진다. lighthouse의 reaction 카드도 사용자의 독해 흐름을 위한 배경으로 사라져야 한다.

두 어휘는 같은 명제다. 에이전트는 사용자의 시작 권한을 침해하지 않는다. Rams가 이 명제를 mirror-mind에 추가하는 가치는 번역 가능성에 있다. Engelbart의 A activity 어휘는 운영 절차에서만 쓰인다. unobtrusive는 표면 디자인 언어로 곧장 번역된다. 빈도·강도·시각 무게가 모두 unobtrusive의 측정 차원이다.

#### 충돌

충돌은 Co-actor 야망에서 생긴다(Engelbart 04 §5 충돌점과 같은 자리). Rams의 unobtrusive는 도구의 어휘다. 도구는 사용자가 부를 때만 등장한다. Co-actor는 "독립된 행위 주체"라 부르기 때문에, 사용자가 부르지 않아도 선제적으로 제안하는 맥락적 자율성을 가진다(mirror-mind-principle 4).

Rams 원칙을 강하게 적용하면 Co-actor 4번 원칙과 즉각 충돌한다. Co-actor가 자율적으로 끼어들 때마다 unobtrusive를 위반한다고 읽힌다. 이 충돌은 해소가 아니라 명시로 답한다. Co-actor의 자율성은 unobtrusive의 정도(빈도·강도·시각 무게) 안에서 행사된다. lighthouse 현재 정본이 "agent는 free-chat 하지 않고 current document와 [system] events에 반응한다"고 못박은 결정이 이 명시의 한 형태다.

#### 빈자리

mirror-mind에 "에이전트가 끼어드는 빈도·강도"를 잴 어휘가 없다. lighthouse의 ambient presence는 low-attention activity signal로 분리되어 있지만, propose 카드의 visual weight, reaction의 시간 간격, system event의 trigger threshold가 명시되어 있지 않다. soulmate처럼 일상에 들어가는 라인업에서는 이 빈자리가 즉시 제품 실패로 이어진다. unobtrusive의 측정 가능한 정의가 라인업별로 필요하다.

### 2.3 C activity × environmentally-friendly — 자원 마모의 누적

#### 공명

Engelbart의 C activity(B를 개선하는 활동)는 회고·정합성 점검·재학습 같은 활동이다. Rams의 environmentally-friendly("좋은 디자인은 환경을 보호한다")는 1970년대 석유 위기를 거치며 강화된 원칙으로, 제품이 사용하는 자원과 발생시키는 폐기물에 대한 책임이다.

두 원칙을 한 평면에 놓으면 새로운 명제가 보인다. C activity는 자원 마모를 일으킨다. 회고를 매주 한다는 말은 시간을 쓴다는 말이고, 정합성 점검을 매 turn 돌린다는 말은 연산을 쓴다는 말이고, 재학습을 한다는 말은 사용자의 인지 부담을 쓴다는 말이다. Engelbart는 1991년 Bootstrapping 보고서에서 C activity를 *permanent and highly-coordinated*라는 형용사로 묶었지만, 그 비용은 명시하지 않았다.

Rams의 environmentally-friendly를 mirror-mind 어휘로 옮기면 **프로세스적 폐기(iterative waste of process)**라는 개념이 떠오른다. 같은 도구의 같은 운영을 반복해도 회고·점검·재학습이 누적 비용을 만든다. lighthouse의 quality gate, mission-control 점검, codex 다차수 리뷰가 모두 C activity다. 각각 시간·연산·집중이라는 명확한 자원을 쓴다.

#### 충돌

충돌은 Engelbart가 C를 무조건 좋은 것으로 보는 데서 생긴다. 그의 1968 demo와 1991 보고서에서 C activity는 거의 "더 많을수록 좋다"는 톤으로 다뤄진다. Rams 어휘를 들이대면 그 가정이 깨진다. C activity도 자원을 누적해 어느 임계 이후 A activity를 침식한다.

mirror-mind 안에 이 충돌의 신호가 이미 있다. 재영의 P0("적은 시간 × 더 좋은 결과 + 남는 시간 사고 활동")는 C activity의 비용을 정확히 의식한 운영 명제다. "AI 생산성 휘둘리지 말 것"도 같은 자리다. Engelbart 어휘만으로는 이 명제의 출처를 설명하기 어렵다. Rams의 environmentally-friendly가 그 자리를 채운다.

#### 빈자리

C activity 비용을 잴 어휘가 mirror-mind에 없다. 회고를 얼마나 자주, 얼마나 길게 해야 하는가. 정합성 점검을 매 turn 돌릴지 매주 돌릴지를 무엇으로 판단하는가. lighthouse의 mission-control 게이트는 "baseline 기준 신규 critical 0"이라는 임계를 두지만, 게이트 자체의 운영 비용에 대한 임계는 두지 않는다. 후속 작업 후보로 C activity 자원 마모 지표를 둔다.

### 2.4 R5 self-hosting × as little design as possible — 하네스 최소화

#### 공명

Engelbart의 R5(self-hosting, Engelbart 02·04에서 추출된 11 조건 중 하나)는 "자기 제품으로 자기 제품의 개선 활동을 운영한다"는 임계점이다. dogfooding(자기 제품을 자기가 쓴다)보다 한 단계 더 나아간 상태다. B와 C activity 자체가 그 제품 위에서 돈다.

Rams의 as little design as possible("작은 디자인이 좋은 디자인이다")은 표면 어휘로 보이지만, mirror-mind 어휘로 옮기면 하네스 최소화 원칙이 된다. 자기 제품으로 자기 제품을 운영하되, 그 운영 자체가 가벼워야 한다. 무거운 self-hosting은 운영 비용이 누적되어 R5의 효용을 깎는다.

agentic-base의 가벼운 베이스 정신(memory `feedback_lightweight_base`)이 정확히 이 자리에 선다. "라이트하우스의 무거운 구현(tsx + TypeScript 기반 mc CLI)을 그대로 따라가지 않는다", ".mjs 유지, 의존성 최소"가 Rams의 as little design as possible과 직접 정합한다.

#### 충돌

충돌은 lighthouse 자체가 보여준다. lighthouse는 mission-control, Story Chain, Evidence Ledger, Aspect, release verdict 같은 무거운 C activity 인프라를 가졌다. R5 self-hosting을 위해 이런 인프라가 필요하다고 본 결정이다. as little design as possible을 강하게 적용하면 이 인프라 대부분이 과잉으로 읽힌다.

해소가 아니라 명시로 답한다. lighthouse는 실제 제품이라 무거운 의존성을 가진다(`feedback_lightweight_base`에 명시됨). agentic-base는 시드라 가벼움을 유지한다. 두 라인업에 같은 원칙을 다른 정도로 적용하자는 합의가 이미 mirror-mind 안에 있다. Rams 어휘는 이 합의를 명시적인 원칙 언어로 끌어올린다.

#### 빈자리

라인업별로 as little design as possible의 임계가 명시되어 있지 않다. lighthouse는 어디까지 무거워도 되는가. soulmate는 어디까지 가벼워야 하는가. frontier-watch는 lighthouse의 무거움을 따라갈 것인가 agentic-base의 가벼움을 따라갈 것인가. 라인업별 무게 표가 mirror-mind 안에 없다. 빈자리로 남는다.

## 3. lighthouse / mirror-mind 라인업 시사

Rams 원칙을 mirror-mind 라인업에 직접 적용했을 때의 운영 명제를 라인업별로 짧게 둔다. 깊이보다 폭을 본다.

### 3.1 lighthouse

| Rams 원칙 | 운영 명제 |
|---|---|
| honest | propose 카드 옆에 confidence indicator를 표시한다. unknown verdict는 표면 시각 언어로 노출된다 — 중립 아닌 blocking 신호. |
| honest | AI 코멘트에 "모르겠다" 모드를 1급 시민으로 둔다. 추측을 단정으로 표시하지 않는다. |
| unobtrusive | reaction 카드의 visual weight, 시간 간격, system event trigger threshold를 명시한다. ambient presence와의 분리는 유지하되 정도 정의가 필요. |
| as little design as possible | Story Chain 정합성 점검의 "less, but better" 임계를 둔다. 모든 promise를 점검하지 않고 baseline 변동분만 점검. 이미 mission-control이 이 방향. |
| environmentally-friendly | C activity 비용 측정 — quality gate 운영 시간, codex 다차수 리뷰 회수, 회고 시간을 기록. 임계를 두고 초과 시 게이트 자체를 의심. |
| thorough down to the last detail | release verdict 세 차원 분리(Intent·AC trace·Aspect)는 이미 이 원칙의 인스턴스. 결합된 한 줄로 환원하지 않는 운영을 유지. |

가장 즉시 효용이 큰 명제가 confidence indicator 디자인이다. lighthouse의 verdict trichotomy가 사용자 화면까지 끊기지 않고 닿는 첫 표현 surface다.

### 3.2 frontier-watch

| Rams 원칙 | 운영 명제 |
|---|---|
| honest | signal/event/thread 3입자에 검증 상태를 표면에 표시. "검증된 signal" vs "추측 thread"가 시각적으로 구분되어야 한다. |
| useful | thread는 사용자의 무슨 B activity를 돕는가를 명시. 단순 정보 피드가 아니라 "다음 판단을 더 잘 내리게 한다"가 thread의 단위. |
| understandable | 4축(카테고리·주체·시간·해석) 중 해석 축은 누가 한 해석인지 명시 — AI 해석인가 큐레이터 해석인가. honest의 확장. |

frontier-watch는 현재 컨셉 단계라 운영 명제가 추상적이다. 그러나 honest 원칙은 컨셉 단계부터 들어가야 한다. 검증/추측의 표면 구분을 나중에 끼워 넣으면 늦다.

### 3.3 soulmate / co-agents

| Rams 원칙 | 운영 명제 |
|---|---|
| unobtrusive | 끼어드는 빈도·강도·시간대의 자기 제어. 사용자가 명시하지 않은 침묵 시간대를 추정하고 지킨다. |
| useful | "활동 친구"의 단위가 정보 제공이 아니라 사용자가 무엇을 더 잘하게 되는가. lighthouse의 augment/replace rubric을 일상 활동 단위로 확장. |
| as little design as possible | co-agents의 개별 하네스를 좁고 가볍게. 범용성은 집합에서 창발(`project_co_agents`의 정의). 개별 하네스를 무겁게 만들지 않는다. |
| long-lasting | 사용자의 자기 표현·관계·관심사를 모델링하되, 일시적 트렌드에 흔들리지 않는 모델 — soulmate가 광고형 추천 시스템이 되지 않는 임계. |

soulmate에서 unobtrusive는 단순 디자인 권고가 아니라 제품 생존 조건이다. 일상에 들어가는 라인업이 끼어드는 정도를 잘못 잡으면 제품이 즉시 거부된다.

### 3.4 agentic-base

| Rams 원칙 | 운영 명제 |
|---|---|
| as little design as possible | `.mjs` 유지, TypeScript 의존성 추가 안 함, 코드는 init 후 사람이 채움. 이미 `feedback_lightweight_base`로 명시된 원칙. Rams 어휘로 추인된다. |
| innovative | 새 라인업의 시드이므로, 기존 라이트하우스를 "표본"으로 두되 단순 복제가 아닌 재구성. 표본 따라가기가 innovative를 막지 않도록. |
| useful | 도메인-중립 시드 — 도메인 콘텐츠는 시드하지 않는다. 사용처에서 채워야 useful이 결정된다. |

agentic-base는 이미 Rams 정신에 가장 가까운 라인업이다. 추가 명제보다 기존 운영을 Rams 어휘로 추인하고 다른 라인업이 이를 참조하게 만드는 효용이 크다.

## 4. 빈자리·후속 작업

### Rams가 채우지 못하는 자리

Rams는 산업디자인 시대 사람이라 몇 곳에서 mirror-mind 문제에 직접 응답하지 못한다.

| 빈자리 | 내용 |
|---|---|
| LLM 비결정성·환각 | Rams의 honest는 출고 시점 1회 정직성이다. 매 turn 재산출되는 비결정 출력의 정직성에 대한 어휘가 없다. mirror-mind의 verdict trichotomy(특히 unknown blocking)가 이 자리를 직접 채우지만, Rams 어휘로는 표현되지 않는다. |
| "Material로서의 AI" | 원안 글의 비유 — "AI를 디자인 재료처럼 다룬다". Rams 본인의 어휘가 아니라 후세대 해석. 그 비유가 얼마나 정당한지(나무·금속처럼 안정된 material인가, 매 turn 변하는 비결정 material인가) 별도 검토 필요. mirror-mind-principle.md에 "Material로서의 AI"를 도입할지 여부는 합의 게이트. |
| Co-actor 권한 매트릭스 | Rams는 도구를 도구로 보는 시대 사람이라, 도구가 자기 권한을 행사하는 단계에 대한 어휘가 없다. Engelbart 04에서 짚힌 같은 빈자리. Rams는 이 자리에서 augment하지 못한다. |
| 사용자 학습 곡선 | Rams의 understandable은 "설명서 없이 이해된다"는 강한 명제다. mirror-mind 라인업(특히 lighthouse)은 chord keyset처럼 학습이 필요한 면이 있다. understandable이 학습 없는 즉시성을 요구하면 일부 라인업이 위반된다. 어느 정도까지가 understandable인지 라인업별 임계가 필요. |
| 환경의 단위 | Rams의 environmentally-friendly는 물리적 자원(전력·재료)을 가리킨다. mirror-mind는 자원이 시간·연산·인지 부담·신뢰다. 같은 어휘로 묶을지 분리할지 판단 필요. |

### 후속 작업 후보

Engelbart 04의 후속 작업 목록과 합쳐서 우선순위는 재영이 가른다. 여기에서는 Rams 발 후속 후보만 둔다.

1. **lighthouse propose 카드 confidence indicator 설계** — Rams honest × Engelbart Evidence Ledger × 이케다 미감 축의 교차점. verdict trichotomy(특히 unknown)가 사용자 화면 시각 언어까지 끊기지 않고 닿는 첫 인스턴스. 디자인 contract 1차 초안 작성.
2. **라인업별 정직성 가이드 카드** — lighthouse / frontier-watch / soulmate / co-agents / agentic-base 각각에 대해 "honest의 단위가 무엇인가", "unknown을 어떻게 표시하는가"를 정리한 짧은 운영 카드 시리즈. 5월 화두 "연구 전문성 강화"의 직접 산출.
3. **"Material로서의 AI" 어휘의 mirror-mind-principle.md 도입 여부 판단** — 도입한다면 4대 원칙에 5번이 추가되는가, 1번(목적의 내재화) 주석으로 들어가는가. 핵심 문서 수정이라 합의 게이트.
4. **unobtrusive의 측정 가능한 정의** — 빈도·강도·시각 무게·시간대를 라인업별로 임계화. soulmate에서 가장 먼저 필요. lighthouse의 ambient presence와 reaction 카드의 임계 차이를 명시하는 일도 같은 작업.
5. **C activity 자원 마모 지표** — Engelbart 04 후속 작업 6번(C activity 성과 지표)과 짝. 성과만이 아니라 비용도 측정. lighthouse mission-control 게이트 운영 시간이 첫 데이터 후보.
6. **라인업별 "as little design as possible" 임계 표** — lighthouse(무거움 허용 한계) / agentic-base(가벼움 유지 한계) / soulmate·frontier-watch(중간) 임계 표. 새 라인업 시작 시 첫 참조 문서.
7. **삼각 모델 평가 체크리스트** — 라인업·기능·인스턴스를 평가할 때 이케다·Engelbart·Rams 세 축을 분리해 점검하는 짧은 체크리스트. 디자인 리뷰·codex 다차수 리뷰의 한 입력.

### Open Questions

- Rams의 honest를 mirror-mind-principle.md의 5번 원칙(또는 4번 맥락적 자율성의 주석)으로 추가할지, 별도 인터페이스 책임 문서로 분리할지.
- "Material로서의 AI" 비유가 LLM 비결정성을 가리는가 드러내는가. 원안 글의 비유는 가려질 위험이 있다.
- lighthouse의 confidence indicator가 verdict trichotomy의 표면 노출이라면, 그 시각 언어를 이케다 미감 축으로 디자인할 것인가 Vignelli 명확성 축으로 디자인할 것인가. 두 미감이 다른 답을 줄 가능성.
- Co-actor 4번 원칙(맥락적 자율성)과 Rams의 unobtrusive 충돌의 해소가 "정도 명시"로 충분한가, 더 강한 재정의가 필요한가.
- agentic-base의 가벼운 베이스 정신을 Rams의 as little design as possible로 추인하는 것이 정합적인가, 다른 명제(예: 시드의 도메인-중립성)와 섞이는가.

---

이 문서는 Engelbart 04와 같은 패턴으로 작성되었다. 시리즈의 다른 산출물(01: 1차 자료, 02: AI 번역, 03: 동시대 사례)이 도착한 뒤, 그 결과를 인용으로 더해 보강할 자리가 본문 각 절에 열려 있다. 특히 02의 "프로세스적 폐기" 정의, 03의 Brauncore/Teenage Engineering 사례는 §2.3·§2.4의 빈자리에 직접 들어갈 후보다.
