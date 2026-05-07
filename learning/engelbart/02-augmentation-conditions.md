---
layout: default
title: "증강 시스템 설계 조건·조립"
---

# 축 2 — 증강 시스템의 설계 조건과 조립

> Engelbart가 "어떻게 하면 도구가 인간 능력을 실제로 증강하는가"의 조건을 어떻게 명시했는지를 1차 자료에서 그대로 복원한다. 압축보다 정확.

## 1. H-LAM/T 프레임워크 — 4 결합 시스템

Engelbart의 1962년 보고서 *Augmenting Human Intellect: A Conceptual Framework* (SRI Report AFOSR-3223 / AUGMENT-3906) §II는 증강 시스템을 단일한 도구가 아니라 **사람을 중심에 둔 4 요소의 결합 시스템**으로 정의한다. 그 시스템의 이름이 H-LAM/T다 — *Human using Language, Artifacts, Methodology, in which he is Trained.*

증강의 정의 자체부터 인용하면:

> "By 'augmenting human intellect' we mean increasing the capability of a man to approach a complex problem situation, to gain comprehension to suit his particular needs, and to derive solutions to problems."
> ("인간 지능의 증강이란, 한 인간이 복잡한 문제 상황에 접근하고, 자기 자신의 필요에 맞는 이해를 얻고, 문제에 대한 해를 도출하는 능력을 키운다는 뜻이다." — Engelbart 1962, §I)

이 정의의 표적이 "지능 그 자체의 강화"가 아니라 **문제 상황에 접근·이해·해결하는 능력**이라는 점이 결정적이다. 증강은 IQ를 올리는 일이 아니라, 작업 사이클을 굴릴 수 있게 만드는 일이다.

§II에서 Engelbart는 증강의 수단(means)을 네 가지 부류로 명시한다. 그대로 인용하면 ([Doug Engelbart Institute, AUGMENT-3906](https://www.dougengelbart.org/pubs/augment-3906.html)):

1. **Artifacts** — *"physical objects designed to provide for human comfort, for the manipulation of things or materials, and for the manipulation of symbols."*
   ("인간의 편의, 사물·재료의 조작, 그리고 기호의 조작을 위해 설계된 물리적 객체.")

2. **Language** — *"the way in which the individual parcels out the picture of his world into the concepts that his mind uses to model that world, and the symbols that he attaches to those concepts."*
   ("개인이 세계의 그림을, 자기 마음이 그 세계를 모델링하는 데 쓰는 개념들로 분할하는 방식, 그리고 그 개념들에 붙이는 기호들.")

3. **Methodology** — *"the methods, procedures, strategies, etc., with which an individual organizes his goal-centered (problem-solving) activity."*
   ("개인이 목표 중심의 문제 해결 활동을 조직하는 방법, 절차, 전략 등.")

4. **Training** — *"the conditioning needed by the human being to bring his skills in using Means 1, 2, and 3 to the point where they are operationally effective."*
   ("인간이 1, 2, 3을 운영 가능한 수준으로 다룰 수 있도록 만드는 조건화.")

그리고 곧장 시스템 관점이 따라붙는다:

> "The system we want to improve can thus be visualized as a trained human being together with his artifacts, language, and methodology."
> ("우리가 개선하고 싶은 시스템은, 훈련된 한 인간과 그의 도구·언어·방법론이 함께 있는 모습으로 그릴 수 있다.")

여기서 핵심 명제 — **도구만 바꾸면 안 된다.** Artifacts 하나만 갈아끼우면 나머지 세 요소(Language, Methodology, Training)가 옛 도구 시대의 상태로 남아있어 새 도구의 능력을 흡수하지 못한다. Engelbart는 H-LAM/T를 "synergetic structure"로 표현한다 — 조직의 효과가 *"greater than the mere addition of their individual effects"* (개별 효과의 단순한 합보다 큰) 상태. 시너지는 네 요소가 서로의 진화를 강제하기 때문에 발생한다. 그가 §II에서 시너지를 지능의 원천 후보로 직접 지목한 표현이 있다: *"synergism is our most likely candidate for representing the actual source of intelligence."* ("시너지즘이 실제 지능의 원천을 대표할 가장 유력한 후보다.")

이 4 결합은 위계적이다. 기본 인간 능력과 기본 도구 능력이 바닥에 있고, 그 위에 더 복합적인 process capability들이 쌓인다. 어떤 process도 sub-process들로 분해되고, 그 sub-process들의 결합 방식 자체가 능력의 차이를 만든다. Engelbart에게 "지능"은 위계 안에서 process를 재조립하는 능력이다.

벽돌-연필 예시는 이 원리의 부정형 사례다. 연필 끝에 벽돌을 묶어두고 글을 써 보면, *"With the brick pencil, we are slower and less precise"* — 손은 같고 언어도 같지만 도구 한 요소가 망가지면 시스템 전체 능력이 무너진다. 거꾸로 읽으면, 좋은 도구 하나가 와도 언어·방법론·훈련이 따라붙지 않으면 같은 일이 일어난다.

## 2. A / B / C Activities — 작업의 3층 구조

Engelbart는 1962 보고서 이후 ARC와 Bootstrap Alliance에서 이 시너지 시스템이 *어떤 활동 구조* 안에서 실제로 굴러가는지를 ABC 모델로 정식화했다. 정본 정의는 [Doug Engelbart Institute, "ABC Model for Continuous Improvement"](https://dougengelbart.org/content/view/230/)에 그대로 있다:

> **A-Activity** — *"Consider the primary activity fulfilling the mission of the organization to be its 'A' Activity – be it building mouse traps, designing courseware, writing legislation, or addressing world hunger."*
> ("조직의 미션을 직접 수행하는 1차 활동을 'A' 활동으로 본다 — 쥐덫을 만들든, 교재를 설계하든, 법안을 쓰든, 기아 문제를 풀든.")
>
> **B-Activity** — *"Consider any effort to improve how the organization does its 'A' work to be its 'B' Activity – introducing new processes or tools, incentive programs, quality initiatives, etc."*
> ("조직이 A 작업을 *수행하는 방식 자체*를 개선하는 모든 노력을 'B' 활동으로 본다 — 새 프로세스나 도구의 도입, 인센티브 프로그램, 품질 이니셔티브 등.")
>
> **C-Activity** — *"Consider any effort in the organization to improve your 'B' Activity ... to be the organization's 'C' Activity. The 'C' Activity improves the improvement cycle time and quality of the organization."*
> ("B 활동 자체를 개선하는 모든 노력을 'C' 활동으로 본다. C 활동은 조직의 *개선 사이클의 속도와 질*을 개선한다.")

세 층은 자원 할당 관점에서 서로 다른 책임을 갖는다. A는 결과물을 만든다. B는 A의 도구·프로세스·언어·훈련을 갱신한다. C는 B가 그 갱신을 어떻게 학습·전파·재투자하는지를 갱신한다.

1991년 *Bootstrapping Organizations into the 21st Century* (AUGMENT-132803)에서 Engelbart는 B와 C가 일회성이어선 안 됨을 강조한다:

> "organizations must adopt a permanent and highly-coordinated *B Activity*, responsible for continuously identifying and implementing candidate improvements to the core business activity."
> ("조직은 영구적이고 고도로 조율된 B 활동을 채택해야 한다. 그 책임은 핵심 비즈니스 활동의 개선 후보들을 *지속적으로* 식별하고 도입하는 것이다.")
>
> "To improve this B Activity improvement capability, organizations will need to invest in an explicit on-going *C Activity*."
> ("이 B 활동의 개선 역량을 개선하려면, 조직은 명시적이고 *상시적인* C 활동에 투자해야 한다.")

이 두 문장의 형용사가 결정적이다 — **permanent**, **highly-coordinated**, **explicit**, **on-going**. 회고를 가끔 하는 게 B가 아니다. 회고를 하는 *방식 자체*를 갱신할 사람과 시간이 따로 없으면 C가 아니다.

## 3. Bootstrap — 자기 가속 메커니즘

Bootstrap은 ABC가 단순 위계가 아니라 *positive feedback loop*가 되는 순간을 가리킨다. Engelbart의 표현으로 ([Bootstrapping the 21st Century, AUGMENT-132803](https://dougengelbart.org/pubs/augment-132803-Bootstrapping.html)):

> *"a strategy for organizational fitness, including leveraging limited resources to effect dramatic, continuous, and rapid improvement."*
> ("제한된 자원을 지렛대로 써서 극적이고 지속적이며 빠른 개선을 일으키는, 조직 체력의 전략.")
>
> *"A key to the long-term vitality of an organization – to get better and better at improving itself."*
> ("조직의 장기 생명력의 열쇠 — *자기 자신을 개선하는 일에서 점점 더 나아지는* 것.")

"점점 더 나아진다"가 핵심이다. B 단독은 mildly-exponential — 매 사이클마다 A가 좋아지지만 사이클 자체의 효율은 일정하다. C가 붙으면 사이클 자체가 짧아지고 정확해지므로 곡선이 진짜 exponential로 휜다. Engelbart는 이를 두고 *compounding improvement capability curve*라고 부른다.

**ARC가 NLS를 NLS로 만들었다는 사실**이 이 이론의 살아있는 증거다. SRI의 Augmentation Research Center는 NLS의 모든 설계 문서, 회의록, 버그 리포트, 계획, 연구 노트를 NLS 자체로 작성·검색·교차참조했다. 1991년 보고서는 이 경험을 이렇게 회고한다: *"the human-system elements – all the methods, procedures, conventions, skills, etc. – must be highly developed, in close association with the continuing evolution of OHS requirements."* (도구 시스템의 진화에 *밀접하게 결합된 채로* 인간 시스템 요소들—방법, 절차, 관례, 기술 전부—이 함께 고도로 발전해야 한다.) 그리고 같은 보고서는 자기 시대의 함정을 지적한다: *"many organizations' Augmentation Systems are now heavily weighted with point-solution technology, seriously overpowering the human-system elements."* (지금 많은 조직의 증강 시스템은 단발성 기술 솔루션 쪽으로 심하게 기울어 있어, 인간 시스템 요소를 심각하게 압도한다.)

dogfooding과의 차이는 여기서 갈린다. dogfooding은 *자기 제품을 자기가 쓴다*에서 멈춘다 (B의 한 형태). Bootstrap은 *자기 제품으로 자기 제품의 개선 활동 자체를 운영*한다 — 즉 C가 같은 도구 위에서 돌아간다. NLS는 NLS로 NLS를 디자인했다.

이 구조의 사회적 확장이 **Networked Improvement Communities (NICs)** 다 — *"improvement communities specially designed to boost their own Collective IQ by applying their mission to themselves."* 자기 미션을 자기 자신에게 적용해서 집단 지능을 끌어올리는 공동체.

## 4. NLS의 구체 설계 결정과 그 의도

1968-12-09 SRI의 Fall Joint Computer Conference 데모(통칭 *The Mother of All Demos*)는 H-LAM/T의 4 요소가 *동시에* 진화한 결과를 90분에 압축해서 보여준다. [Doug Engelbart Institute의 1968 Demo Interactive 페이지](https://www.dougengelbart.org/firsts/1968-demo-interactive.html)와 표준 자료들에서 핵심 설계 결정을 그대로 추리면:

- **Mouse** — *"a pointing device with control buttons."* 화면 좌표 위에서 손의 위치를 직접 매핑. 의도: 타이핑 흐름을 끊지 않고도 정확한 포인팅을 가능하게 해, 사고와 조작 사이의 latency를 좁히는 것. 키보드와 동시에 운영.
- **Chord keyset** — Engelbart가 무대에서 부른 표현 그대로 *"the one hand equivalent of what you can do with a keyboard."* 5개 키의 동시 누름으로 31가지 코드. 의도: 한 손은 마우스, 다른 한 손은 키셋 — 손을 키보드와 마우스 사이로 *옮기지 않고* 명령과 입력을 흘려보내기 위한 양손 분업.
- **Hierarchical outline** — 모든 문서가 트리. 의도: 인간 사고가 위계로 분해된다는 §II의 process hierarchy 명제를 문서 표현에 그대로 박아 넣기.
- **Viewspecs** — view specification. 같은 파일을 outline level로 펼치거나 접고, 라인을 truncate하고, branch에 집중하고, 저자 정보를 켜고 끌 수 있다. 의도: 데이터는 하나, *바라보는 방식*은 작업 맥락마다 다르게. 도구를 작업자에게 맞추는 권한을 작업자에게 돌려주는 장치.
- **Verb-noun command language** — *"typing 'dw' causes 'Delete Word'"*. 의도: 명령을 자연어 흉내가 아니라 *학습 가능한 조작 언어*로 설계. Language(2번)와 Training(4번)이 도구 인터페이스 안으로 들어온 사례.
- **Cross-reference link / hypertext** — 문서 사이 점프, 텍스트와 그래픽 뷰 사이 traversal. 의도: 문서를 선형 출력물이 아니라 *탐색 가능한 그래프*로. 작업자의 사고 경로가 문서의 정렬 순서에 종속되지 않게 한다.
- **Real-time collaborative editing & video conferencing** — 무대의 Engelbart와 Menlo Park의 Bill Paxton이 같은 문서 위에서 *"bug fight"* 진행. 의도: 증강은 한 사람의 능력 강화가 아니라 사람-사람 결합의 강화. 협업이 도구의 부가기능이 아니라 본체.
- **Hot vs. Cold retrieval** — 목적지를 알 때(hot)와 모를 때(cold)의 정보 회수 모드를 분리. 의도: 작업의 인지 상태에 맞춰 검색 인터페이스가 갈라져야 한다는 인식.

각 결정의 공통 의도는 한 줄로 정리된다 — **사고 흐름의 latency와 모드 전환 비용을 깎아, 인간이 더 큰 문제 단위를 한 호흡에 잡게 만드는 것.** 이건 §I의 증강 정의("approach a complex problem situation, gain comprehension, derive solutions")의 직접 구현이다.

## 5. 증강 도구의 조건 리스트

Engelbart **본인이 명시한** 조건과, 위 1-4를 종합해 **이 리서치가 추출한** 조건을 구분해 적는다.

### Engelbart 본인이 명시

- **(E1) 시스템은 4 요소다 — Artifacts / Language / Methodology / Training이 함께 진화해야 한다.** (1962 §II) 도구만 바꾸는 개입은 H-LAM/T가 아니라 brick-pencil이다.
- **(E2) 활동은 3층이다 — A / B / C가 모두 살아 있어야 한다.** B는 일회성이 아니라 *permanent and highly-coordinated*, C는 *explicit and on-going*. (Bootstrapping the 21st Century, 1991)
- **(E3) 시스템은 자기 자신을 개선해야 한다 — bootstrap.** *"to get better and better at improving itself."* C 활동이 같은 도구 위에서 돌아갈 때 곡선이 휜다.
- **(E4) 인간 시스템과 도구 시스템은 균형을 잃으면 안 된다.** *"point-solution technology ... seriously overpowering the human-system elements"*는 실패 상태.
- **(E5) 시너지가 지능의 원천이다.** *"synergism is our most likely candidate for representing the actual source of intelligence."* 4 요소가 서로의 진화를 강제하지 않으면 합 이상이 나오지 않는다.
- **(E6) 증강의 표적은 IQ가 아니라 문제 접근·이해·해결 능력이다.** (1962 §I 정의)

### 이 리서치가 추출 (Engelbart 사상에 정합하나 그가 같은 문장으로 명시하지는 않은 형태)

- **(R1) 사용자는 도구의 한계를 푸는 권한을 가져야 한다.** Viewspecs와 verb-noun 명령어가 그 증거 — 도구의 모드를 작업자가 즉석에서 바꿀 수 있어야 증강이지, 정해진 모드만 강요하면 자동화에 가깝다.
- **(R2) 협업은 부가기능이 아니라 본체다.** 1968 데모의 split-screen 협업이 마지막 수서가 아니라 데모의 정점인 것은 의도적이다. 증강은 사람-사람 결합 위에서 정의된다.
- **(R3) 사고와 조작 사이의 latency를 깎는 것이 곧 증강이다.** Mouse + keyset의 양손 분업이 이 조건의 H/W 구현. 도구가 모드 전환을 강요하면 그만큼 사고가 끊긴다.
- **(R4) 도구의 데이터 모델은 사고의 위계를 그대로 받아써야 한다.** Hierarchical outline + cross-reference link가 그 사례 — 사고가 트리이자 그래프임을 거부하는 데이터 모델은 사고를 데이터 모델 쪽으로 끌어내린다.
- **(R5) 도구의 운영 기록도 그 도구로 처리되어야 한다 (self-hosting).** ARC가 NLS 운영을 NLS로 한 것이 dogfooding과 갈라지는 지점. C 활동이 같은 도구 위에 올라타 있을 때만 bootstrap이 작동한다.

## 6. 현재 작업 접점 — mirror-mind 운영·lighthouse 설계 관점

이 조건 리스트를 mirror-mind와 lighthouse 위에 직접 비춘다. 평가가 아니라 **어떤 자리에 무엇이 와 있고 무엇이 비어 있는지**를 보는 일이다.

- **A 활동** — lighthouse, soulmate, agentic-base, youngcompany 블로그 등 실제 제품/저작물이 만들어지는 자리. 코드 구현은 하위 프로젝트(lighthouse 등)로 위임하는 mirror-mind 정책 자체가 A를 어디에 두는지를 분명히 한다.
- **B 활동** — `operations.md`, `agentic-engineering-principles.md`, 주간 플랜(`tasks/weekly/`), 회고, 품질 게이트 프롬프트, codex 다차수 리뷰. A를 *수행하는 방식*을 갱신하는 자리. 이게 살아있다.
- **C 활동** — `mirror-mind-principle.md`, `AGENTS.md`, `agents-md-writing-guide.md`, 그리고 메모리 시스템(`memory/memory-architecture.md`)과 사실/해석 분리 구조. 즉 *B를 어떻게 굴릴지*에 대한 SSOT들. Engelbart 기준에서 보면 C가 *명시적으로 분리되어 있고*, 핵심 문서 수정에 합의 게이트가 있다는 점에서 *highly-coordinated*에 부합한다.
- **Bootstrap (self-hosting) 측면** — mirror-mind가 자기 자신을 mirror-mind로 운영하고 있는가. `memory/network/`, `tasks/weekly/`, `scripts/check.py`, work-start/work-end 트리거가 mirror-mind 안에서 mirror-mind 운영을 굴린다. NLS가 NLS를 운영했던 구조와 형식적으로 같다. 차이는, mirror-mind의 도구 일부(에디터, 셸, Claude Code 자체)는 외부에서 빌려온 점 — 즉 H-LAM/T의 Artifacts 층은 부분 self-host다.
- **lighthouse 설계 관점** — lighthouse가 "사람 + AI = 두 주체의 협력"을 표방한다면, 조건 (R2)와 (E1)이 직접 압력으로 작용한다. *언어*(propose 카드 스키마, FSM 상태 라벨), *방법론*(취소 구조 #51, 2층 FSM), *훈련*(사용자가 협업 모드를 익히는 경로)이 *도구 변경과 동시에* 갱신되지 않으면 brick-pencil 상태가 된다. propose 카드 Zod 스키마 단일 원본화는 (E1)의 Language 축을 도구 축에 맞춘 사례로 읽힌다.
- **빈자리 후보** — (R5)의 self-hosting 관점에서 보면, lighthouse 자체가 lighthouse의 개선 활동(B/C)을 운영하는 단계까지 가 있는지가 다음 질문이다. dogfooding(B)을 넘어 *lighthouse로 lighthouse의 회고·계획·기억을 운영하는*(C self-host) 단계가 bootstrap의 임계점이다.

---

**출처**
- Engelbart, D. C. (1962). *Augmenting Human Intellect: A Conceptual Framework.* SRI Summary Report AFOSR-3223 / AUGMENT-3906. https://www.dougengelbart.org/pubs/augment-3906.html
- Engelbart, D. C., & Lehtman, H. (1988-1991 계열). *Bootstrapping Organizations into the 21st Century — A Strategic Framework.* AUGMENT-132803. https://dougengelbart.org/pubs/augment-132803-Bootstrapping.html
- Doug Engelbart Institute, *ABC Model for Continuous Improvement.* https://dougengelbart.org/content/view/230/
- Doug Engelbart Institute, *1968 Demo Interactive.* https://www.dougengelbart.org/firsts/1968-demo-interactive.html
- *The Mother of All Demos*, SRI / Fall Joint Computer Conference, San Francisco, 1968-12-09.
