---
layout: default
title: "Douglas C. Engelbart 리서치 — 통합 해석"
---

# Douglas C. Engelbart 리서치 — 통합 해석 (초안)

**작성일**: 2026-05-08 (W19)
**목적**: 5월 화두 "연구 전문성 강화"의 첫 인스턴스. mirror-mind 사상의 직계 조상을 1차 자료에서 복원하고, Co-actor·agentic-engineering·lighthouse 설계와 직접 잇기.
**진행 방식**: 클코 서브에이전트 3 + codex exec 메타 1, 병렬 실행 (≈ 217s 가장 오래 걸린 축 기준).
**상태**: 4 산출물 완료. 본 README는 통합 해석 초안 — 재영 검토 후 교정.

---

## 산출물 인덱스

| 파일 | 축 | 한 줄 요약 |
|---|---|---|
| `01-augmentation-vs-automation.md` | Engelbart vs 자동화 사조 | Augmentation/Automation 분기는 효율의 정도가 아니라 *주어*가 다른 두 명제. 같은 ARPA 자금 안의 두 줄기. LLM 시대에 같은 분기선이 재연. |
| `02-augmentation-conditions.md` | 증강 시스템 설계 조건·조립 | H-LAM/T(Artifacts/Language/Methodology/Training) 4 결합 + A·B·C 3층 + Bootstrap. 1962·1968·1991 1차 자료 직접 인용. |
| `03-limits-and-critique.md` | 한계·비판·실패한 이유 | PARC는 표면(마우스·GUI)만 가져가고 회로(B/C·Bootstrap·viewspecs)를 떼냈다. chord keyset 실패는 도구 단독 실패가 아니라 사회 인프라 부재. |
| `04-mirror-mind-connections.md` | mirror-mind 직접 접점 (codex 메타) | 5 명제(H-LAM/T↔Model+Harness, A/B/C↔mirror-mind 운영, Bootstrap↔lighthouse, Co-evolution↔Co-actor, Augment/Replace↔Harness)를 공명/충돌/빈자리 3 항목으로 정리. |

---

## 통합 명제 — 4 산출물이 같은 곳을 가리킨다

> **Co-actor는 Augmentation의 부정이 아니라 LLM 시대로 갱신된 Augmentation이다.**
> Harness는 H-LAM/T의 21세기 재기술이다. Lighthouse는 A activity를 빠르게 하는 도구가 아니라 **B activity를 가능하게 하는 도구**로 재정의되어야 한다. Augment vs Replace의 분기는 모델 능력이 아니라 **하네스 설계**에서 갈린다.

이 명제는 4 산출물에서 각각 별개로 도착했다.

- **A1**: "Co-actor의 어긋남은 LLM이 만든 새 사실에서 옴 — Engelbart Artifact의 신뢰 모델 '내가 누르면 작동한다'는 LLM 비결정성 위에서 모자라다. Augmentation의 부정이 아니라 LLM 시대로 갱신된 Augmentation."
- **A2**: H-LAM/T의 4 요소가 Harness의 분해와 정합. Engelbart 본인 명시 6 + 리서치 추출 5 = **증강 도구 11 조건**. 그 중 **R5(self-hosting)** 가 dogfooding과 갈라지는 임계점.
- **A3**: "LLM 시대 두 독해는 모델 능력이 아니라 하네스 설계에서 갈린다. 수용 모드는 B/C activity 회로를 끊고, 관찰·재구성·재지시 모드는 살린다." → **lighthouse는 A activity 도구가 아니라 B activity 도구**.
- **04 codex**: "Engelbart는 도구를 도구로 보았고 mirror-mind는 AI를 독립된 주체로 본다. 하지만 완전한 존재론적 전환으로 보면 과하다 — Co-actor는 법적·윤리적 동등 주체가 아니라 **협업 인터페이스에서 수동 도구처럼 대하면 실패한다는 운영 명제**."

네 축이 서로 다른 자료에서 출발해 같은 결론에 도달한 것이 통합의 근거다.

---

## 핵심 발견 묶음

### 1. 사상사적 분기는 효율이 아니라 *주어*

자동화: 사람이 하던 일을 기계가 한다 — 사람의 자리는 줄어든다.
증강: 사람이 더 어려운 일을 할 수 있게 된다 — 사람의 자리는 *복잡해진다*.

Licklider가 ARPA IPTO에서 SRI(Engelbart)와 SAIL(McCarthy)을 동시에 부양했다는 사실(Markoff 2005)은 두 라인이 적대 진영이 아니라 *한 부처의 두 명제*임을 보여준다. mirror-mind는 후자(Engelbart 라인)의 같은 쪽에 서 있다.

### 2. Engelbart의 단위는 도구가 아니라 H-LAM/T 시스템

마우스·NLS는 "도구"가 아니라 시스템 안의 한 자리(Artifact). 그 자리의 변경은 다른 자리(Language·Methodology·Training)의 변경을 *강제한다*. **도구만 바꾸면 brick-pencil**.

mirror-mind에서:
- Artifacts ↔ 코드베이스·Story Chain·Evidence Ledger·memory·admin surface
- Language ↔ Promise·Aspect·Verdict·Co-actor·Harness 같은 통제 어휘
- Methodology ↔ contract→propagation→enforcement→verification, sample-first, 작업 시작·종료
- Training ↔ AGENTS.md·skill·read order (단, **사람의 훈련은 빈자리**)

### 3. A·B·C 3층과 Bootstrap

1991년 Bootstrapping 보고서의 형용사가 결정적이다 — B는 "permanent and highly-coordinated", C는 "explicit and on-going". 회고를 *가끔* 하는 게 B가 아니다. 회고를 하는 *방식 자체*를 갱신할 자원이 없으면 C가 아니다.

mirror-mind 매핑:
- A: lighthouse·soulmate·agentic-base·youngcompany 블로그
- B: operations.md, agentic-engineering-principles.md, 주간 플랜, 회고, 품질 게이트, codex 다차수 리뷰
- C: mirror-mind-principle.md, AGENTS.md, agents-md-writing-guide.md, memory-architecture.md (핵심 문서 합의 게이트가 *highly-coordinated*에 부합)

**Bootstrap = C가 같은 도구 위에서 돌아갈 때**. dogfooding(자기 제품을 자기가 쓴다)과 self-hosting(자기 제품으로 자기 제품의 개선 활동을 운영한다)의 구분이 이 지점.

### 4. PARC의 흡수는 단순화가 아니라 사용자 모델의 교체

Bardini *Bootstrapping*(2000)의 진단: NLS는 "사용자를 발명한다(도구가 사람을 끌어올린다)" 위에 섰고, PARC는 "현재 있는 사람을 받아들인다"는 인류학으로 갈아탔다. **같은 기술을 다른 인류학에 올린 것**. mirror-mind/lighthouse가 빠질 수 있는 같은 함정.

### 5. chord keyset 실패는 사회 인프라 부재

바이올린에는 음악원·강사·평가 체계가 있다. 컴퓨팅에는 없었다. 이 구분이 (a) 비판의 정당성("사람들이 안 배웠다")과 (b) 한계("사회가 학습을 받칠 인프라를 만들지 않기로 했다")를 동시에 설명. mirror-mind 안의 AGENTS.md·operations.md·기억 시스템·주간 플랜은 그 인프라 자리.

### 6. Kay의 "violin"은 변호가 아니라 진단

Kay는 Engelbart의 "co-evolution"을 "literacy"로 개명하면서 사회적 단위를 **조직→개인으로 한 단계 내렸다**. Engelbart가 Collective IQ를 보았다면 Kay는 개인의 인지 도구를 보았다. **Engelbart 계보 안의 가장 큰 분기점**. mirror-mind는 Kay 쪽이 아니라 Engelbart 쪽(조직 단위)에 가깝다 — operations·기억 시스템·핵심 문서 합의가 그 증거.

### 7. LLM 시대의 두 독해 — 능력이 아니라 하네스에서 갈린다

- 낙관: chord keyset의 진입장벽이 자연어 인터페이스로 우회된다.
- 비관: LLM이 답을 즉시 주면 B/C activity 회로가 끊긴다.

차이는 모델 안에 있지 않고 **하네스 안에 있다**. 사용자가 LLM 출력을 "수용 모드"로 받으면 augment는 일어나지 않고, "관찰·재구성·재지시 모드"로 받으면 일어난다. P0(속도가 아닌 통제력) 작업 방식의 Engelbart 어휘 번역.

---

## 빈자리·임계점

4 산출물에서 일관되게 짚힌 mirror-mind의 빈자리:

| 빈자리 | 내용 | 출처 |
|---|---|---|
| **R5 self-hosting** | lighthouse가 lighthouse 자신의 B/C를 lighthouse로 운영하는 단계 — Bootstrap의 임계점. 현재는 dogfooding(B)에 머물러 있다. | A2, 04 |
| **사람의 Training 층** | 좋은 승인·반려·evidence 판독·프롬프트 제출 습관. 에이전트 훈련은 AGENTS.md·skill로 일부 해결됐지만 사람 훈련은 약함. | A2, 04 |
| **Co-actor 권한 매트릭스** | "독립된 행위 주체"라는 철학 선언을 어디서 주체·어디서 실행자인지 *운영 가능한 권한 모델*로 낮추기. agentic-engineering의 4 권한(Human/Agent/System/Evaluator)과 연결. | 04 |
| **augment/replace 판정 rubric** | 제품 기능별로 "어떤 능력을 증강하는가 / 어떤 대체 위험이 있는가 / 행동 증거로 무엇을 볼 것인가". slop 재검토와 직결. | 03, 04 |
| **C activity 성과 지표** | 정합성 점검·배선 검증·Evidence Ledger·회고가 실제로 어떤 실패를 줄였는지의 측정. 미배선 발견 수, unknown verdict 감소, promise drift 차단 사례. | 04 |
| **lighthouse 재정의** | A activity 도구(연구를 빠르게)가 아니라 **B activity 도구(연구 방식을 개선)**로 재정의 가능한가. 정체성 #134 작업과 직결. | 03 |

---

## 후속 작업 제안 (재영 검토용)

기존 5월 화두("연구 전문성 강화")의 후속 인스턴스 후보. 재영이 가르고 우선순위 정함.

1. **H-LAM/T × Harness 대응표 작성** — `agentic-engineering/` 안 또는 별도 문서에 현재 파일·스크립트·스킬·훈련 공백을 4 칸에 매핑. **Training 칸의 빈자리가 가장 잘 보이는 작업**.
2. **lighthouse 재정의 검토** — "A activity 도구 → B activity 도구"로 재정의 가능한가. 정체성 #134(통제감 축 재작성)와 합쳐서 진행. *Engelbart 시리즈를 lighthouse 통제감 축에 직접 인용 가능*.
3. **augment/replace 판정 rubric** — lighthouse propose 카드·검색 설명·gap network·citation lineage 각각에 대해 행동 증거 기반 rubric. #133(비공개 테스트 행동 관찰 체크리스트)와 자연스럽게 합쳐짐.
4. **Co-actor 권한 매트릭스** — `mirror-mind-principle.md` 또는 `agentic-engineering/boundaries.md`에 권한 분해 절 추가. 핵심 문서 수정이라 *합의 게이트*.
5. **사람 Training 층 — "운영 카드" 시리즈** — 좋은 승인·반려·evidence 판독·프롬프트 제출 습관을 짧은 카드로. 5월 화두 "연구 전문성 강화"의 직접 산출.
6. **C activity 성과 지표 — 회고 메트릭 시범** — 1주(W19) 회고에서 미배선 발견 수·unknown verdict 감소·promise drift 차단 사례를 기록 시작.
7. **블로그 글감 — "Engelbart, LLM 시대로 갱신된 Augmentation"** — youngcompany 블로그 1편. 4 산출물의 통합 명제를 자연석 글쓰기로. *연구 전문성 강화 + 외부 발신 동시*.

---

## Open Questions

- Co-actor 원칙이 "법적·윤리적 동등 주체"라는 의미가 아니라 "운영 명제(수동 도구처럼 대하면 실패한다)"임을 `mirror-mind-principle.md` 본문에 명시할 것인가, 별도 권한 매트릭스 문서로 분리할 것인가.
- "lighthouse는 B activity 도구"라는 재정의가 통제감 축(#134)과 일치하는가, 아니면 다른 축인가.
- R5 self-hosting을 lighthouse에 적용하는 단계는 무엇인가 — workspace document를 lighthouse 자신의 회고·계획 운영에 쓰는 시도가 가능한가.
- Bardini의 "사용자 모델 교체" 진단이 lighthouse slop 재검토와 같은 위험을 가리키는가, 다른 위험을 가리키는가.
- Engelbart 시리즈를 1편 글로 묶을지(블로그), 시리즈로 풀지(연구 전문성 강화 한 달).

---

## 출처·메타

각 산출물에 1차 자료 출처가 붙어 있다. 공통 핵심:

- **Engelbart 1차 자료**: AHI 1962 (AUGMENT-3906), Bootstrapping the 21st Century 1991 (AUGMENT-132803), ABC Model 정본, 1968 Demo Interactive (Doug Engelbart Institute)
- **2차 사료**: Bardini *Bootstrapping* (2000), Markoff *What the Dormouse Said* (2005), Bret Victor *Future of Programming* (DBX 2013), Alan Kay *User Interface: A Personal View* (1989)
- **현대 접점**: Karpathy *Software 3.0* (YC AI Startup School 2025), Anthropic *Building Effective Agents*, *Measuring AI Agent Autonomy*

리서치 패턴 자체:
- 클코 서브에이전트(general-purpose) × 3 병렬 + codex exec(gpt-5.5) 메타 1 병렬 = 4축. 가장 오래 걸린 축 기준 ≈ 217s. 같은 폴더 다른 파일이라 충돌 없음.
- 4 축이 서로 모르는 채 같은 결론에 도달했다는 사실 자체가 통합 명제의 1차 검증. 메모리 시스템에 등록된 "3개 서브에이전트 병렬 + codex" 패턴(세션110·135)의 재인스턴스.
